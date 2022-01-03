# Configuração de um servidor de gateway com Iptables/NAT

## 4º passo - habilitar o firewall e permitir o acesso ssh

```
sudo ufw enable
```
```
sudo ufw allow ssh
```
![4](https://github.com/MNahVR/Sred/blob/main/Galeria/4.png)


## 5º passo - habilitar o encaminhamento de pacotes das interfaces WAN para LAN

````
sudo nano /etc/ufw/sysctl.conf
````

### retirasse o "#" da frase, como mostra a imagem
![5](https://github.com/MNahVR/Sred/blob/main/Galeria/5.png)

## 6º passo  - conferir se os nomes das interfaces de rede, estão corretos
### WAN interface: ens160
### LAN interface: ens192


````
ifconfig -a
````
![6](https://github.com/MNahVR/Sred/blob/main/Galeria/6.png)


## 7º passo - recriar o arquivo /etc/rc.local

````
sudo nano /etc/rc.local
````

## 8º passo - transcrever o que está escrito abaixo no arquivo que foi criado

````
#!/bin/bash

# /etc/rc.local

# Default policy to drop all incoming packets.
# Politica padrão para bloquear (drop) todos os pacotes de entrada
iptables -P INPUT DROP
iptables -P FORWARD DROP

# Accept incoming packets from localhost and the LAN interface.
# Aceita pacotes de entrada a partir das interfaces localhost e the LAN.
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -i enp0s8 -j ACCEPT

# Accept incoming packets from the WAN if the router initiated the connection.
# Aceita pacotes de entrada a partir da WAN se o roteador iniciou a conexao
iptables -A INPUT -i enp0s3 -m conntrack \
--ctstate ESTABLISHED,RELATED -j ACCEPT

# Forward LAN packets to the WAN.
# Encaminha os pacotes da LAN para a WAN
iptables -A FORWARD -i enp0s8 -o enp0s3 -j ACCEPT

# Forward WAN packets to the LAN if the LAN initiated the connection.
# Encaminha os pacotes WAN para a LAN se a LAN inicar a conexao.
iptables -A FORWARD -i enp0s3 -o enp0s8 -m conntrack \
--ctstate ESTABLISHED,RELATED -j ACCEPT

# NAT traffic going out the WAN interface.
# Trafego NAT sai pela interface WAN
iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE

# rc.local needs to exit with 0
# rc.local precisa sair com 0
exit 0
````
![7](https://github.com/MNahVR/Sred/blob/main/Galeria/7.png)


## 9º passo - tornar o arquivo em executável e o deixá-lo inicializável no boot

````
sudo chmod 755 /etc/rc.local
````
## 10º passo - verificar o status do firewall

````
Esse,
sudo ufw status

ou,
systemctl status ufw.service
````

## 11º passo - reiniciar a máquina

````
sudo reboot
````

![9](https://github.com/MNahVR/Sred/blob/main/Galeria/9.png)

## 12º passo - encaminhamento de portas para acesso externo à serviços da rede interna.
### Adicione as informações do IPTABLES sobre portas, IP e Interface no arquivo /etc/rc.local
````
1º - entre no arquivo, com:
sudo nano /etc/rc.local

2º - adicione as informações a seguir:

iptables -A PREROUTING -t nat -i ens192 -p tcp –-dport 445 -j DNAT –-to 10.9.14.100:445
iptables -A FORWARD -p tcp -d 10.9.14.100 –-dport 445 -j ACCEPT

iptables -A PREROUTING -t nat -i ens192 -p tcp –-dport 139 -j DNAT –-to 10.9.14.100:139
iptables -A FORWARD -p tcp -d 10.9.14.100 –-dport 445 -j ACCEPT

iptables -A PREROUTING -t nat -i ens160 -p tcp –-dport 53 -j DNAT –-to 10.9.14.221:53
iptables -A FORWARD -p udp -d 10.9.14.221 –-dport 53 -j ACCEPT
````

![10](https://github.com/MNahVR/Sred/blob/main/Galeria/10.png)

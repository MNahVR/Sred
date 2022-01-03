# Configuração de um servidor de gateway com Iptables/NAT
## CONFIGURAÇÃO SAMBA

## 13º - Faça o update primeiro, e em seguida a instalação do samba

````
sudo apt update
````
![11](https://github.com/MNahVR/Sred/blob/main/Galeria/11.png)

````
sudo apt install samba
````

![12](https://github.com/MNahVR/Sred/blob/main/Galeria/12.png)

## 14º - Verifique se o samba esta indo
````
ou,
whereis samba

ou,
sudo systemctl status smbd

ou,
netstat -an | grep LISTEN
````
![13](https://github.com/MNahVR/Sred/blob/main/Galeria/13.png)

## 15º - Fazer backup do arquivo de configuração do samba

````
sudo cp /etc/samba/smb.conf{,.backup}
````

## 15º - Verificar se foi feito mesmo o backuo do arquivo e criar um arquivo novo somente com os comandos necessários

````
ls -la /etc/samba
````

````
sudo bash -c 'grep -v -E "^#|^;" /etc/samba/smb.conf.backup | grep . > /etc/samba/smb.conf'
````

````
sudo nano /etc/samba/smb.conf
````
![14](https://github.com/MNahVR/Sred/blob/main/Galeria/14.png)

## 16º - Editar arquivo digitado anteriormente (/etc/samba/smb.conf)

### Adicionar o que esta escrito abaixo no diretorio [global]:

````
interfaces = 127.0.0.1/8 ens160 ens192
````

### Adicionar também a parte do diretório [publico] no final do arquivo

````
[public]
   comment = public anonymous access
   path = /samba/public
   browsable =yes
   create mask = 0660
   directory mask = 0771
   writable = yes
   guest ok = no
   valid users = @sambashare
````
![15](https://github.com/MNahVR/Sred/blob/main/Galeria/15.png)


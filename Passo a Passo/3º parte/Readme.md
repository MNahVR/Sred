# Configuração de um servidor de gateway com Iptables/NAT
## CONFIGURAÇÃO SAMBA

## 13º - Faça o update primeiro, e em seguida a instalação do samba

````
sudo apt update
````

````
sudo apt install samba
````
## 14º - Verifique se o samba esta indo
````
ou,
whereis samba

ou,
sudo systemctl status smbd

ou,
netstat -an | grep LISTEN
````

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



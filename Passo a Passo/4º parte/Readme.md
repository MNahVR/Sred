# Configuração do Bind9 (DNS Server)

## 22º passo - Instalar o bind9, via apt-get (o bind9 é a aplicação de DNS que roda no servidor)

````
sudo apt-get install bind9 dnsutils bind9-doc
````
![24](https://github.com/MNahVR/Sred/blob/main/Galeria/24.png)

````
* Verifique seu status:

sudo systemctl status bind9

![25](https://github.com/MNahVR/Sred/blob/main/Galeria/25.png)

* Caso não rode:

sudo systemctl enable bind9
````

## 23º passo - Os diretórios do bind

````
* Verificar se os arquivos do bind ficam na no diretório /etc/bind:

ls -la /etc/bind
````
![26](https://github.com/MNahVR/Sred/blob/main/Galeria/26.png)

## 24º passo - As zonas

````
* Criar um diretório para armazendar os arquivos de zonas

sudo mkdir /etc/bind/zones
````


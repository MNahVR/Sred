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

* Criar um diretório para armazendar os arquivos de zonas
````
sudo mkdir /etc/bind/zones
````
![27](https://github.com/MNahVR/Sred/blob/main/Galeria/27.png)
````
Os arquivos db são bancos de dados de resolução de nomes, ou seja, quando se sabe o nome da máquina mas não se conhece o IP.

No nosso caso o domínio/zona local será labredes.ifalarapiraca.local e o arquivo db será db.labredes.ifalarapiraca.local
````

### 24.1º passo - zona direta

Para que o arquivo db.labredes.ifalarapiraca.local contenha os nomes das máquinas do domínio labredes.
ifalarapiraca.local, é necessário que se faça uma cópia do arquivo /etc/bind/db.empty.

````
sudo cp /etc/bind/db.empty /etc/bind/zones/db.labredes.ifalarapiraca.local 
````

### 24.2º passo - zona reversa

Vamos criar a zona reversa a partir do arquivo /etc/bind/db.127.

OBS: ela é utilizada quando não se conhece o IP mas sabe-se o nome do host.


````
sudo cp /etc/bind/db.127 /etc/bind/zones/db.10.9.14.rev
````


## 25º passo - Editar arquivos db

### 25.1º passo - zona direta: db.labredes.ifalarapiraca.local

Editar o arquivo e adicionar informações a respeito do domínio.

````
sudo nano /etc/bind/zones/db.labredes.ifalarapiraca.local
````


### 25.2º passo - zona reversa: db.10.9.14.rev

Editar o arquivo e adicionar as informações da zona reversa.

````
sudo nano /etc/bind/zones/db.10.9.14.rev
````

## 26º passo - Configuração do named.conf.local

Para ativar as zonas descritas nos arquivos db deve-se:

Editar o arquivo de configuracão do bind para informar onde eles foram salvos.

````
sudo nano /etc/bind/named.conf.local
````

## 27º passo - Verificação de sintaxe

Checar a sintaxe de configuração do BIND.

````
sudo named-checkconf
````

## 28º passo - Verificar a sintaxe dos arquivos de dados

Verificar se a formatação da sintaxe dos arquivos db está correta.

### 28.1º passo - Entrar no diretório zones

````
cd /etc/bind/zones
````

### 28.2º passo - Digitar os comandos e verificar se está certo

````
sudo named-checkzone labredes.ifalarapiraca.local db.labredes.ifalarapiraca.local

&

sudo named-checkzone 14.9.10.in-addr.arpa db.10.9.14.rev
````

## 29º passo - Configurar para somente resolver endereços IPv4

### 29.1º passo - Entrar em /etc/default/named

````
sudo nano /etc/default/named
````

### 29.2º passo - Adicionar o -4 na seguinte linha OPTIONS="-u bind"

````
*Exemplo:

# run resolvconf?
RESOLVCONF=no

# startup options for the server
OPTIONS="-4 -u bind"
````

## 30º passo - Reiniciar o BIND

````
sudo systemctl restart bind9
````

## 31º passo - Configuração dos clientes

Configurar o DNS na máquina srv01 na interface de rede local (ens160).

````
sudo systemctl restart bind9
```

### 31.1º passo - Entrar em /etc/netplan/00-installer-config.yaml

````
sudo nano /etc/netplan/00-installer-config.yaml
````

### 31.2º passo - Configurando 

````
Antes
````
````
Depois
````

## 32º passo - Testar servidor DNS

Observe se o DNS servers e DNS Domain estão corretos.

````
systemd-resolve --status ens160
````
## 33º passo - Garantir que o serviço DNS resolve o DNS do Google

````
ping google.com
````

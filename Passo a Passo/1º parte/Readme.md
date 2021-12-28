# Configuração de IP estático e DNS na interface de rede


## 1º passo - Editar o arquivo 00-installer-config.yaml

Para isso, digite:
```
sudo nano /etc/netplan/00-installer-config.yaml
```
![1](https://github.com/MNahVR/Sred/blob/main/Galeria/1.png)

## 2º passo - Configuração do arquivo
```
network:
    ethernets:
        ens160:          
            dhcp4: false                  
            addresses: [10.9.14.121/24]   
            gateway4: 10.9.14.1             
                addresses:
                   - 8.8.8.8             
                   - 8.8.4.4             
                search: []                
        ens192:                           
            addresses: [192.168.0.161/29] 
    version: 2
```
![2](https://github.com/MNahVR/Sred/blob/main/Galeria/2.png)

## 3º passo - Aplicar as configurações e depois vê-las

```
sudo netplan apply
```

```
ifconfig -a
```
![3](https://github.com/MNahVR/Sred/blob/main/Galeria/3.png)
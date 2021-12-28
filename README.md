## CABEÇALHO
* IFAL - campus Arapiraca
* Aluna: Maria Nathálya Veiga Rodrigues
* Turma: 914

OBS: usei a VM do Guilherme Lima, que saiu do Ifal.

## INTRODUÇÃO
Nesta atividade requeresse a configuração da VM para implementação do SAMBA, que é um serviço de compartilhamento de arquivos, e do servidor de resoluçao de DNS, BIND9.

## Tabelas das Configurações de Rede

* Rede interna

| DESCRIÇÃO   | IP            |
|:------------|:------------- |
| Rede        | 10.9.14.0     |
| Máscara     | 255.255.255.0 |
| VirtualBox (gateway)     | 10.9.14.1      |
| Broadcast   | 10.9.14.255  |
| srv01         | 10.9.14.121   |
| samba       | 10.9.14.121   |

* Rede externa

|  DESCRIÇÃO  |       IP      |
|:------------|:------------- |
| Rede        | 192.168.0.201 |
| Máscara     | 255.255.255.0 |
| VirtualBox (gateway)     | 192.168.0.1 |
| Broadcast   | 192.168.0.255 |

* Servidores

|    Nome da VM     |                       NOME                           |
|:------------------|:-----------------------------------------------------|
| Gateway (gw)      | gw.nathalya_914.labredes.ifalarapiraca.local     |
| server01 (srv01) | srv01.nathalya_914.labredes.ifalarapiraca.local    |
| Samba-SRV.        | srv.nathalya_914.labredes.ifalarapiraca.local  |

### CONFIGURAÇÕES - Passo a Passo

1º Parte - [Configuração de IP estático e DNS na interface de rede](https://github.com/MNahVR/Sred/blob/main/Passo%20a%20Passo/1%C2%BA%20parte/Readme.md)

2º Parte - [Configuração de um servidor de gateway com Iptables/NAT](https://github.com/MNahVR/Sred/blob/main/Passo%20a%20Passo/2%C2%BA%20parte/Readme.md)

3º Parte - [Configuração de um servidor de arquivos com Samba](https://github.com/MNahVR/Sred/tree/main/Passo%20a%20Passo/3%C2%BA%20parte)

4º Parte - [Configuração dos servidores DNS Master e Slave](https://github.com/MNahVR/Sred/tree/main/Passo%20a%20Passo/4%C2%BA%20parte)
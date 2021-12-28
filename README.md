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

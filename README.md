# Como usar:

Estas configurações foram feitas apenas para fins acadêmicos. Este é um teste simples dos protocolos de roteamento OSPF e RIP, você pode usá-lo com 3 Máquinas Virtuais funcionando como roteadores.

Nota: Para que funcione, configurações adicionais podem ser necessárias no software da VM, como ativar as configurações de "Rede Interna" e "Modo Promíscuo".

# Configurar netplan de cada roteador para configurar o DHCP básico e o IP Estático:

## R1:

```yaml
network:
  version: 22
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      addresses: [192.168.12.1/24]
``` 

Em seguida, ``sudo netplan apply``.


## R2:

```yaml
network:
  version: 22
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      addresses: [192.168.12.2/24]
    enp0s9:
      addresses: [192.168.23.2/24]
```

Em seguida, ``sudo netplan apply``.

## R3:

```yaml
network:
  version: 22
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      addresses: [192.168.23.3/24]`
```
Em seguida, ``sudo netplan apply``.

# Instale o BIRD

``sudo apt-get update``

``sudo apt-get install bird``

# Em cada roteador, substitua o conteúdo dos arquivos bird.config pelos arquivos de configuração OSPF **OU** RIP do repositório:

Você pode editar pelo editor nano com: 

``sudo nano etc/bird/bird.config``

Nota: Em alguns casos, é necessário autorização de superuser para modificar esse arquivo, para isso, use ``sudo su``.

# Comandos para verificar e testar conexão:

``birdc show status``

``birdc show protocols``

``birdc show protocols all rip1``

``birdc show protocols all ospf``

``birdc show route protocol rip1``

``birdc show route protocol ospf``

``birdc show route``

``ping 192.168.xx.xx``

``traceroute 192.168.xx.xx``

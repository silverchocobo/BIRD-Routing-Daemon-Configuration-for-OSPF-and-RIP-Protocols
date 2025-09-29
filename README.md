## Notes:

This configurations were made for academical purposes only. This is a simple test of OSPF and RIP routing protocols, you can use it with 3 Virtual Machines working as routers.

Note: To make it functional, additional configurations might be needed on the VM software, like activating the "Internal Network" and "Promiscuous Mode" configurations, plus adding these scripts on the netplan of each router to set up the basic DHCP and Static IP:

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

Then, ``sudo netplan apply``.


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

Then, ``sudo netplan apply``.

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
Then, ``sudo netplan apply``.

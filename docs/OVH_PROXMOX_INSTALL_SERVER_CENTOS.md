# SERVER INSTALL WITH CENTOS

> Manuel d'installation de serveurs dédiés
[Configurer une IP Fail Over sur CentOS](https://www.ovh.com/us/g2044.configure_a_failover_ip_with_centos)

## Installation de machines sur serveur dédié OVH avec PROXMOX

> on CENTOS 7

1. Récupérer l'adresse mac virtuelle depuis le manager OVH
2. Se connecter avec l'utilisateur ROOT depuis l'interface PROXMOX
3. Installer internet sur la VM *(config OVH)*

vi /etc/sysconfig/network-scripts/ifcfg-ens18

    DEVICE=ens18
    HWADDR=ADRESSE.MAC.DE.VOTREIP
    TYPE=Ethernet
    ONBOOT=yes
    BOOTPROTO=none
    USERCTL=none
    PEERDNS=yes
    IPADDR=IP.FAIL.OVER
    IPV6INIT=no
    NETMASK=255.255.255.255
    GATEWAY=IP.DE.VOTREDEDIE.254


vi /etc/sysconfig/network-scripts/route-ens18

    IP.DE.VOTREDEDIE.254 – 255.255.255.255 ens18
    default IP.DE.VOTREDEDIE.254


vi /etc/resolv.conf

    nameserver 213.186.33.99

/etc/init.d/network restart

> Redémarrer la machine virtuelle si problème

4. Installer les dépôts absents si besoin

sudo yum install epel-release

[...]

5. Installer OPENSSH

yum install openssh openssh-server

6. Installer les clés SSH

Si le fichier n'existe pas le créer comme ceci:

    cd ~
	mkdir .ssh
	touch .ssh/authorized_keys
	chmod 700 .ssh
	chmod 600 .ssh/authorized_keys

7. Tester la connexion

8. Sécuriser la connexion (à minima)

nano /etc/ssh/sshd_config

    ServerKeyBits 2048
    PermitRootLogin no
    PasswordAuthentication no

/etc/init.d/ssh restart

9. Installer Python

sudo yum -y install python36u

10. Execute Ansible script

> SECURISER LE SERVEUR
> AND IT'S DONE!

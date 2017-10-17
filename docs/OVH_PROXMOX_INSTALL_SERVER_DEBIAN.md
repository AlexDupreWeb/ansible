# SERVER INSTALL WITH DEBIAN

> Télécharger l'iso ICI

    cd /var/lib/vz/template/iso/
    wget http://cdimage.debian.org/debian-cd/8.5.0/amd64/iso-cd/debian-8.5.0-amd64-netinst.iso

> Manuel d'installation de serveurs dédiés
[Configurer une IP Fail Over sur Debian](https://www.ovh.com/fr/g2042.configurer_une_ip_fail_over_sur_debian)

## Installation d'un serveur PROXMOX sur serveur dédié OVH

Utiliser les templates OVH

> SECURISER LE SERVEUR

## Installation de machines sur serveur dédié OVH avec PROXMOX

> on DEBIAN 8.4

1. Récupérer l'adresse mac virtuelle depuis le manager OVH
2. Se connecter avec l'utilisateur ROOT depuis l'interface PROXMOX
3. Installer internet sur la VM *(config OVH)*

nano /etc/network/interfaces

    auto lo eth0
    iface lo inet loopback
    iface eth0 inet static
            address IP.FAIL.OVER
            netmask 255.255.255.255
            broadcast IP.FAIL.OVER
            post-up route add IP.DE.VOTREDEDIE.254 dev eth0
            post-up route add default gw IP.DE.VOTREDEDIE.254
            post-down route del IP.DE.VOTREDEDIE.254 dev eth0
            post-down route del default gw IP.DE.VOTREDEDIE.254

nano /etc/resolv.conf

    nameserver 213.186.33.99

/etc/init.d/networking restart

> Redémarrer la machine virtuelle si problème

4. Installer les dépôts DEBIAN

nano /etc/apt/sources.list

    deb http://ftp.fr.debian.org/debian jessie-backports main contrib non-free
    deb http://ftp.debian.org/debian jessie main contrib non-free

5. Installer OPENSSH

apt-get install openssh-server

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

apt-get install python

10. Execute Ansible script

> SECURISER LE SERVEUR
> AND IT'S DONE!

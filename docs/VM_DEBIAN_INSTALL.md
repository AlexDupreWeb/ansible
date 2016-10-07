# VIRTUAL MACHINE INSTALL

> Virtual machine install  dor development

# On DEBIAN 8.4

1. Update package

    apt-get update
    apt-get upgrade

2. Install SSH server

    apt-get install openssh-server

3. Install packages
Manual mode:


    apt-get install htop
    #apt-get install git
    apt-get install apache2
    apt-get install mod_proxy
    apt-get install mod_proxy_http
    apt-get install mod_rewrite
    apt-get install mod_headers

    apt-get install php5
    #apt-get install php5-curl
    #apt-get install php-mcrypt

    apt-get install mysql-server

    apt-get install sudo
    add user alexandre sudo


Or use Ansible (as you want)

4. Mount share folder
To start, mount the folder in permanent mode



Next VM configuration:

> In case of problem: http://pazpop.fr/installer-les-additions-invite-de-virtualbox-sur-debian-8/

    nano /etc/group vboxsf:x:1001:www-data

    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install build-essential module-assistant

    sudo apt-cache search linux-headers-$(uname -r)
    sudo apt-get install linux-headers-$(uname -r)

    mount /media/cdrom
    sh /media/cdrom/VBoxLinuxAdditions.run --nox11
    shutdown -r

> Note: Create your dest folder...

    mount -t vboxsf shared_name /destination_folder
    sudo ln -s /destination_folder symbolic_link_name
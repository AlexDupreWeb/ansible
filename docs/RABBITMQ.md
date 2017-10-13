## RABBITMQ SERVER

### INSTALLATION

- Par le gestionnaire de packet DEBIAN
- Et si ce n'est pas la dernière version
  - `wget <urlOfPackage> --no-check-certificate` du dernier package de rabbitmq-server
  - `dpkg -i <packageName>`
  - `apt-get -f install` si il manque des dépendances

> Vérifier le bon fonctionnement de rabbitmq `rabbitmqctl status`

**Les commandes utiles**
- `service rabbitmq-server start`
- `service rabbitmq-server stop`
- `service rabbitmq-server restart`
- `rabbitmqctl start`
- `rabbitmqctl stop`
- `rabbitmqctl restart`
- `rabbitmqctl list_queues`
- `rabbitmq-plugins list`
- `rabbitmqctl add_user`
- `rabbitmqctl delete_user`


**Documentation**
- :feet: [Installation](https://www.rabbitmq.com/install-debian.html)
- :paperclip: [Fichier de configuration](https://www.rabbitmq.com/configure.html#configuration-file)
- :whale: [Container Docker](https://hub.docker.com/r/rafakato/rabbitmq-delayed-message-exchange)

**Plugin pour le délai**
- Download the plugin `wget http://www.rabbitmq.com/community-plugins/v3.6.x/rabbitmq_delayed_message_exchange-0.0.1.ez`
- Copy plugin into rabbitmq repository `sudo cp rabbitmq_delayed_message_exchange-0.0.1.ez /usr/lib/rabbitmq/lib/rabbitmq_server-3.6.10/plugins/`
- Check if plugin is correctly added `ls -lah /usr/lib/rabbitmq/lib/rabbitmq_server-3.6.10/plugins/`
- Enable plugin `rabbitmq-plugins enable rabbitmq_delayed_message_exchange`
- Enable plugin `rabbitmq-plugins enable rabbitmq_consistent_hash_exchange`
- Check if plugins are enabled `rabbitmq-plugins list`

### POC

1. Configuration des 2 vhost consumer + publisher

```
# Sur la VM
apt-get install apache2
echo "deb http://packages.dotdeb.org jessie all" > /etc/apt/sources.list.d/dotdeb.list
wget https://www.dotdeb.org/dotdeb.gpg --no-check-certificate && apt-key add dotdeb.gpg
apt-get update
apt install php7.0 libapache2-mod-php7.0 php7.0-mysql php7.0-curl php7.0-json php7.0-gd php7.0-mcrypt php7.0-msgpack php7.0-memcached php7.0-intl php7.0-sqlite3 php7.0-gmp php7.0-geoip php7.0-mbstring php7.0-xml php7.0-zip php7.0-bcmath
```

2. Configuration des utilisateurs

```
rabbitmqctl add_user <YOUR_USERNAME> <YOUR_PASSWORD>
rabbitmqctl set_user_tags <YOUR_USERNAME> administrator
rabbitmqctl set_permissions -p / <YOUR_USERNAME> ".*" ".*" ".*"
```

### :whale: DOCKER

- `docker pull rafakato/rabbitmq-delayed-message-exchange`
- `docker run -d --hostname rabbitmq --name rabbitmq -p 5672:5672 -p 15672:15672 rafakato/rabbitmq-delayed-message-exchange`
- `docker start rabbitmq`

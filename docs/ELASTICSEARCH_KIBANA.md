# HOW TO INSTALL ELASTICSEARCH AND KIBANA

> https://www.elastic.co/start

## Requirements

```bash
# JAVA 8 Required
# Install dep | Install package | Configure as default
sudo nano /etc/apt/sources.list.d/java-8-debian.list
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886
sudo apt-get update
sudo apt-get install oracle-java8-installer
java -version
sudo apt-get install oracle-java8-set-default
```

## Install

Elasticsearch
```bash
sudo apt-get install apt-transport-https
echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
sudo apt-get update && sudo apt-get install elasticsearch
```

Kibana
```bash
sudo apt-get install apt-transport-https
echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
sudo apt-get update && sudo apt-get install kibana
```

Configure
```bash
cd /usr/share/elasticsearch/
bin/elasticsearch-plugin install x-pack

cd /usr/share/kibana/
bin/kibana-plugin install x-pack

cd /usr/share/elasticsearch/
bin/elasticsearch

cd /usr/share/kibana/
bin/kibana

```

/usr/share/elasticsearch/bin/elasticsearch

Open your Browser:
`http://localhost:5601`

Enter credentials
Username: `elastic` Password: `changeme`

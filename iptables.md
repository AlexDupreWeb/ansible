#Les bases IPTABLES

Lister les regles IPTABLES

    sudo iptables -L --line-numbers


Ajouter une entrée aux règles IPTABLES

    sudo iptables -A INPUT -p all -s 91.134.27.3 -m comment --comment "SHINKEN"  -j ACCEPT


Supprimer une entrée aux règles IPTABLES

    sudo iptables -D INPUT 36


Sauvegarder les règles IPTABLES

*En mode root*

    iptables-save -c > /etc/iptables-save


Ajouter les autorisations SNMP aux règles IPTABLES

    sudo iptables -I INPUT 3 -p udp -i eth0 --dport 161 -j ACCEPT
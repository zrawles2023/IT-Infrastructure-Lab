#Create file for Reverse DNS
sudo nano /etc/bind/db.192.168.50

#Configure Reverse DNS and Assign addresses

$TTL 604800
@   IN  SOA ns1.internal.lan. admin.internal.lan. (
          2         ; Serial
     604800         ; Refresh
      86400         ; Retry
    2419200         ; Expire
     604800 )       ; Negative Cache TTL

@       IN  NS      ns1.internal.lan.

3       IN  PTR     ns1.internal.lan.
4       IN  PTR     client01.internal.lan.
5       IN  PTR     client02.internal.lan.


#Configure local configuration to include Reverse DNS

sudo nano /etc/bind/named.conf.local

zone "50.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/db.192.168.50";
};

#Check file for errors
sudo named-checkconf
sudo named-checkzone 50.168.192.in-addr.arpa /etc/bind/db.192.168.50

#Testing from Client01 ONLY (Static IP)
dig -x 192.168.50.3 +short

Output:ns1.internal.lan


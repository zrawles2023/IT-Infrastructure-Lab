sudo apt update
sudo apt install isc-dhcp-server




//edit main config file
sudo nano /etc/dhcp/dhcpd.conf

# DHCP Configuration for internal.lan (invaid)
option domain-name for "internal.lan";
option domain-name-servers 192.168.50.3;  # DNS server IP (IT-Server)

default-lease-time 600;
max-lease-time 7200;

subnet 192.168.50.0 netmask 255.255.255.0 {
  range 192.168.50.100 192.168.50.150;
  option routers 192.168.50.1; # No real router, but required by DHCP
}


sudo nano /etc/default/isc-dhcp-server

INTERFACESv4="" -> INTERFACESv4="enp0s8"

ip link




#restart server
sudo systemctl restart isc-dhcp-server
sudo systemctl enable isc-dhcp-server
sudo systemctl status isc-dhcp-server



#dhcp server status was inactive. used " sudo journalctl -xeu isc-dhcp-server.service to view log for issues
#Issues resolved, invalid system in configuration file, additionla "for".

# DHCP Configuration for internal.lan (valid)
option domain-name "internal.lan";
option domain-name-servers 192.168.50.3;  # Your DNS server IP (IT-Server)

default-lease-time 600;
max-lease-time 7200;

subnet 192.168.50.0 netmask 255.255.255.0 {
  range 192.168.50.100 192.168.50.150;
  option routers 192.168.50.1; # No real router, but required by DHCP
}



#Configure Client-02 for DHCP

sudo nano /etc/netplan/*.yaml

network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: true


sudo netplan apply

#check ping validation
ip a
ping it-server.internal.lan



--------------

The DHCP server is running and handing out IP addresses in the specified range.

Client-02 now properly receives IP and DNS settings via DHCP on the correct network interface (enp0s3).

DNS resolution for internal hosts (ns1.internal.lan) is confirmed working.



#Install Samba
sudo apt update
sudo apt install samba -y


#Shared file directory with guest access
sudo mkdir -p /srv/shared
sudo chown nobody:nogroup /srv/shared
sudo chmod 0775 /srv/shared

#Edit Samba config to allow guest access
sudo nano /etc/samba/smb.conf
   
   [Shared]
   path = /srv/shared
   browsable = yes
   read only = no
   guest ok = yes
   force user = nobody

#Restart and check status us Samba
sudo systemctl restart smbd
sudo systemctl status smbd

#Allow through UWF
sudo ufw allow 'Samba'

#Access the shared file from Client01 
smbclient //192.168.50.3/Shared -N

#Create a test file for shared folder (IT Server)
echo "Test file from IT Server" | sudo tee /srv/shared/hello.txt

#Verify files on Client01 
smb: \> ls

  Output:
         smb: \> ls
         .               D   0   SUN JUN 29 11:14:53 2025
         ..              D   0   SUN JUN 29 11:14:53 2025
         hello.txt       N   25  SUN JUN 29 11:14:53 2025

                    12028924 blocks of sizw 1024. 6173908 blocks available
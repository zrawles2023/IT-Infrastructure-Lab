
#Update and install Apache Web Server

sudo apt update 
sudo apt install apache2 -y

#Install PHP
sudo apt install php php-cli php-common php-curl php-gd php-imap php-mysql php-mbstring php-xml php-zip php-bz2 php-intl php-ldap libapache2-mod-php unzip -y

#Install MariaDB
sudo apt install mariadb-server -y

#Create the database for GLPI
sudo mysql -u root -p

#mysql commands for database
CREATE DATABASE glpidb CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

CREATE USER 'glpiuser'@'localhost' IDENTIFIED BY 'ticketpass';

GRANT ALL PRIVILEGES ON glpidb.* TO 'glpiuser'@'localhost';

FLUSH PRIVILEGES;

EXIT;

#Download GLPI and extract it
wget https://github.com/glpi-project/glpi/releases/download/10.0.15/glpi-10.0.15.tgz
tar -xzf glpi-10.0.15.tgz
sudo mv glpi /var/www/html/

#set permissions
sudo chown -R www-data:www-data /var/www/html/glpi
sudo chmod -R 755 /var/www/html/glpi

#Apache configuration to use ns1.internal.lan instead of IT Server IP
sudo nano /etc/apache2/sites-available/glpi.conf

<VirtualHost *:80>
    DocumentRoot /var/www/html/glpi
    ServerName it-server.internal.lan

    <Directory /var/www/html/glpi>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>

#Confirm and restart Apache 
sudo a2ensite glpi.conf
sudo a2enmod rewrite
sudo systemctl restart apache2

#Initial Login Info (default)
Role	     Username	    Password
Admin	       glpi	      glpi
Technician     tech	      tech
Normal User    normal	      normal
Post-only      postonly	      postonly



#Need to run on IT Server so GLPI Ticketing is active
sudo systemctl status apache2
sudo systemctl status mariadb
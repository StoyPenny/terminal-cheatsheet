# Server

This is a quick reference guide on common terminal commands for setting up and maintaining your server. 

---------------
<br><br>

### Install Apache
Install Apache on your server.
```cmd
sudo apt install apache2
```
<br>

### Install MySQL
Install the MySQL database on your server.
```cmd
sudo apt install mysql-server
```
<br>

Secure the installation
```cmd
sudo mysql_secure_installation
```
<br>

### Install PHP with Apache
Install PHP on your server that utilizes Apache. Choose the one that includes the modules you need or customize this command to fit your needs. After installing PHP, be sure to restart your apache server.

Install PHP with apache module
```cmd
sudo apt install php libapache2-mod-php
```

Install PHP with common PHP modules
```cmd
sudo apt install php libapache2-mod-php php-opcache php-cli php-gd php-curl php-mysql
```

Install PHP with required PHP modules for WordPress
```cmd
sudo apt install php7.2 libapache2-mod-php7.2 php7.2-common php7.2-mbstring php7.2-xmlrpc php7.2-gd php7.2-xml php7.2-mysql php7.2-cli php7.2-zip php7.2-curl
```

Restart the apache server
```cmd
sudo systemctl restart apache2
```
<br>

### Install PHP with NGINX
Install PHP on your server that utilizes Apache.
```cmd
sudo apt install php-fpm // Install PHP with apache module
sudo systemctl restart nginx // Restart the server
```
<br>

### Install PHP Modules
Install a specific PHP module on your server.
```cmd
sudo apt install php-[extname] // Replace extname with your extensions's name
```
<br>

### Show All PHP Modules
Show all of the PHP Modules that are installed on your server.
```cmd
php -m // Show all PHP modules
php -m | grep -i mongo // Search for a PHP module (mongo)
```
<br>

### Configure PHP.ini
Open the php.ini file
```cmd
sudo nano /etc/php/7.2/apache2/php.ini
```

Configure with the following values or values of your own.
```
file_uploads = On
allow_url_fopen = On
memory_limit = 256M
upload_max_filesize = 100M
max_execution_time = 360
date.timezone = America/Chicago
```
<br>

### Configure Virtual Host for Apache2
Create and open a file for your new Virtual Host, this should match your website name. 
```cmd
sudo nano /etc/apache2/sites-available/wordpress.conf
```

Add the following to your file, customizing the DocumentRoot, ServerName, & ServerAlias values to match your setup.
```
<VirtualHost *:80>
     ServerAdmin admin@example.com
     DocumentRoot /var/www/html/wordpress/
     ServerName example.com
     ServerAlias www.example.com

     <Directory /var/www/html/wordpress/>
        Options +FollowSymlinks
        AllowOverride All
        Require all granted
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
```

Enable the Website
```cmd
sudo a2ensite wordpress.conf
```

Enable the Rewrite Module
```cmd
sudo a2enmod rewrite
```

Restart Apache 
```cmd
sudo systemctl restart apache2
```

Composer

This is a quick reference guide on common Composer terminal commands. For more details on using composer with Ubuntu, [see this article](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-ubuntu-18-04).

---------------
<br><br>

### Install Composer
First, you will need to get and install all of the dependencies for composer to work.
```cmd
sudo apt install curl php-cli php-mbstring git unzip
```

Navigate to your home directory and download the installer file
```cmd
cd ~
curl -sS https://getcomposer.org/installer -o composer-setup.php
```

Install Composer Globablly
```cmd
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

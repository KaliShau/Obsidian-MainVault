
___
##### Install:
```ZSH
sudo pacman -S apache
sudo systemctl start httpd
```
##### Settings:
```ZSH
sudo nano /etc/httpd/conf/httpd.conf

# Not comment
LoadModule rewrite_module modules/mod_rewrite.so
LoadModule php_module modules/libphp.so
Include conf/extra/php_module.conf
```
##### Install PHP:
```ZSH
sudo pacman -S php php-apache

# and add
sudo nano /etc/httpd/conf/httpd.conf
<FilesMatch \.php$>
    SetHandler application/x-httpd-php
</FilesMatch>

# and add not comment
sudo nano /etc/php/php.ini
extension=mysqli
```
##### Install database: [[MariaDB]]
##### Create database:
```SQL
CREATE DATABASE wordpress_db;
CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
##### Install WordPress:
```ZSH
cd /srv/http

sudo wget https://wordpress.org/latest.zip
sudo unzip latest.zip -d wordpress
```
##### Set the correct access rights:
```ZSH
sudo chown -R Shau:http /srv/http/wordpress
```
##### Create config file:
```ZSH
cd /etc/httpd/conf
sudo mkdir vhosts
cd vhosts
sudo touch wordpress.conf
sudo nano wordpress.conf

# add
<VirtualHost *:80>
    DocumentRoot "/srv/http/wordpress"
    ServerName wordpress.local
    <Directory "/srv/http/wordpress">
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```
##### Turn on virtual hosts:
```ZSH
sudo nano /etc/httpd/conf/httpd.conf

# add 
Include conf/vhosts/*.conf
```
##### Local hosts:
```ZSH
sudo nano /etc/hosts

127.0.0.1   wordpress.local
```
##### Restart Apache:
```ZSH
sudo systemctl restart httpd
```

##### If it does not start:
```ZSH
# comment
#LoadModule mpm_event_module modules/mod_mpm_event.so

# not comment
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so
```
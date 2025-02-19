
___
##### Install:
```ZSH
# install and start
sudo pacman -S mariadb
sudo systemctl start mysqld

# initial setting
sudo mysql_secure_installation

mysql -u root -p
```
##### Enter:
```ZSH
mysql -u root -p
```
##### Create user add grants:
```SQL
CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'user'@'localhost';
FLUSH PRIVILEGES;
```
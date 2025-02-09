
___
##### Install:
```
# install and start
sudo pacman -S mariadb
sudo systemctl start mysqld

# initial setting
sudo mysql_secure_installation

mysql -u root -p
```
##### Enter:
```
mysql -u root -p
```
##### Create user add grants:
```
CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'user'@'localhost';
FLUSH PRIVILEGES;
```
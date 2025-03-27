
___
#### Добавить пользователя:
```ZSH
useradd admin
```

#### Смена пароля:
```ZSH
passwd admin
```

#### Выдача прав sudo:
```ZSH
sudo usermod -aG sudo admin

sudo mkdir -p /home/admin # Создание директории админа
sudo chown admin:admin /home/admin # Изменение владельца
sudo chmod 700 /home/admin # Выдача прав
```
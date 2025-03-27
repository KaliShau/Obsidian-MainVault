
___
1. После переход на сервер по [[Ssh]] нужно скачать репозиторий: git clone и настроить ssh ключи для установки обновлений и безопасности [[ssh-keygen]].
2. Далее нужна node js: 
```ZSH
curl -o- https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
```
И нужно перезапустить терминал
3. Установка lts версии: nvm install --lts
4. Если использовался npm в разработке используем его, в противном случае качаем свой менеджер: npm install -g pnpm
5. Качаем пакеты: pnpm i 
6. Собираем проект: pnpm build (может понадобится добавить .env)
7. Запускаем менеджер процессов [[pm2]]: npx pm2 start pnpm --name client -- start
8. Собираем остальные части: сервер и БД
9. Настройка автозапуска: npx pm2 startup и npx pm2 save
10. Настройка firefall: 
```ZSH
sudo apt install ufw

sudo ufw allow ssh # Разрешения доступа по ssh
sudo ufw allow http # Разрешения доступа по http

sudo ufw enable
```
11. Далее идет базовая настройка nginx: [[Nginx]]
12. Установка ssl сертификатов [[Ssl]]]
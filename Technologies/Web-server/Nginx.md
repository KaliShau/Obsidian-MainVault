
___
Установка:
```Zsh
apt install nginx
```

Базовый конфиг:
```Nginx
Открываем /etc/nginx/sites-available
Создаем файл с именем из своего домена и расширением .conf

Базовая конфигурация:
server {
	server_name chainx.tw1.su; # Свой домен
	
	location / {
		include proxy_params;
		proxy_pass http://localhost:3000;
	}
	listen 80;
}

Ссылка в sites_enabled: sudo ln -s /etc/nginx/sites-available/chainx.tw1.su.conf /etc/nginx/sites-enabled

Тест конфига: nginx -t
Перезапуск: nginx -s reload

Конфиг с api:
server {
        server_name chainx.tw1.su; # Свой домен
		
        location / {
                include proxy_params;
                proxy_pass http://localhost:3000;
        }
		
        location /api/ {
                proxy_pass http://localhost:4000/api/;
        }
        listen 80;
}

```

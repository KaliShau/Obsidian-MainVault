
___
## 🔹 **Способ 1: Автоматически (Let's Encrypt + Certbot) — самый простой способ**

### **1. Установите Certbot**
```bash
# Для Ubuntu/Debian
sudo apt update
sudo apt install certbot python3-certbot-nginx

# Для CentOS/RHEL
sudo dnf install certbot python3-certbot-nginx
```
### **2. Получите сертификат и автоматически настроите Nginx**

```bash
sudo certbot --nginx -d chainx.tw1.su -d www.chainx.tw1.su
```
Certbot автоматически:
- Сгенерирует SSL-сертификаты
- Настроит Nginx (`/etc/nginx/sites-available/your_config`)
- Добавит автоматическое обновление (чтобы сертификаты не истекли)

### **3. Проверьте, что Nginx перезагрузился**
```bash
sudo systemctl restart nginx
sudo systemctl status nginx
```
### **4. Проверьте HTTPS в браузере**

Откройте:  
🔗 **`https://chainx.tw1.su`**  
Должна быть зелёная замок (без ошибок).
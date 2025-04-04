
___
**PM2** — это продвинутый **менеджер процессов** для Node.js-приложений, который помогает управлять их работой в фоновом режиме, обеспечивает автоматический перезапуск при сбоях, балансировку нагрузки и мониторинг.  

### 🔹 **Основные возможности PM2**  
✔ **Запуск и управление процессами** (старт, остановка, перезагрузка)  
✔ **Кластер-режим** – запуск нескольких инстансов приложения для распределения нагрузки  
✔ **Автоперезапуск** при падении приложения  
✔ **Логирование** – сбор и просмотр логов (`pm2 logs`)  
✔ **Мониторинг** ресурсов (CPU, RAM) через `pm2 monit`  
✔ **Автозагрузка** при старте системы (`pm2 startup`)  
✔ **Удобная конфигурация** через `ecosystem.config.js`  

---

### 🔹 **Основные команды PM2**  

| Команда | Описание |  
|---------|----------|  
| `pm2 start app.js` | Запустить приложение |  
| `pm2 stop app.js` | Остановить приложение |  
| `pm2 restart app.js` | Перезапустить приложение |  
| `pm2 delete app.js` | Удалить из списка PM2 |  
| `pm2 list` | Список всех процессов |  
| `pm2 logs` | Показать логи |  
| `pm2 monit` | Мониторинг (CPU/RAM) |  
| `pm2 save` | Сохранить текущие процессы |  
| `pm2 startup` | Настроить автозапуск при загрузке ОС |  

---

### 🔹 **Пример использования**  
1. **Запуск приложения**  
   ```bash
   pm2 start server.js --name "my-api"
   ```
2. **Запуск в кластер-режиме (используя все ядра CPU)**  
   ```bash
   pm2 start server.js -i max --name "my-api-cluster"
   ```
3. **Настройка автозагрузки (для Linux)**  
   ```bash
   pm2 startup
   pm2 save
   ```

PM2 особенно полезен в **production-среде**, так как обеспечивает отказоустойчивость и удобное управление Node.js-приложениями. 🚀
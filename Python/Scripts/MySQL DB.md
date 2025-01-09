
___
##### Для подключения к бд MySQL нужен:
```
import mysql.connector
```
##### Код для создания коннекта к БД:
```
def connect(self):
	try:
		logging.info('Попытка подключения к базе данных...')
		
		config_data = config().load_config()
		
		self.conn = mysql.connector.connect(
			host = config_data['database']['host'],
			port = config_data['database']['port'],
			user = config_data['database']['user'] ,
			password = config_data['database']['password'],
			database = config_data['database']['dbname'],
			charset="utf8mb4",
			collation="utf8mb4_unicode_ci"
		)
		
		logging.info('Успешное подключение к базе данных.')
		logging.info('Проверка таблиц.')
		
		cursor = self.conn.cursor()
		
		cursor.execute(sql.table_roles)
		cursor.execute(sql.table_statuses)
		cursor.execute(sql.table_priorities)
		cursor.execute(sql.table_departments)
		cursor.execute(sql.table_users)
		cursor.execute(sql.table_tickets)
		cursor.execute(sql.table_comments)
		cursor.execute(sql.table_user_departments)
		cursor.execute(sql.table_reports)
		  
		self.conn.commit()
		
		logging.info('Таблицы исправны.')
		
		return True
		
	except mysql.connector.Error as err:
		logging.error(f'Ошибка подключения к базе данных: {err}')
		
		self.conn = None
		
		return False
```
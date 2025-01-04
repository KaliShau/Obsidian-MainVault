
___
#### Load config:
```
def load_config(self):
	with open('config.json', 'r') as file:
		config = json.load(file)
	return config
```
Данный скрипт предназначен для получения данных из json файла

#### Save config:
```
def save_config(self, password, user, host, port, db):
config = self.load_config()

config['database']['password'] = password
config['database']['user'] = user
config['database']['host'] = host
config['database']['port'] = port
config['database']['dbname'] = db

with open('config.json', 'w') as file:
json.dump(config, file, indent=5)
```
Данный скрипт предназначен для сохраненя данных в файл json

#### Create config:
```
def create_config(self):
if not os.path.exists('config.json'):

	config = {
	'database': {
	'host': 'localhost',
	'user': 'default_user',
	'password': 'default_password',
	'port': '3306',
	'dbname': 'default_db'
		}
	}

	with open('config.json', 'w') as file:
		json.dump(config, file, indent=5)
```
Данный скрипт предназначен для создания конфига если он еще не создан
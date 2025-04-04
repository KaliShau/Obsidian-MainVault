
___
#### **1. Таблица `users` (Пользователи)**

Эта таблица будет хранить данные всех пользователей системы (администраторы, классные руководители, студенты).

| Поле         | Тип данных   | Описание                                    |
| ------------ | ------------ | ------------------------------------------- |
| `id`         | SERIAL       | Уникальный идентификатор пользователя       |
| `username`   | VARCHAR(50)  | Логин пользователя                          |
| `password`   | VARCHAR(255) | Хэш пароля пользователя                     |
| `role`       | VARCHAR(20)  | Роль пользователя (admin, teacher, student) |
| `full_name`  | VARCHAR(100) | Полное имя пользователя                     |
| `created_at` | TIMESTAMP    | Дата и время создания записи                |

#### **2. Таблица `groups` (Группы)**

Эта таблица будет хранить информацию о группах студентов.

|Поле|Тип данных|Описание|
|---|---|---|
|`id`|SERIAL|Уникальный идентификатор группы|
|`name`|VARCHAR(50)|Название группы|
|`teacher_id`|INT|Идентификатор классного руководителя (внешний ключ на `users.id`)|

#### **3. Таблица `students` (Студенты)**

Эта таблица будет хранить информацию о студентах.

|Поле|Тип данных|Описание|
|---|---|---|
|`id`|SERIAL|Уникальный идентификатор студента|
|`user_id`|INT|Идентификатор пользователя (внешний ключ на `users.id`)|
|`group_id`|INT|Идентификатор группы (внешний ключ на `groups.id`)|
|`birth_date`|DATE|Дата рождения студента|
|`address`|VARCHAR(255)|Адрес студента|
|`phone`|VARCHAR(20)|Телефон студента|
	
#### **4. Таблица `grades` (Оценки)**

Эта таблица будет хранить информацию об оценках студентов.

|Поле|Тип данных|Описание|
|---|---|---|
|`id`|SERIAL|Уникальный идентификатор оценки|
|`student_id`|INT|Идентификатор студента (внешний ключ на `students.id`)|
|`subject`|VARCHAR(100)|Название предмета|
|`grade`|INT|Оценка (от 2 до 5)|
|`date`|DATE|Дата выставления оценки|
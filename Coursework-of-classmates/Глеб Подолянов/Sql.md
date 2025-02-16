
___
```
-- Таблица Roles (Роли)
CREATE TABLE Roles (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    name VARCHAR(50) NOT NULL UNIQUE,
    description TEXT
);

-- Таблица Users (Пользователи)
CREATE TABLE Users (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    login VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    
    fio VARCHAR(50),
    email VARCHAR(100) UNIQUE,
    phone_number VARCHAR(20),
    role_id INT NOT NULL,
    FOREIGN KEY (role_id) REFERENCES Roles(ID)
);

-- Таблица Statements (Заявления)
CREATE TABLE Statements (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FIO TEXT NOT NULL,
    address TEXT NOT NULL,
    type_work TEXT NOT NULL
);

-- Добавление ролей
INSERT INTO Roles (name, description) VALUES
('Admin', 'Администратор системы'),
('Operator', 'Сотрудник'),
('Client', 'Клиент');
```

___
```
-- Таблица Users (Пользователи)
CREATE TABLE Users (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    login VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100) UNIQUE,
    phone_number VARCHAR(20),
    role_id INT NOT NULL,
    CONSTRAINT fk_role
        FOREIGN KEY (role_id)
        REFERENCES Roles(ID)
);

-- Таблица Roles (Роли)
CREATE TABLE Roles (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    name VARCHAR(50) NOT NULL UNIQUE,
    description TEXT
);

-- Таблица TypesWorks (Типы работ)
CREATE TABLE TypesWorks (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    type VARCHAR(50) NOT NULL UNIQUE,
    description TEXT
);

-- Таблица Statements (Заявления)
CREATE TABLE Statements (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FIO TEXT NOT NULL,
    address TEXT NOT NULL,
    type_work_id INT NOT NULL,
    CONSTRAINT fk_type_work
        FOREIGN KEY (type_work_id)
        REFERENCES TypesWorks(ID)
);

-- Добавление ролей
INSERT INTO Roles (name, description) VALUES
('Admin', 'Администратор системы'),
('Operator', 'Сотрудник');

-- Добавление типов работ
INSERT INTO TypesWorks (type, description) VALUES
('Ремонт', 'Ремонтные работы'),
('Установка', 'Установка оборудования'),
('Обслуживание', 'Техническое обслуживание');
```
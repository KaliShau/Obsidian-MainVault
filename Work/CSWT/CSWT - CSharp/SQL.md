
___
```SQL
-- Создание таблицы Roles (Роли)
CREATE TABLE Roles (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    role_name VARCHAR(50) NOT NULL UNIQUE,
    description TEXT
);

-- Создание таблицы Users (Пользователи)
CREATE TABLE Users (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100) UNIQUE,
    phone_number VARCHAR(20),
    role_id INT NOT NULL,
    FOREIGN KEY (role_id) REFERENCES Roles(ID)
);

-- Создание таблицы Statuses (Статусы заявок)
CREATE TABLE Statuses (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status_name VARCHAR(50) NOT NULL UNIQUE,
    description TEXT
);

-- Создание таблицы Priorities (Приоритеты заявок)
CREATE TABLE Priorities (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    priority_name VARCHAR(50) NOT NULL UNIQUE,
    description TEXT
);

-- Создание таблицы Departments (Отделы)
CREATE TABLE Departments (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    department_name VARCHAR(100) NOT NULL UNIQUE,
    description TEXT
);

-- Создание таблицы User_Departments (Связь пользователей с отделами)
CREATE TABLE User_Departments (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    user_id INT NOT NULL,
    department_id INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES Users(ID),
    FOREIGN KEY (department_id) REFERENCES Departments(ID),
    UNIQUE (user_id, department_id)
);

-- Создание таблицы Tickets (Заявки)
CREATE TABLE Tickets (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    title TEXT NOT NULL,
    description TEXT NOT NULL,
    solution TEXT,
    closed_at TIMESTAMP,
    client_id INT NOT NULL,
    priority_id INT NOT NULL,
    status_id INT NOT NULL,
    assigned_to INT,
    FOREIGN KEY (client_id) REFERENCES Users(ID),
    FOREIGN KEY (priority_id) REFERENCES Priorities(ID),
    FOREIGN KEY (status_id) REFERENCES Statuses(ID),
    FOREIGN KEY (assigned_to) REFERENCES Users(ID)
);

-- Создание таблицы Comments (Комментарии к заявкам)
CREATE TABLE Comments (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    comment_text TEXT NOT NULL,
    ticket_id INT NOT NULL,
    user_id INT NOT NULL,
    FOREIGN KEY (ticket_id) REFERENCES Tickets(ID),
    FOREIGN KEY (user_id) REFERENCES Users(ID)
);

-- Создание таблицы Reports (Отчеты)
CREATE TABLE Reports (
    ID SERIAL PRIMARY KEY,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    report_name VARCHAR(255) NOT NULL,
    report_type VARCHAR(50) NOT NULL,
    report_data JSONB,
    user_id INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES Users(ID)
);

-- Создание триггера для автоматического обновления updated_at
CREATE OR REPLACE FUNCTION update_updated_at()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Применение триггера ко всем таблицам
DO $$
DECLARE
    t text;
BEGIN
    FOR t IN 
        SELECT table_name FROM information_schema.tables 
        WHERE table_schema = 'public' AND table_type = 'BASE TABLE'
    LOOP
        EXECUTE format('CREATE TRIGGER update_%s_updated_at
                        BEFORE UPDATE ON %I
                        FOR EACH ROW EXECUTE FUNCTION update_updated_at()', 
                        t, t);
    END LOOP;
END;
$$ LANGUAGE plpgsql;
```
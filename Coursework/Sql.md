
___
##### Tables:
```SQL
-- Таблица Statuses
CREATE TABLE Statuses (
    status_id SERIAL PRIMARY KEY,
    status_name VARCHAR(255) NOT NULL UNIQUE
);

-- Таблица Users
CREATE TABLE Users (
    user_id SERIAL PRIMARY KEY,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    username VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    full_name VARCHAR(255) NOT NULL,
    role VARCHAR(50) NOT NULL CHECK (role IN ('Admin', 'ASU_staff', 'Client'))
);

-- Таблица Requests
CREATE TABLE Requests (
    request_id SERIAL PRIMARY KEY,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    client_id INT NOT NULL,
    content TEXT NOT NULL,
    status_id INT NOT NULL,
    assigned_to INT,
    closed_at TIMESTAMP,
    FOREIGN KEY (client_id) REFERENCES Users(user_id) ON DELETE CASCADE,
    FOREIGN KEY (status_id) REFERENCES Statuses(status_id) ON DELETE RESTRICT,
    FOREIGN KEY (assigned_to) REFERENCES Users(user_id) ON DELETE SET NULL
);

-- Таблица Reports
CREATE TABLE Reports (
    report_id SERIAL PRIMARY KEY,
    user_id INT NOT NULL,
    report_title VARCHAR(255) NOT NULL,
    report_text TEXT NOT NULL,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(user_id) ON DELETE CASCADE
);
```
##### Statuses:
```
INSERT INTO Statuses (status_name) VALUES 
	('Новая'),
	('Принята'),
	('Закрыта');
```
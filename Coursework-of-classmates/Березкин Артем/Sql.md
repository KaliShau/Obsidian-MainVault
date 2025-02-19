
___
##### Tables and insert requests:
```SQL
-- Создание таблицы Users
CREATE TABLE Users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    role VARCHAR(20) NOT NULL
);

-- Создание таблицы Suppliers
CREATE TABLE Suppliers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    contact_person VARCHAR(100),
    phone VARCHAR(20),
    email VARCHAR(100)
);

-- Создание таблицы Materials
CREATE TABLE Materials (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    quantity INT NOT NULL,
    unit VARCHAR(20) NOT NULL,
    supplier_id INT REFERENCES Suppliers(id)
);

-- Создание таблицы Requests
CREATE TABLE Requests (
    id SERIAL PRIMARY KEY,
    material_id INT REFERENCES Materials(id),
    quantity INT NOT NULL,
    status VARCHAR(20) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
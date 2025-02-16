
___
```
CREATE TABLE Users (
    user_id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    role VARCHAR(20) NOT NULL CHECK (role IN ('admin', 'employee', 'client')),
    department_id INT REFERENCES Departments(department_id)
);

CREATE TABLE Departments (
    department_id SERIAL PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE Requests (
    request_id SERIAL PRIMARY KEY,
    client_id INT REFERENCES Users(user_id),
    description TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status_id INT REFERENCES RequestStatuses(status_id),
    assigned_to INT REFERENCES Users(user_id)
);

CREATE TABLE RequestStatuses (
    status_id SERIAL PRIMARY KEY,
    status_name VARCHAR(50) NOT NULL UNIQUE
);

CREATE TABLE RequestComments (
    comment_id SERIAL PRIMARY KEY,
    request_id INT REFERENCES Requests(request_id),
    user_id INT REFERENCES Users(user_id),
    comment_text TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
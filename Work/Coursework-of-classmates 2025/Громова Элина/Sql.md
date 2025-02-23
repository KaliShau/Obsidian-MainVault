
___
##### Tables and insert requests:
```SQL
-- Таблица users
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role VARCHAR(20) NOT NULL CHECK (role IN ('Admin', 'Teacher', 'Student')),
    full_name VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Таблица groups
CREATE TABLE groups (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    teacher_id INT REFERENCES users(id) ON DELETE SET NULL
);

-- Таблица students
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    user_id INT UNIQUE REFERENCES users(id) ON DELETE CASCADE,
    group_id INT REFERENCES groups(id) ON DELETE SET NULL,
    birth_date DATE,
    address VARCHAR(255),
    phone VARCHAR(20)
);

-- Таблица grades
CREATE TABLE grades (
    id SERIAL PRIMARY KEY,
    student_id INT REFERENCES students(id) ON DELETE CASCADE,
    subject VARCHAR(100) NOT NULL,
    grade INT NOT NULL CHECK (grade >= 2 AND grade <= 5),
    date DATE DEFAULT CURRENT_DATE
);

INSERT INTO users (username, password, role, full_name) VALUES 
	('admin','admin','Admin','Admin');
```

___
##### Tables and insert requests:
```SQL
CREATE TABLE Users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role VARCHAR(20) NOT NULL
);

CREATE TABLE Students (
    id SERIAL PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    group_name VARCHAR(50) NOT NULL
);

CREATE TABLE Events (
    id SERIAL PRIMARY KEY,
    event_name VARCHAR(100) NOT NULL,
    event_date DATE NOT NULL
);

CREATE TABLE Participation (
    id SERIAL PRIMARY KEY,
    student_id INTEGER REFERENCES students(id) NOT NULL,
    event_id INTEGER REFERENCES events(id) NOT NULL,
    participation_type VARCHAR(50),
    points INTEGER
);

INSERT INTO Users (username, password, role) VALUES 
	('admin', 'admin', 'Admin');
```
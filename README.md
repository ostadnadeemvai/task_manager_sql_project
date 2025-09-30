*Database name Task Manager*

CREATE DATABASE task_manager;

*2 Tables are created*
 1.User Table
 2.Task Table

   users table

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

   tasks table

CREATE TABLE tasks (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    title VARCHAR(200) NOT NULL,
    description TEXT,
    status ENUM('pending', 'in_progress', 'completed') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);


*Relationships query are connected with two table*
*This is 1:N relationship between users and tasks*

   user input

INSERT INTO users (name, email) VALUES
('Nadeem Hossain', 'nadeem@gmail.com'),
('Saiful Islam','saiful@gmail.com'),
('Mamun', 'mamun@gmail.com');


   tasks input

INSERT INTO tasks (user_id, title, description, status) VALUES
(1, 'Design Homepage', 'Create wireframe for homepage', 'in_progress'),
(1, 'Write Blog Post', 'Draft blog post about new features', 'pending'),
(2, 'Fix Login Bug', 'Resolve issue with login form validation', 'completed'),
(2, 'Update Documentation', 'Add details to API docs', 'pending'),
(3, 'Database Backup', 'Schedule weekly backup', 'in_progress'),
(3, 'Team Meeting', 'Organize sprint planning meeting', 'completed');

Execute SQL queries are given below

#Select all tasks

SELECT * FROM tasks;

#Update a task’s status

UPDATE tasks
SET status = 'completed'
WHERE id = 2;

#Delete a task

DELETE FROM tasks
WHERE id = 5;

#Show tasks with Sorting and Limit/Pagination

sorting and Limit

SELECT * FROM tasks
ORDER BY created_at DESC
LIMIT 3;

Pagination

SELECT * FROM tasks
ORDER BY created_at DESC
LIMIT 3 OFFSET 3;

#Using Aggregator Functions

Counting how many tasks user have

SELECT u.name, COUNT(t.id) AS total_tasks
FROM users u
LEFT JOIN tasks t ON u.id = t.user_id
GROUP BY u.id, u.name;

Finding a maximum user tasks

SELECT u.name, COUNT(t.id) AS total_tasks
FROM users u
JOIN tasks t ON u.id = t.user_id
GROUP BY u.id, u.name
ORDER BY total_tasks DESC
LIMIT 1;

#Perform Inner Join, Left Join, and Right Join between users and tasks

Inner Join

SELECT u.name, t.title, t.status
FROM users u
INNER JOIN tasks t ON u.id = t.user_id;

Left join

SELECT u.name, t.title, t.status
FROM users u
LEFT JOIN tasks t ON u.id = t.user_id;

Right join

SELECT u.name, t.title, t.status
FROM users u
RIGHT JOIN tasks t ON u.id = t.user_id;

Thats the way i done my project work and showing its code also

Thank You!!

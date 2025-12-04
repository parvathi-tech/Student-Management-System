Student Management System – MySQL Project

1. Project Overview

The Student Management System (SMS) is a basic SQL-based project designed to store and manage student details, course information, and student enrollments.
The system uses relational database concepts, primary keys, and foreign keys to ensure data integrity.

2. Objectives

Store student information

Store course details

Manage enrollments between students and courses

Maintain relationships using primary & foreign keys

Retrieve student-course reports using SQL queries

3. System Requirements

Database: MySQL

Version: MySQL 5.7+ / 8+

Tools: MySQL Workbench / phpMyAdmin / CLI

4. Database Design

The system contains three core entities:

1️⃣ students – stores student personal information
2️⃣ courses – stores course details
3️⃣ enrollments – bridge table linking students ↔ courses

5. ER Diagram (English Description)

One student can enroll in multiple courses

One course can be taken by multiple students

Relationship: Many-to-Many, resolved using enrollments table

STUDENTS (1) ----< ENROLLMENTS >---- (1) COURSES


6. Table Structures (DDL)

CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    age INT,
    gender VARCHAR(10),
    email VARCHAR(100),
    phone VARCHAR(15)
);
6.2 courses Table

CREATE TABLE courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100),
    fee DECIMAL(10,2)
);


6.3 enrollments Table

CREATE TABLE enrollments (
    enrollment_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);

7. Sample Data (DML)

Students

INSERT INTO students (first_name, last_name, age, gender, email, phone) VALUES
('Lakshmi', 'Parvathi', 23, 'Female', 'lakshmi@gmail.com', '9876543001'),
('Rahul', 'Kumar', 21, 'Male', 'rahul@gmail.com', '9876543222');

COURSES

INSERT INTO courses (course_name, fee) VALUES
('Java Full Stack', 15000),
('Python Programming', 12000),
('Data Science', 25000);


Enrollments

INSERT INTO enrollments (student_id, course_id, enrollment_date) VALUES
(1, 1, '2025-01-01'),
(1, 3, '2025-01-05'),
(2, 2, '2025-01-07');

8. CRUD Operations

8.1 Create Data
INSERT INTO students (...) VALUES (...);
INSERT INTO courses (...) VALUES (...);
INSERT INTO enrollments (...) VALUES (...);

8.2 Read Data
Get all students

SELECT * FROM students;

Get all courses 
SELECT * FROM courses;

Student + Course Enrollment Report
SELECT s.first_name, s.last_name, c.course_name, e.enrollment_date
FROM enrollments e
JOIN students s ON e.student_id = s.student_id
JOIN courses c ON e.course_id = c.course_id;


8.3 Update Data
UPDATE students SET email = 'newmail@gmail.com' WHERE student_id = 1;

8.4 Delete Data
DELETE FROM students WHERE student_id = 2;

9. Important SQL Queries (Reports)
Count students in each course

SELECT c.course_name, COUNT(e.student_id) AS total_students
FROM enrollments e
JOIN courses c ON e.course_id = c.course_id
GROUP BY c.course_name;

Get students enrolled in a particular course

SELECT s.first_name, s.last_name
FROM enrollments e
JOIN students s ON e.student_id = s.student_id
WHERE e.course_id = 1;


10. Conclusion

This SQL project demonstrates core database functionalities including:

Table creation (DDL)

Data insertion and modification (DML)

Foreign key relationships

Many-to-many implementation using a bridge table

Reporting using JOINs and aggregation


# Student Management API

The Student Management API is a web-based system designed to manage student and course data through RESTful API endpoints. Built with PHP and MySQL, the API facilitates seamless CRUD (Create, Read, Update, Delete) operations for students and courses. It ensures secure and efficient handling of data while maintaining proper relationships between students and their enrolled courses.

## Purpose

The purpose of this API is to provide a robust backend system for managing student records and course details in educational institutions. It simplifies the management process for administrators by offering structured, reliable, and error-handling mechanisms.

## Key Features

1. Comprehensive CRUD Operations:
* Add, view, update, and delete students and courses.

2. Error Handling:
* Validates input fields for missing data, duplicate entries, invalid formats (e.g., emails, dates), and non-existent records.

3. Data Relationships:
* Establishes a proper relationship between students and courses using course IDs.

4. Search and Filter Functionalities:
* Search for students by name, email, or filter by course ID.

5. Input Validation:
* Ensures accurate data entry with checks for valid email formats and date compliance (YYYY-MM-DD).

6. Secure Communication:
* Implements API key-based authentication for secure access (optional enhancement).

7. Error Messages and HTTP Status Codes:
* Returns meaningful error messages for better user understanding with corresponding HTTP codes (e.g., 400 for bad requests, 409 for conflicts).

8. Compatibility with Postman:
* Fully testable using Postman for all CRUD operations and error scenarios.

## Setup Instructions

# API Endpoints
Below is the list of API endpoints, including HTTP methods, endpoint URLs, request bodies, and sample responses.

* Create a New Student
HTTP Method: POST
Endpoint URL: http://localhost/student-management-api/index.php?request=students
Request body: 
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john.doe@example.com",
  "birthdate": "2000-05-15",
  "course_id": 2
}
Sample response:
Success (201): "message": "Student created successfully"
Error (400 - Invalid email): "message": "Invalid email format"
Error (409 - Duplicate email): "message": "Duplicate email"

* Retrieve All Students
HTTP Method: GET
Endpoint URL: http://localhost/student-management-api/index.php?request=students
Sample response:
Success (200): {
    "student_id": 1,
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@example.com",
    "birthdate": "2000-05-15",
    "course_id": 2
  }
No Match (200): "message": "No students found"

* Retrieve Specific Students
HTTP Method: GET
Endpoint URL: http://localhost/student-management-api/index.php?request=students/49
Sample response:
Success (200): {
    "student_id": "49",
    "first_name": "Emma",
    "last_name": "Wilson",
    "email": "emma.wilson@example.com",
    "birthdate": "1999-12-01",
    "course_id": "1"
}
Error (404): "message": "Student not found"

* Retrieve Students With Filter by Name, Course ID, and Email.
HTTP Method: Get
Endpoint URLs:
Filter by name: http://localhost/student-management-api/index.php?request=students&search=riley
Filter by name and course id: http://localhost/student-management-api/index.php?request=students&search=riley&course_id=2
Filter by email address: http://localhost/student-management-api/index.php?request=students&search=riley.clark@example.com 
Request body: {
        "student_id": "62",
        "first_name": "Riley",
        "last_name": "Clark",
        "email": "riley.clark@example.com",
        "birthdate": "1999-05-25",
        "course_id": "2"
    }

* Update Student Information
HTTP Method: PUT or PATCH
Endpoint URL: http://localhost/student-management-api/index.php?request=students/62
Request Body (Partial or Full):
{
    "student_id": "62",
    "first_name": "Riley",
    "last_name": "Clark",
    "email": "riley.clark@example.com",
    "birthdate": "1999-05-25",
    "course_id": "2"
}
Sample responses:
Success (200): "message": "Student updated successfully"
Error (400 - Invalid email): "message": "Invalid email format"
Error (400): "message": "Invalid birthdate format. Use YYYY-MM-DD"
Error (409 - Duplicate email): "message": "Duplicate email"




# SQL Queries & Dummy Data

CREATE TABLE courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(255) NOT NULL,
    description TEXT
);

CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(255) NOT NULL,
    last_name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    birthdate DATE NOT NULL,
    course_id INT,
    FOREIGN KEY (course_id) REFERENCES courses(course_id)
);

INSERT INTO courses (course_name, description) VALUES
('Computer Science', 'Study of computation and information processing.'),
('Information Technology', 'Focus on using technology to solve problems.'),
('Engineering', 'Design and build complex systems.');

INSERT INTO students (first_name, last_name, email, birthdate, course_id) VALUES
('John', 'Doe', 'john.doe@example.com', '2000-01-01', 1),
('Jane', 'Smith', 'jane.smith@example.com', '1999-02-15', 2),
('Alice', 'Johnson', 'alice.johnson@example.com', '1998-03-30', 3),
('Bob', 'Brown', 'bob.brown@example.com', '1997-07-10', 1),
('Charlie', 'Davis', 'charlie.davis@example.com', '1996-05-22', 2),
('David', 'Miller', 'david.miller@example.com', '1998-09-13', 3),
('Emma', 'Wilson', 'emma.wilson@example.com', '1999-12-01', 1),
('Fiona', 'Moore', 'fiona.moore@example.com', '2000-06-25', 2),
('George', 'Taylor', 'george.taylor@example.com', '2001-11-30', 3),
('Hannah', 'Anderson', 'hannah.anderson@example.com', '1997-08-17', 1),
('Isaac', 'Thomas', 'isaac.thomas@example.com', '1998-01-05', 2),
('Jack', 'Jackson', 'jack.jackson@example.com', '1996-03-11', 3),
('Karen', 'White', 'karen.white@example.com', '1999-10-29', 1),
('Liam', 'Harris', 'liam.harris@example.com', '2000-04-20', 2),
('Mia', 'Martin', 'mia.martin@example.com', '1997-02-08', 3),
('Noah', 'Thompson', 'noah.thompson@example.com', '2001-12-18', 1),
('Olivia', 'Garcia', 'olivia.garcia@example.com', '1998-07-22', 2),
('Parker', 'Martinez', 'parker.martinez@example.com', '1996-10-14', 3),
('Quinn', 'Roberts', 'quinn.roberts@example.com', '2000-08-09', 1),
('Riley', 'Clark', 'riley.clark@example.com', '1999-05-25', 2);

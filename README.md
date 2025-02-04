CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    DOB DATE,
    Gender VARCHAR(10),
    Email VARCHAR(100)
);

CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(100),
    Credits INT
);

CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY,
    StudentID INT,
    CourseID INT,
    EnrollmentDate DATE,
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);

CREATE TABLE Grades (
    GradeID INT PRIMARY KEY,
    EnrollmentID INT,
    Grade CHAR(2),
    FOREIGN KEY (EnrollmentID) REFERENCES Enrollments(EnrollmentID)
);


-- Inserting Students
INSERT INTO Students (StudentID, FirstName, LastName, DOB, Gender, Email) 
VALUES (1, 'John', 'Doe', '2000-05-15', 'Male', 'john.doe@example.com'),
       (2, 'Jane', 'Smith', '1999-07-22', 'Female', 'jane.smith@example.com');

-- Inserting Courses
INSERT INTO Courses (CourseID, CourseName, Credits) 
VALUES (101, 'Mathematics', 3), 
       (102, 'Physics', 4);

-- Enroll Students in Courses
INSERT INTO Enrollments (EnrollmentID, StudentID, CourseID, EnrollmentDate)
VALUES (1, 1, 101, '2025-01-01'),
       (2, 1, 102, '2025-01-01'),
       (3, 2, 101, '2025-01-01');

-- Assigning Grades
INSERT INTO Grades (GradeID, EnrollmentID, Grade)
VALUES (1, 1, 'A'), 
       (2, 2, 'B'),
       (3, 3, 'A');

SELECT 
    s.StudentID, 
    s.FirstName, 
    s.LastName, 
    c.CourseName, 
    g.Grade
FROM 
    Students s
JOIN 
    Enrollments e ON s.StudentID = e.StudentID
JOIN 
    Courses c ON e.CourseID = c.CourseID
JOIN 
    Grades g ON e.EnrollmentID = g.EnrollmentID
ORDER BY 
    s.StudentID;

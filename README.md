# StudyMate

A robust and efficient Spring Boot REST API designed to modernize and streamline student attendance management for educational institutions. StudyMate facilitates seamless recording, tracking, and management of attendance records, reducing administrative overhead and improving data accuracy.

## 📖 About The Project

StudyMate empowers faculty members to effortlessly record attendance for their subjects. The system provides intuitive interfaces for viewing and managing these records, replacing traditional paper-based methods with a secure, automated, and integrated digital solution.

The core entities managed by the system are:
- **Students**
- **Subjects**
- **Faculty**
- **Attendance Records**
- **Users** (for authentication)

### 🎯 Objectives
- **Automate Attendance Tracking:** Provide a RESTful API for easy integration with existing educational platforms and front-end applications.
- **Ensure Data Accuracy:** Implement automated validation and consistent storage mechanisms for all attendance records.
- **Enhance Workflows:** Simplify and improve the daily workflows for both faculty and administrative staff.

## 🛠️ Built With

*   **Backend Framework:** [Spring Boot 2.5.6](https://spring.io/projects/spring-boot)
*   **Java Version:** JDK 1.8
*   **Database:** [MySQL 8](https://www.mysql.com/)
*   **ORM Framework:** [Hibernate 5.6](https://hibernate.org/) (JPA Implementation)
*   **Build Tool:** [Maven](https://maven.apache.org/)
*   **API Testing:** [Postman](https://www.postman.com/)

## 🏗️ Project Architecture

StudyMate follows a standard layered architecture to ensure separation of concerns, scalability, and maintainability.

1.  **Controller Layer:** Handles incoming HTTP requests, performs basic validation, and returns appropriate responses.
2.  **Service Layer:** Contains the core business logic, orchestrates operations, and manages transactions.
3.  **DAO (Data Access Object) Layer:** Abstracts all database interactions using JPA and Hibernate, performing CRUD operations.

## 📦 Modules & API Endpoints

### 1. Student Module
Manages all CRUD operations for student records.
- `GET /student/get-all-students` - Fetch all students
- `POST /student/add-student` - Create a new student
- `GET /student/get-student-by-id/{id}` - Get a student by ID
- `PUT /student/update-student` - Update a student's details
- `DELETE /student/delete-student/{id}` - Delete a student

### 2. Subject Module
Manages all CRUD operations for subject records.
- `GET /subject/get-all-subjects` - Fetch all subjects
- `POST /subject/add-subject` - Create a new subject
- `GET /subject/get-subject-by-id/{id}` - Get a subject by ID
- `PUT /subject/update-subject` - Update a subject's details
- `DELETE /subject/delete-subject/{id}` - Delete a subject

### 3. Faculty Module
Manages all CRUD operations for faculty member records.
- `GET /faculty/get-all-faculties` - Fetch all faculty
- `POST /faculty/add-faculty` - Create a new faculty member
- `GET /faculty/get-faculty-by-id/{id}` - Get a faculty member by ID
- `PUT /faculty/update-faculty` - Update a faculty member's details
- `DELETE /faculty/delete-faculty/{id}` - Delete a faculty member

### 4. Attendance Module
Handles the creation and retrieval of attendance records.
- `GET /attendance/get-all-attendance-records` - Retrieve all attendance records
- `POST /attendance/add-attendance` - Create a new attendance record. Requires:
  - `subjectId`
  - List of `studentIds` (for students who were present)
  - `date`
  - (The system automatically captures the `facultyId` of the attendance taker)

### 5. User Module
Handles user authentication and management.
- `POST /user/login-user` - Authenticate a user (username & password)
- `POST /user/register-user` - Register a new user
- `GET /user/get-user-by-username/{username}` - Get user details by username
- `GET /user/get-all-user` - Get a list of all registered users
- `DELETE /user/delete-user/{username}` - Delete a user by username

## 🗃️ Database Schema

The application uses a MySQL relational database. Key tables include:
- `student` (`id`, `name`, `email`)
- `subject` (`id`, `name`)
- `faculty` (`id`, `name`, `email`)
- `attendance_record` (`id`, `date_time`, `subject_id`, `faculty_id`)
- `attendance_students` (Join table for Many-to-Many relationship between `attendance_record` and `student`)
- `user` (`username`, `password`, `email`, `first_name`, `last_name`, `role`)

> An Entity-Relationship (ER) diagram is available for download within the project documentation.

## 🚀 Getting Started

### Prerequisites
*   Java JDK 1.8
*   Maven 3.6+
*   MySQL Server 8.0
*   (Optional) An IDE like Eclipse or IntelliJ IDEA

### Installation & Setup
1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/StudyMate.git
    cd StudyMate
    ```

2.  **Configure Database:**
    *   Create a MySQL database named `studymate_db` (or your preferred name).
    *   Update the `application.properties` file (`src/main/resources/`) with your database URL, username, and password:
    ```properties
    spring.datasource.url=jdbc:mysql://localhost:3306/studymate_db
    spring.datasource.username=your_mysql_username
    spring.datasource.password=your_mysql_password
    # Hibernate settings
    spring.jpa.hibernate.ddl-auto=update
    spring.jpa.show-sql=true
    ```

3.  **Build and Run the Application:**
    *   Using Maven:
    ```bash
    mvn clean install
    mvn spring-boot:run
    ```
    *   The application will start on `http://localhost:8080`.

4.  **Test the APIs:**
    *   Import the provided Postman collection (if available) to test all endpoints.
    *   Alternatively, use `curl` or any other API client to interact with the endpoints.

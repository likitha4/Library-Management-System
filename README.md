# 📚 Library Management System

A Java Swing desktop application for managing library operations including book inventory, student records, book issuance, and return tracking — backed by a MySQL relational database.

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | Java (JDK 8+) |
| UI Framework | Java Swing (AWT) |
| Database | MySQL |
| Connectivity | JDBC (`com.mysql.jdbc.Driver`) |
| Build Tool | Apache NetBeans (Ant-based) |
| Libraries | `rs2xml.jar` (ResultSet → JTable), `jcalendar-tz-1.3.3-4.jar` (Date Picker) |

---

## 🚀 Features

- **Authentication** — Secure login, signup, and forgot-password flows for library users
- **Book Management** — Add new books, search and view the full book catalogue
- **Student Management** — Register students and maintain detailed student profiles
- **Issue & Return** — Issue books to students with due-date tracking via a calendar date picker; process returns with automated record updates
- **Statistics Dashboard** — View real-time tables of currently issued books and return history
- **About Us** — Informational screen about the library system
- **Splash / Loading Screen** — Branded entry screen before login

---

## 📁 Project Structure

```
LibraryManagementSystem/
├── src/
│   └── librarymanagementsystem/
│       ├── LibraryManagementSystem.java  # Entry point / splash screen
│       ├── Login_user.java               # Login screen
│       ├── Signup.java                   # New user registration
│       ├── Forgot.java                   # Password recovery
│       ├── Home.java                     # Main dashboard (post-login)
│       ├── AddBook.java                  # Add book to inventory
│       ├── BookDetails.java              # View/search book catalogue
│       ├── AddStudent.java               # Register new student
│       ├── StudentDetails.java           # View/search student records
│       ├── IssueBook.java                # Issue a book to a student
│       ├── ReturnBook.java               # Process book returns
│       ├── Statistics.java               # Issue & return statistics
│       ├── aboutUs.java                  # About screen
│       ├── Loading.java                  # Loading/splash UI
│       ├── conn.java                     # MySQL JDBC connection singleton
│       ├── icons/                        # UI image assets
│       └── jar/                          # Third-party JAR dependencies
├── nbproject/                            # NetBeans project metadata
└── manifest.mf
```

---

## ⚙️ Setup & Configuration

### Prerequisites

- Java JDK 8 or higher
- MySQL Server (running locally)
- Apache NetBeans IDE (recommended) or any Java IDE

### Database Setup

1. Start your MySQL server.
2. Create a database named `library`:
   ```sql
   CREATE DATABASE library;
   ```
3. Create the required tables (example schema):
   ```sql
   USE library;

   CREATE TABLE users (
       username VARCHAR(50) PRIMARY KEY,
       password VARCHAR(50)
   );

   CREATE TABLE books (
       bookId VARCHAR(20) PRIMARY KEY,
       name VARCHAR(100),
       author VARCHAR(100),
       publisher VARCHAR(100),
       edition VARCHAR(20),
       price DECIMAL(8,2),
       quantity INT
   );

   CREATE TABLE student (
       rollNo VARCHAR(20) PRIMARY KEY,
       name VARCHAR(100),
       branch VARCHAR(50),
       semester VARCHAR(10),
       phoneNo VARCHAR(15)
   );

   CREATE TABLE issueBook (
       issueId INT AUTO_INCREMENT PRIMARY KEY,
       bookId VARCHAR(20),
       rollNo VARCHAR(20),
       issueDate DATE,
       returnDate DATE
   );
   ```

### Connection Configuration

The database connection is configured in `conn.java`:

```java
c = DriverManager.getConnection("jdbc:mysql://localhost/library", "root", "");
```

Update the **username** and **password** fields to match your MySQL credentials.

### Running the Application

1. Open the project in NetBeans (File → Open Project).
2. Add the JAR dependencies from `src/librarymanagementsystem/jar/` to the project classpath.
3. Also add the MySQL Connector/J JAR to the classpath.
4. Run `LibraryManagementSystem.java` (the main entry point).

---

## 🔗 Dependencies

| JAR | Purpose |
|-----|---------|
| `mysql-connector-java` | JDBC driver for MySQL connectivity |
| `rs2xml.jar` | Converts SQL `ResultSet` to `JTable` model |
| `jcalendar-tz-1.3.3-4.jar` | Date picker (`JDateChooser`) for issue/return dates |

---

## 📸 Application Flow

```
Splash Screen → Login / Signup
                    ↓
              Home Dashboard
         ┌────────┼────────────┐
     Books     Students     Reports
   Add/View   Add/View    Statistics
         └────────┼────────────┘
            Issue / Return Book
```

---

## 🧩 Key Design Decisions

- **`conn.java` as a shared connection class** — A lightweight JDBC wrapper instantiated per operation to keep database access straightforward across all modules.
- **`rs2xml.jar` integration** — Converts `ResultSet` objects directly into `TableModel`, enabling fast population of `JTable` components without manual row parsing.
- **`JDateChooser`** — Provides a user-friendly calendar widget for selecting issue and return dates, replacing manual text entry and reducing input errors.

---

## 📌 Notes

- This is a **desktop application** (not web-based). No server or browser is required.
- Default MySQL connection uses `root` with an empty password — update `conn.java` before deploying in any shared or production environment.
- The project was built and tested using **Apache NetBeans IDE**.

# create
# README.md — Library Management Database (SQL Project)
# Project Title
# Library Management System — Normalized SQL Database (up to 3NF)

# What I Built
I designed and implemented a relational database system for a Library Management System using MySQL.
The database stores and manages information about books, authors, members, and borrowing records efficiently.
This system allows librarians to:
Track books and their authors
Manage members
Record which member borrowed which book and when

# Why I Built It
Libraries handle large amounts of data — books, members, borrowing details — which must be:
Accurate (no duplication)
Easily searchable
Logically organized

By applying database normalization up to Third Normal Form (3NF), I eliminated data redundancy and ensured data consistency.
This project demonstrates my understanding of:
Database design principles
Entity Relationship Modeling (ERD)
Normalization (1NF → 3NF)
SQL schema creation and queries

# How I Built It
 Step 1 — Requirement Analysis
Identified key entities and relationships:
Authors
Books
Members
Borrow (transactions)

Step 2 — Database Design (ER Diagram)
Conceptual relationships:
Authors (1) ───< Books (1) ───< Borrow >───(1) Members

Each author can write many books,
each member can borrow many books,
and each borrowing record connects one book and one member.

 Step 3 — Normalization
 1NF: Removed repeating groups, ensured atomic data.
 2NF: Removed partial dependencies on composite keys.
 3NF: Removed transitive dependencies (non-key fields depend only on the primary key).

 Step 4 — Implementation in MySQL / Google Colab
Used MySQL to:
Create tables
Define relationships via foreign keys
Insert sample data
Run queries to verify the structure


Example Commands:
CREATE DATABASE LibraryDB;
USE LibraryDB;

CREATE TABLE Authors (
  Author_ID INT PRIMARY KEY AUTO_INCREMENT,
  Author_Name VARCHAR(100),
  Country VARCHAR(50)
);

CREATE TABLE Books (
  Book_ID INT PRIMARY KEY AUTO_INCREMENT,
  Title VARCHAR(100),
  Genre VARCHAR(50),
  Publish_Year INT,
  Author_ID INT,
  FOREIGN KEY (Author_ID) REFERENCES Authors(Author_ID)
);

- Running the Project in Google Colab
To run MySQL inside Google Colab:
!apt-get update -qq
!apt-get install -y mysql-server > /dev/null
!service mysql start
!mysql -e "ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root'; FLUSH PRIVILEGES;"
!mysql -uroot -proot -e "CREATE DATABASE LibraryDB; SHOW DATABASES;"

Then execute your SQL schema and queries.

 -  Example Query
SELECT m.Member_Name, b.Title, br.Borrow_Date, br.Return_Date
FROM Borrow br
JOIN Members m ON br.Member_ID = m.Member_ID
JOIN Books b ON br.Book_ID = b.Book_ID;


 -  Learning Outcomes
Understood database normalization (1NF–3NF)
Practiced foreign key relationships
Created ER diagrams and SQL scripts
Ran SQL queries inside Google Colab



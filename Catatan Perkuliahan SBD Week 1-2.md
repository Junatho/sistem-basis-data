## 📘 SISTEM BASIS DATA

### 🗓️ Week 1: Introduction to Database (DB)

#### 📍 Definition and Purpose of Database
Database Management Systems (DBMS) | Purpose of DBMS:
Before the advent of modern DBMS, many applications used file systems directly to manage data. This approach came with a plethora of challenges:
1. Data Redundancy
2. Inconsistency
3. Difficulty in Accessing Data
4. Need for New Programs
5. Data Isolation
6. Integrity Problems
7. Challenges with Constraints
8. Atomicity of Updates
9. Concurrent Access Issues
10. Security Problems

#### 📍 View of Data (VOD)
a major purpose of a database system is to provide users with an abstract view of the data.
- Data models: a conceptual framework that determines the structure, organization, and the flow of data in a system. It servees as a blueprint ofr designing databases.
- Data abstraction: hide the complexity of data structures to represent data in the database from user through several levels of data abstraction.

#### 📍 VOD - Data Models
- Data: the actual information that will be stored in the database. Ex: the names and addresses of customers in a business database
- D. relationships: describe how different pieces of data are connected to each other. Ex: in a university database, for instance, a student might be related to courses via enrollment records
- D. semantic: the meaning of the data. Ex: it isnt just about knowing that a database has a date field, but understanding that it represents a students' enrollment date.
- D. constraints: rules that determine the permissible value or combinations of values for certain data. Ex: a student's age cannot be negative, or that an email address must be unique across all records.

#### 📍 VOD - Data Models Types
- Relational: organizes data into tables (or relations in mathematical terms). Ex: MySQL
- Entity Relationship: mainly for database design. Represents entities and how they relate to one another. Visualized using ER diagrams. Ex: "Student" and "Course" might be entities, with a "takes" relationship representing that a student is enrolled in a course.

#### 📍 Object-based (VOD data model type)
- Object oriented: objects encapsulate both data and methods to manipulate the data. Ex: a "Car" object might have data (like color and model) and methods (like start() and stop()).
- Object-relational: combines the characteristics of both relational and object-oriented data models. It allows objects, classes, and inheritance to be directly supported in database schemas and query languages.
Semi-structured: data is hierarchical but not strictly structured. Ex: XML, JSON

#### 📍 VOD - Abstraction
- Physical level: describes how a record (e.g., instructor) is stored
- Logical level: describes data stored in database, and the relationships among the data
--> type instructor = record
          ID: string;
          name : string:=;
          dept_name = string;
          salary : integer;
               end;
- View level: application programs hide details of data types. Views can also hide information (such as an employee's salary) for security purposes

#### 📍 Data Definition Language (DDL)
1. Specification notion for defining the database schema
Example:     create table instructor {
                             ID                        char(5),
                             Name                 varchar (20),
                             dept_name      varchar(20),
                             salary                numeric (8,2) }
2. DDL compiler generates a set of table templates stored in a data dictionary
3.  Data dictionary contains metadata (i.e., data about data)
--> database schema
--> integrity constraints
--> authorization

#### 📍 Database Access from Application Program
SQL, being a non-procedural query language, is designed specifically for managing and querying data in relational databases.

SQL Limitations:
- cant take dynamic input from users
- doesnt dictate how the results display to end users
- doesnt handle networking tasks

Solutions:
Dynamic SQL or parameterized queries are used. Generated on the fly; can change based on user input


### 🗓️ Week 2: Introduction to Relational Model

#### 📍 Database Schema
- schema: the logical structure of the database
- instance: a snapshot of the data in the database at a given instant in time
- example:
--> schema: *instructor (ID, name, dept_name, salary)*
--> instance: (data table)

Keys are the concepts that form the backbone of relational database design, ensuring data integrity, reducing redundancy, and enabling data retrieval and manipulation, and those keys are:
- Superkey (SK)
- Candidate Key (CK)
- Primary Key (PK)
--> example: ID + gaboleh null values 
- Foreign Key (FK)

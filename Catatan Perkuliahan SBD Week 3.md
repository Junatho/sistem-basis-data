## 📘 SISTEM BASIS DATA

### 🗓️ Week 3: Intro to SQL (1)

#### 📍 About SQL
- SQL was originally developed by IBM under the name "Sequel" (1970)
- The name was later changed to "Structured Query Language" or "SQL"
- SQL-86: The 1st to be adopted as a standard by the ANSL
- SQL-89: A minor enhancement to SQL-86
- SQL-92 (or SQL2): Introduced many new features and became widely adopted as the new standard for many years
- SQL-1999 (or SQL3): Added support for advanced features like trigonometry and object-oriented capabilities. The name SQL-1999 replaced the previous name format
- SQL-2003: Introduced features like XML support and windowed analysis

Commercial Developments
- Many commercial database systems support most, if not all, of the features from SQL-92 and also incorporate features from the newer standards
- However each system might have its own variations and proprietary extensions that don't always conform to the standards. This can lead to differences in syntax and behavior across different database systems

Important note!
- Its always crucial to check the documentation for the specific database system you're using
- Not all SQL examples or features found in books or online tutorials will work the same way on every system

#### 📍 SQL Parts
1. Data Manipulation Language (DML)
2. Data Definition Language (DDL)
3. Transaction Control
4. Embedded SQL & Dynamic SQL
5. Authorization

#### 📍 Data Definition Language
The SQL DDL provides a set of commands and functionalities that allow database administrators and developers to define and manage the structure of a database:
1. Schema for Each Relation: This defines the blueprint or structure of a table (relation). It specifies the columns and their names
2. Type of Values Associated with Each Attribute: This defines the datatype for each column in the table
3. Integrity Constraints: These are rules that ensure data remains accurate and consistent
4. Set of Indices to Be Maintained for Each Relation:
--> Indices improve the speed of data retrieval operations on a database
--> They work like an index at the back of a book, providing a quick way to locate data while having to search every row
‎
#### 📍 Create Table Construct
- An SQL relation is defined using the **create table** command:
**create table r**
    (A1, D1, A2, D2, ..., An Dn
         (integrity-constraint1),
             ...,
         (integrity-constraintk)
    )

- R is the name of the relation
- each Ai is an attribute name in the schema of relation r
- Di is the data type of values in the domain of attribute Ai

create table instructor (
  ID char(5),
     name varchar(20) not null,
     dept_name varchar(20),
  salary numeric(8,2),
      
  primary key (ID),
  foreign key (dept_name) references department);

create table department (
  dept_name varchar(20),
  building varchar(15),
  budget numeric(12,2) check (budget > 0),
  primary key (dept_name));
    
create table student (
  ID varchar(5),
  name varchar(20) not null,
  dept_name varchar(20),
  tot_cred numeric(3,0),
  primary key (ID),
  foreign key (dept_name) references department
  
create table course (
     course_id varchar(8),
     title varchar(50),
  dept_name varchar(20),
  credits numeric(2,0),
     primary key (course_id),
     foreign key (dept_name) references department);
  
create table section (
  course_id varchar(8),
     sec_id varchar(8),
     semester varchar (6) check (semester in ('Fall', 'Winter', 'Spring', 'Summer'));
  year numeric(4,0) check (year > 1701 and year < 2100),
     building varchar(15),
     room_number varchar(7),
  time_slot_id varchar(4),
     primary key (course_id, sec_id, semester, year),
     foreign key (course_id) references course on delete cascade,
  foreign key (building, room_number) references classroom on delete set null);

create table takes (
     ID varchar(5),
     course_id varchar(8),
  sec_id varchar(8)
     semester varchar(6),
     year numeric(4,0),
  grade varchar(2),
     primary key (ID, course_id, sec_id, semester, year),
     foreign key (ID) references student,
  foreign key (course_id sec_id, semester, year) references section);

#### 📍 The Select Clause
- The select clause lists the attributes desired in the result of a query
--> corresponds to the projection (pi) operation of the relational algebra
- Ex: find the names of all instructors:
          select name
          from instructor
- NOTE: SQL names are case insensitive (i.e., u may use upper or lower case letters)
--> e.g., Name = NAME = name
--> some people use upper case whenever we use bold font

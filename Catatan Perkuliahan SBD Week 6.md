## 📘 SISTEM BASIS DATA

### 🗓️ Week 6: Intermediate to SQL (2)

#### 📍 INTEGRITY CONSTRAINTS
- Integrity Constraints guard against accidental damage to the database, by ensuring that authorized changes to the database do not result in a loss of data consistency. For example: A checking account must have a balance > $10,000.00. A salary of a bank employee must be at least $4.00 an hour. A customer must have a (non-null) phone number
- Constraints on a single relation: NOT NULL (declare something to not be null), UNIQUE, PRIMARY KEY, CHECK (P) where P is a predicate; specifies a predicate P that must be satisfied by every tuple in a relation

#### 📍 Referential Integrity
Ensures that a value that appears in one relation for a given set of attributes also appears for a certain set of attributes in another relation
-> Ex: if "George Orwell" is a author name appearing in one of the tuples in the books relation, then there exists a tuple in the authors relation for "George Orwell"
Foreign keys can be specified as part of the SQL create table statement
-> foreign key (Author_ID) references authors
By default, a foreign key references the primary-key attributes of the referenced table
SQL allows a list of attributes of the referenced relation to be specified explicitly
-> foreign key (Author_ID) references author (Author_ID)
When a referential-integrity constraint is violated, the normal procedure is to reject the action that caused the violation
There are some alternative; ON DELETE CASCADE or ON DELETE SET NULL. These two actions determine what should be done with rows that have a foreign key when the row they reference in another table is deleted

#### 📍 ON DELETE CASCADE:
Function: When a row in the parent table is deleted, all related rows in the child table are also automatically deleted
Ex: if we delete George Orwell from the authors table and the foreign key in the books table has ON DELETE CASCADE

#### 📍 ON DELETE SET NULL:
Function: When a row in the parent table is deleted, the foreign key values ina ll related rows in the child table are set to NULL
Ex: if we delete George Orwell from the authors table and the foreign key in the books table has ON DELETE SET NULL
also; in some cases we may want to delete related data to maintain data integrity, while in others we may want to remove the reference but still maintaine the row by setting the foreign key to NULL

#### 📍 Check Conditions
We could use a CHECK condition if we want to ensure that all books have a title of at least three characters.
CREATE TABLE Books (
       Book_ID INT,
       Book_Title VARCHAR(255)
                 CHECK (LENGTH(Book_Title) >= 3)
       Author_ID INT
);

If we try to add a new book with a title less than three characters, the CHECK condition would prevent this insertion.
INSERT INTO Books (Book_Title, Author_ID) VALUES ('Of', 3)
^^the above query would fail due to the CHECK condition

#### 📍 Assertion
Assertion is a condition declared over multiple tables. Suppose we want to ensure that the average salary of authors must be below a certain value across all authors in the database. Here's how it might look:
CREATE ASSERTION Authors_Salary_Assertion
CHECK (
        SELECT AVG(salary)
        FROM Authors
        WHERE Salary IS NOT NULL
) < 70000;

If we try to update the library:
UPDATE Authors
SET Salary = 75000
WHERE Author_Name = 'J.K. Rowling';
^^if the update makes the average salary exceed the limit defined in the assertion (70000 in this case), the update operation will fail

#### 📍 INDEX DEFINITION
INDEX CREATION
In database management, efficiently retrieving data is crucial for performance. While many queries only target a subset of records, without an organized retrieval method, the system might inefficiently scan through all records, which can be resource-intensive. This is where an index becomes invaluable.
An index, created using the create index command is a data structure that enables the database system to locate tuples with a specific attribute value in a relation swiftly and without referring to scan every tuple
This not only enhances query performance but also ensures a smoother and faster data retrieveal process, especially in large datasets

Example syntax to create an index:
CREATE INDEX <index_name> ON <relation_name> (attribute_name);
Suppose we have a table named 'student':
CREATE TABLE student (
    ID VARCHAR(5)
    name VARCHAR(20) NOT NULL,
    dept_name VARCHAR(20),
    tot_cred NUMERIC (3,0) DEFAULT 0;
    PRIMARY KEY (ID)
);

Creating an Index:
Creating an index on the 'ID' attribute:
CREATE INDEX studentID_index ON student (ID);
^^this will optimize the search queries related to the 'ID' attribute by creating a data structure that makes the retrieval of rows based on 'ID' more efficient

Query Example:
When we need to retrieve all details of the student with 'ID' '12345':
SELECT * FROM student WHERE ID = '12345';
result: ID 12345, Name Alice, dept_name Computer Sci, tot_cred 100
^^with 'studentID_index in palce, when executing the query, the system doesn't scan all the records in the 'student' table. instead it uses the index to locate the record with 'ID' '12345' efficiently, saving time and computational resources, especially vital when dealing with entensive datasets 

#### 📍 AUTHORIZATION
We may assign a user several forms of authorizations on parts of the database
Read: allows reading, but not modification of data
Insert: allows insertion of new data, but not modification of existing data
Update: allows modification, but not deletion of data
Delete: allows deletion of data

Each of these types of authorizations is called a privilege. We may authroize the user all, none, or a combination of these types of privileges on specified parts of a database, such as a relation or a view.

Forms of authorization to modify the database schema
Index: allows creation and deletion of indices
Resources: allow creation of new relations
Alteration: allows addition or deletion of attributes in a relation
Drop: allows deleteion of relations

To specify authorization in SQL
The grant statement is used to confer authorizationgrant <privilege list> on <relation or view> to <user list>
<user list> is a user-id, public (allows all valid users privilege), and a role
Example:grant select on department to Amit, Satoshi

Granting Privilege in SQL
Granting a privilege on a view does not imply granting any privileges on the underlying relations
The grantor of the privilege must already hold the privilege on the specified item (or be the database administrator)

To revoke authorization in SQL
The revoke statement is used to revoke authorizationrevoke <privilege-list> on <relation or view> from <user-list>

Example:
revoke select on student from U1, U2, U3

<privilege-list> may be all to revoke all privileges in the revokee may hold
If <revokee-list> includes public, all users lose the privlege except those granted it explicitly
If the same privilege was granted twice to the same user by different grantees, the user may retain the privilege after the revocation
All privileges that depend on the privilege being revoked are also revoked

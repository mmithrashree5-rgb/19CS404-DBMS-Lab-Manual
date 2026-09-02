# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

For example:

Test	Result
select * from Employee;
EmployeeID  Name        Department  Salary
----------  ----------  ----------  ----------
201         John Doe    HR          50000
202         Jane Smith  Engineerin  75000
203         Emily Davi  Marketing   60000

-

```sql
-INSERT INTO Employee (EmployeeID, Name, Department, Salary)
SELECT EmployeeID, Name, Department, Salary
FROM Former_employees;
```

**Output:**
<img width="1225" height="227" alt="image" src="https://github.com/user-attachments/assets/ef426b6d-df8c-4e60-bb58-656ca8637155" />



**Question 2**
---
-In the Employee table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT
 

For example:

Test	Result
SELECT * FROM Employee;
EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT
 

```sql
INSERT INTO Employee (EmployeeID, Name, Position, Department, Salary)
VALUES
  (5, 'George Clark', 'Consultant', NULL, NULL),
  (7, 'Noah Davis', 'Manager', 'HR', 60000),
  (8, 'Ava Miller', 'Consultant', 'IT', NULL);
```

**Output:**
<img width="645" height="226" alt="image" src="https://github.com/user-attachments/assets/4b08a86f-a616-493f-83ef-004b1845cd24" />



**Question 3**
---
Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

For example:

Test	Result
SELECT * FROM Student_details WHERE RollNo = 201;
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
201         David Lee   M           Physics     92


```sql
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (201, 'David Lee', 'M', 'Physics', 92);
```

**Output:**
<img width="717" height="182" alt="image" src="https://github.com/user-attachments/assets/bded9414-613f-443f-89c0-1fe7f6fff2cf" />



**Question 4**
---Write a SQL query to Add a new column mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           mobilenumb  number      0                       0


-- 
ALTER TABLE Student_details ADD mobilenumb number;

```

**Output:**
<img width="807" height="290" alt="image" src="https://github.com/user-attachments/assets/cc907190-2ca9-4133-84e0-4367512a5586" />



**Question 5**
---
Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.
For example:

Test	Result
INSERT INTO contacts (contact_id, first_name, last_name, email, phone) VALUES (1, 'John', 'Doe', 'john.doe@example.com', '1234567890');
SELECT * FROM contacts;

```sql
CREATE TABLE contacts(
   contact_id INTEGER PRIMARY KEY,
   first_name TEXT NOT NULL,
   last_name TEXT NOT NULL,
   email TEXT,
   phone TEXT NOT NULL CHECK(length(phone) >= 10)
   );
```

**Output:**
<img width="703" height="251" alt="image" src="https://github.com/user-attachments/assets/3ba0990d-0c06-40d9-94fc-c099b17b4e7d" />


**Question 6**
---
--Create a table named Members with the following columns:

MemberID as INTEGER
MemberName as TEXT
JoinDate as DATE
For example:

Test	Result
pragma table_info('Members');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           MemberID    INTEGER     0                       0
1           MemberName  TEXT        0                       0
2           JoinDate    DATE        0                       0


```sql
CREATE TABLE Members(
   MemberID INTEGER,
   MemberName TEXT,
   JoinDate DATE
   );
```

**Output:**

<img width="815" height="296" alt="image" src="https://github.com/user-attachments/assets/f9654762-31a2-4a49-a19c-af972d8d24f8" />


**Question 7**
---
--Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           Country     TEXT        0                       0
 

```sql
ALTER TABLE Student_details ADD Country TEXT;
```

**Output:**

<img width="697" height="282" alt="image" src="https://github.com/user-attachments/assets/309563c6-e614-4d4d-8dff-77a41ff27199" />


**Question 8**
---
-- Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;
InvoiceID   InvoiceDate  Amount      DueDate     OrderID
----------  -----------  ----------  ----------  ----------
1           2024-08-0

```sql
--CREATE TABLE Invoices(
   InvoiceID INTEGER PRIMARY KEY,
   InvoiceDate DATE,
   Amount REAL CHECK (Amount > 0),
   DueDate DATE CHECK (DueDate > InvoiceDate),
   OrderID INTEGER REFERENCES orders(OrderID)
   );

**Output:**

<img width="587" height="175" alt="image" src="https://github.com/user-attachments/assets/cc01c810-5e4e-4863-8895-7796d13f188f" />


**Question 9**
---
--Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.
For example:

Test	Result
-- Attempt to insert a record with NULL FirstName
INSERT INTO Employees (EmployeeID, FirstName, LastName, Email, Salary, DepartmentID)
VALUES (1, NULL, 'Doe', 'john.doe@example.com', 50000, 1);
Error: NOT NULL constraint failed: Employees.FirstName


```sql
CREATE TABLE Employees(
   EmployeeID INTEGER PRIMARY KEY,
   FirstName VARCHAR(255) NOT NULL,
   LastName VARCHAR(255) NOT NULL,
   Email VARCHAR(255) UNIQUE,
   Salary INT CHECK (Salary > 0),
   DepartmentID INT,
   FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
   );
```

**Output:**
<img width="583" height="348" alt="image" src="https://github.com/user-attachments/assets/27673467-d9d3-4ede-9831-dbf5b7552aaf" />


**Question 10**
---
-- create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.
For example:

Test	Result
INSERT INTO jobs (job_id, job_title, min_salary, max_salary) VALUES (1, 'Software Engineer', 9000, 15000);
SELECT * FROM jobs;
job_id      job_title          min_salary  max_salary
----------  -----------------  ----------  ----------
1           Software Engineer  9000 

```sql
--CREATE TABLE jobs(
   job_id INT,
   job_title VARCHAR(255) DEFAULT '',
   min_salary INT DEFAULT 8000,
   max_salary INT DEFAULT NULL
   );
```

**Output:**
<img width="632" height="265" alt="image" src="https://github.com/user-attachments/assets/21a6a655-ec98-431e-a841-3b11aefcd4ed" />




## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

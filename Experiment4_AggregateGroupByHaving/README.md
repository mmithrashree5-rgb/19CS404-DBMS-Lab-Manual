# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--How many patients are there in each city?

Sample table: Patients Table



For example:

Result
Address     TotalPatients
----------  -------------
Berlin      3
Chicago     4
Mexico      3

-- 

```sql
--SELECT Address, COUNT(*) AS TotalPatients
FROM Patients
GROUP BY Address;
```

**Output:**
<img width="322" height="357" alt="image" src="https://github.com/user-attachments/assets/0934085d-f79a-4f20-9e93-acdfda17fb6e" />



**Question 2**
---
--How many prescriptions were written by each doctor?

Sample tablePrescriptions Table



For example:

Result
DoctorID    TotalPrescriptions
----------  ------------------
1           1
2           1
3           1
4           1
5           1
6           1
7           1
8           1
9           1
10          1

```sql
--
 SELECT DoctorID, COUNT(*) AS TotalPrescriptions
FROM Prescriptions
GROUP BY DoctorID;

```

**Output:**


<img width="330" height="685" alt="image" src="https://github.com/user-attachments/assets/74ff3f4b-9888-4b7b-8047-f795e1f57b08" />

**Question 3**
---
-- What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table



For example:

Result
DoctorID    TotalAppointments
----------  -----------------
1           1
2           3
5           3
9           2
10          1

```sql
-- SELECT DoctorID, COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID;
```

**Output:**
<img width="355" height="568" alt="image" src="https://github.com/user-attachments/assets/ceb9c442-060c-4c5d-8e29-a874ed627422" />



**Question 4**
---
-- Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000

 

For example:

Result
COUNT
----------
4


```sql
-- SELECT COUNT(DISTINCT age) AS COUNT
FROM employee;
```

**Output:**
<img width="367" height="320" alt="image" src="https://github.com/user-attachments/assets/cc18e97a-309d-4830-bcc4-32dc920a81a4" />



**Question 5**
---
--Write a SQL query to count the number of customers. Return number of customers.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

 

For example:

Result
COUNT
----------
8


```sql
--
```SELECT COUNT(*) AS COUNT
FROM customer;

**Output:**

<img width="368" height="317" alt="image" src="https://github.com/user-attachments/assets/49cba121-8e1b-4f6f-8a18-93301247c16f" />

**Question 6**
---Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

 

For example:

Result
COUNT
----------
8

--

```sql
-- SELECT COUNT(*) AS COUNT
FROM customer
WHERE grade IS NOT NULL;
```

**Output:**
<img width="347" height="288" alt="image" src="https://github.com/user-attachments/assets/73db7525-cc85-45b2-a994-cac79cd6b7eb" />



**Question 7**
---
-- Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
age_difference
--------------
13


```sql
-- 
```SELECT MAX(age) - MIN(age) AS age_difference
FROM employee;

**Output:**
<img width="462" height="240" alt="image" src="https://github.com/user-attachments/assets/db4c35a8-ef03-438f-9118-06cd3b1356f6" />



**Question 8**
---Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1



For example:

Result
address     SUM(salary)
----------  -----------
Bhopal      8500
Hyderabad   4500
Indore      10000
Mumbai      6500

-- 

```sql
--SELECT address, SUM(salary) AS "SUM(salary)"
FROM customer1
GROUP BY address
HAVING SUM(salary) > 2000;
```

**Output:**
<img width="617" height="437" alt="image" src="https://github.com/user-attachments/assets/687007ef-fc12-4d4c-8680-102071227614" />

**Question 9**
---Write the SQL query that achieves the grouping of data by occupation, calculates the minimum work hours for each occupation, and excludes occupations where the minimum work hour is not greater than 8.

Sample table: employee1



For example:

Result
occupation  MIN(workhour)
----------  -------------
Business    10
Doctor      15
Engineer    12
Teacher     9

-- 

```sql
--SELECT occupation, MIN(workhour) AS "MIN(workhour)"
FROM employee1
GROUP BY occupation
HAVING MIN(workhour) > 8;
```

**Output:**
<img width="620" height="422" alt="image" src="https://github.com/user-attachments/assets/2204669d-f979-4ab5-87c0-e274e3b92980" />


**Question 10**
---
-- Write an SQL query that groups the customer data into 5-year age intervals, calculates the minimum salary for each group, and excludes groups where the minimum salary is not less than 2000.

Table: customer1



For example:

Result
age_group   MIN(salary)
----------  -----------
25          1500


```sql
--
```SELECT (age / 5) * 5 AS age_group,
       MIN(salary) AS "MIN(salary)"
FROM customer1
GROUP BY (age / 5) * 5
HAVING MIN(salary) < 2000;

**Output:**
<img width="602" height="283" alt="image" src="https://github.com/user-attachments/assets/8a8c165e-063f-466f-b046-d643120c452c" />




## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

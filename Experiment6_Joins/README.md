# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
-- Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

For example:

Result
name             cust_name        city             grade            salesman_id
---------------  ---------------  ---------------  ---------------  -----------
Bob Emily        Brad Davis       New York         200              5001
Bob Emily        Nick Rimando     Chennai          100              5001
Nail Knite       Graham Zusi      California       200              5002
Nail Knite       Julian Green     London           300              5002
Pit Alex         Brad Guzan       London           100              5005
Mc Lyon          Fabian Johns     Paris            300              5006
Paul Adam        Jozy Altidore    Moscow           200              5007
Lauson Hen       Geoff Cameron    Berlin           100              5003


```sql
--SELECT s.name, c.cust_name, c.city, c.grade, c.salesman_id
FROM salesman AS s
LEFT JOIN customer AS c
ON s.salesman_id = c.salesman_id;
```

**Output:**

<img width="765" height="768" alt="image" src="https://github.com/user-attachments/assets/d0eea671-7e5b-48c4-89a8-7bd960d8a0be" />


**Question 2**
---
-- Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the test name from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id



TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date



For example:

Result
patient_name     test_name
---------------  ---------------
Alice            Blood Pressure
Bob              X-Ray
Charlie          Blood Test


```sql
SELECT p.first_name AS patient_name, t.test_name
FROM patients AS p
INNER JOIN test_results AS t
ON p.patient_id = t.patient_id;```

**Output:**

<img width="357" height="486" alt="image" src="https://github.com/user-attachments/assets/75924b4c-8cdd-43ab-92e6-414eafff6a18" />

**Question 3**
---
--  From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
Customer Name    city             Salesman         commission
---------------  ---------------  ---------------  ---------------
Nick Rimando     Chennai          Bob Emily        0.15
Graham Zusi      California       Nail Knite       0.13
Brad Guzan       London           Pit Alex         0.11
Fabian Johns     Paris            Mc Lyon          0.14
Brad Davis       New York         Bob Emily        0.15
Geoff Cameron    Berlin           Lauson Hen       0.12
Julian Green     London           Nail Knite       0.13
Jozy Altidore    Moscow           Paul Adam        0.13

```sql
-- SELECT c.cust_name AS "Customer Name",
       c.city,
       s.name AS "Salesman",
       s.commission
FROM customer AS c
INNER JOIN salesman AS s
ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="658" height="861" alt="image" src="https://github.com/user-attachments/assets/19616f53-e206-4146-b480-8c04153a4ce5" />


**Question 4**
---
--SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
cust_name        city             ord_no           ord_date         Order Amount  name        commission
---------------  ---------------  ---------------  ---------------  ------------  ----------  ----------
Nick Rimando     Chennai          70002            2012-10-05       65.26         Bob Emily   0.15
Nick Rimando     Chennai          70008            2012-09-10       5760.0        Bob Emily   0.15
Nick Rimando     Chennai          70013            2012-04-25       3045.6        Bob Emily   0.15
Graham Zusi      California       70001            2012-10-05       150.5         Nail Knite  0.13
Graham Zusi      California       70007            2012-09-10       948.5         Nail Knite  0.13
Brad Guzan       London           70009            2012-09-10       270.65        Pit Alex    0.11
Fabian Johns     Paris            70010            2012-10-10       1983.43       Mc Lyon     0.14
Brad Davis       New York         70005            2012-07-27       2400.6        Bob Emily   0.15
Geoff Cameron    Berlin           70003            2012-10-10       2480.4        Lauson Hen  0.12
Geoff Cameron    Berlin           70004            2012-08-17       110.5         Lauson Hen  0.12
Julian Green     London           70012            2012-06-27       250.45        Nail Knite  0.13
Jozy Altidore    Moscow           70011            2012-08-17       75.29         Paul Adam   0.13

```sql
--SELECT c.cust_name,
       c.city,
       o.ord_no,
       o.ord_date,
       o.purch_amt AS "Order Amount",
       s.name,
       s.commission
FROM customer AS c
LEFT JOIN orders AS o
    ON c.customer_id = o.customer_id
LEFT JOIN salesman AS s
    ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="940" height="762" alt="image" src="https://github.com/user-attachments/assets/6053f410-cf87-47e0-9615-5429e81a8fa8" />

**Question 5**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
Customer Name    city             Salesman         city             commission
---------------  ---------------  ---------------  ---------------  ----------
Nick Rimando     Chennai          Bob Emily        New York         0.15
Graham Zusi      California       Nail Knite       Paris            0.13
Julian Green     London           Nail Knite       Paris            0.13
Jozy Altidore    Moscow           Paul Adam        Rome             0.13

```sql
SELECT c.cust_name AS "Customer Name",
       c.city,
       s.name AS "Salesman",
       s.city,
       s.commission
FROM customer AS c
INNER JOIN salesman AS s
ON c.salesman_id = s.salesman_id
WHERE c.city <> s.city
  AND s.commission > 0.12;```

**Output:**

<img width="757" height="557" alt="image" src="https://github.com/user-attachments/assets/ba3db201-06fd-406d-896b-615d4564b25a" />

**Question 6**
---
From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
Customer Name    city             Salesman         commission
---------------  ---------------  ---------------  ---------------
Nick Rimando     Chennai          Bob Emily        0.15
Graham Zusi      California       Nail Knite       0.13
Fabian Johns     Paris            Mc Lyon          0.14
Brad Davis       New York         Bob Emily        0.15
Julian Green     London           Nail Knite       0.13
Jozy Altidore    Moscow           Paul Adam        0.13
```sql
```SELECT c.cust_name AS "Customer Name",
       c.city,
       s.name AS "Salesman",
       s.commission
FROM customer AS c
INNER JOIN salesman AS s
ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;

**Output:**

<img width="631" height="702" alt="image" src="https://github.com/user-attachments/assets/cff855a5-88fc-466b-9dcc-08fd0041952b" />

**Question 7**
---write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
For example:

Result
Salesman         cust_name        city
---------------  ---------------  ---------------
Bob Emily        Brad Davis       New York
Nail Knite       Fabian Johns     Paris
Pit Alex         Brad Guzan       London
Pit Alex         Julian Green     London
Mc Lyon          Fabian Johns     Paris

-- 

```sql
SELECT s.name AS Salesman,
       c.cust_name,
       c.city
FROM salesman AS s
INNER JOIN customer AS c
ON s.city = c.city;```

**Output:**

<img width="448" height="625" alt="image" src="https://github.com/user-attachments/assets/5448e5c0-f8bc-4a5d-90fe-77800be8e9e8" />

**Question 8**
---Write an SQL query to retrieve all columns from the 'customer' table (aliased as 'c') using a LEFT JOIN with the 'orders' table on the 'customer_id' column, and filter the results to include only those orders placed between '2012-07-01' and '2012-07-30'.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

 

For example:

Result
customer_id      cust_name        city             grade            salesman_id
---------------  ---------------  ---------------  ---------------  -----------
3007             Brad Davis       New York         200              5001

```sql
```SELECT c.*
FROM customer AS c
LEFT JOIN orders AS o
ON c.customer_id = o.customer_id
WHERE o.ord_date BETWEEN '2012-07-01' AND '2012-07-30';

**Output:**

<img width="748" height="325" alt="image" src="https://github.com/user-attachments/assets/d04bfe6b-f43f-41cf-9f79-8b92bb561c5f" />

**Question 9**
---Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-02-01' and '2024-02-28'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id



APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date



For example:

Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
2                Bob              Miller           1995-08-23       2024-02-15      2024-03-01      2

```sql
```SELECT p.*
FROM patients AS p
INNER JOIN appointments AS a
ON p.patient_id = a.patient_id
WHERE a.appointment_date BETWEEN '2024-02-01' AND '2024-02-2

**Output:**
<img width="880" height="345" alt="image" src="https://github.com/user-attachments/assets/5be6f176-e125-47dd-a900-3e4e06696378" />


**Question 10**
---Write the SQL query that achieves the selection of all columns from the "patients" table, with an inner join on the "doctor_id" column, and includes a condition filtering for patients whose doctors have the first name 'John' and last name 'Smith'.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)

For example:

Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
1                Alice            Williams         1980-05-12       2024-01-10                      1

```sql
```
SELECT p.*
FROM patients AS p
INNER JOIN doctors AS d
ON p.doctor_id = d.doctor_id
WHERE d.first_name = 'John'
  AND d.last_name = 'Smith';
**Output:**
<img width="923" height="318" alt="image" src="https://github.com/user-attachments/assets/4d5195e6-ef97-4143-958e-79271808b76c" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.

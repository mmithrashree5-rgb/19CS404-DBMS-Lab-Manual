# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL statement to Increase the selling price by 15% in the products table where quantity in stock is less than 50 and supplier ID is 10.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lv     INT        
quantity       INT        
supplier_id    INT           
For example:

Test	Result
select changes();
changes()
----------
4


```sql
UPDATE Products
SET sell_price=sell_price*1.15
WHERE quantity<50
AND supplier_id=10
```

**Output:**
<img width="997" height="407" alt="image" src="https://github.com/user-attachments/assets/9701fa18-1efe-4797-aee1-cbad4484b5d5" />


**Question 2**
---Write a SQL statement to Change the category to 'Household' where product name contains 'Detergent' in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT           
For example:

Test	Result
select changes();
changes()
----------
4

```sql
```UPDATE Products
SET category='Household'
WHERE product_name LIKE
'%Detergent%';

**Output:**
<img width="1012" height="401" alt="image" src="https://github.com/user-attachments/assets/a7b119dc-4859-4067-a810-cf63623d0d9b" />


**Question 3**
---
-- Write a SQL statement to change the first_name column of employees table with 'John' for those employees whose department_id is 80 and gets a commission_pct below 0.35.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT * FROM EMPLOYEES WHERE DEPARTMENT_ID=80 AND COMMISSION_PCT=.25;
EMPLOYEE_ID  FIRST_NAME  LAST_NAME   EMAIL       PHONE_NUMBER        HIRE_DATE   JOB_ID      SALARY      COMMISSION_PCT  MANAGER_ID  DEPARTMENT_ID
-----------  ----------  ----------  ----------  ------------------  ----------  ----------  ----------  --------------  ----------  -------------
151          John        Bernstein   DBERNSTE    011.44.1344.345268  8/7/87      SA_REP      9500        0.25            145         80
152          John        Hall        PHALL       011.44.1344.478968  8/8/87      SA_REP      9000        0.25            145         80
161          John        Sewall      SSEWALL     011.44.1345.529268  8/17/87     SA_REP      7000        0.25            146         80
162          John        Vishney     CVISHNEY    011.44.1346.129268  8/18/87     SA_REP      10500       0.25            147         80
168          John        Ozer        LOZER       011.44.1343.929268  8/24/87     SA_REP      11500       0.25            148         80
175          John        Hutton      AHUTTON     011.44.1644.429266  8/3

```sql
--UPDATE EMPLOYEES
SET FIRST_NAME = 'John'
WHERE DEPARTMENT_ID = 80
  AND COMMISSION_PCT < 0.35;
```

**Output:**
<img width="1201" height="466" alt="image" src="https://github.com/user-attachments/assets/1ef74f89-66bf-46e0-957e-535596e1490a" />



**Question 4**
---
--Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.



For example:

Test	Result
select changes();
changes()
----------
2


```sql
--UPDATE purchases
SET per_unit_price = 25,
    total_price = quantity * 25
WHERE purchase_date = '2022-08-15'
  AND product_id = 12;
```

**Output:**
<img width="877" height="367" alt="image" src="https://github.com/user-attachments/assets/763e0e24-7f35-4f74-9b2f-029059bb8e41" />



**Question 5**
---Write a SQL statement to Update the product_name to 'Premium Bread' whose product ID is 5 in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```sql
-- 
```UPDATE products
SET product_name = 'Premium Bread'
WHERE product_id = 5;

**Output:**
<img width="950" height="305" alt="image" src="https://github.com/user-attachments/assets/b7607e6f-56c6-4678-aa2b-8f5449ad1f2e" />



**Question 6**
---Write a SQL query to Delete customers with 'GRADE' 2 and 'CUST_NAME' starting with 'M', and whose 'PAYMENT_AMT' is less than 3000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
1

-- 

```sql
--DELETE FROM Customer
WHERE GRADE = 2
  AND CUST_NAME LIKE 'M%'
  AND PAYMENT_AMT < 3000;
```

**Output:**
<img width="1201" height="298" alt="image" src="https://github.com/user-attachments/assets/2f1778eb-2b15-46d4-bdbf-95d91e14eb9b" />




**Question 7**
---Write a SQL query to delete a specific doctor from Doctors table whose ID is 1.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
--

```sql
-- DELETE FROM Doctors
WHERE doctor_id = 1;
```

**Output:**
<img width="520" height="162" alt="image" src="https://github.com/user-attachments/assets/31cab732-23da-4452-baf6-ee17a5ade058" />


**Question 8**
---
--Write a SQL query to Delete customers with 'GRADE' 3 and whose 'CUST_NAME' contains the substring 'BBB', and 'PAYMENT_AMT' is greater than 2000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
0


```sql
-- 
```DELETE FROM Customer
WHERE GRADE = 3
  AND CUST_NAME LIKE '%BBB%'
  AND PAYMENT_AMT > 2000;

**Output:**

<img width="1291" height="465" alt="image" src="https://github.com/user-attachments/assets/eff4acbb-dbf6-47a7-bece-82b488b9d9a2" />


**Question 9**
---Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

-- 

```sql
--DELETE FROM Doctors
WHERE specialization = 'Cardiology';
```

**Output:**

<img width="537" height="302" alt="image" src="https://github.com/user-attachments/assets/4ff404c8-ff63-4725-895b-eaab4f16e772" />


**Question 10**
---Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology


```sql
-- 
```DELETE FROM Doctors
WHERE doctor_id BETWEEN 2 AND 4;

**Output:**
<img width="506" height="777" alt="image" src="https://github.com/user-attachments/assets/c381def3-1d72-4fc1-a8c5-3e77934c1000" />



## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.

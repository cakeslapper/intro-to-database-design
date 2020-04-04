# Intro to Database Design SQL
SQL statements learned in my Intro to Database Design class

## [Table of Contents](#table-of-contents)
   - [Table](#table)
     - [Create](#create)
     - [Copy](#copy)
     - [Drop](#drop)
     - [Insert](#insert)
         + [Copy all data to table](#copy-all-data-from-one-table-and-insert-it-into-a-second-table-by-using-a-mix-of-select-and-insert-statements)
         + [Copy some data to table](#copy-some-data-from-one-table-and-insert-it-into-a-second-table-by-using-a-mix-of-select-and-insert-statements)
     - [Update](#update)
     - [Delete](#delete)
   - [Alter](#alter)
   - [Select](#select)
   - [CONSTRAINTS](#constraints)
     - [Column constraints](#column-constraints)
     - [Unnamed](#unnamed)
     - [Named](#named)
     - [Table level constraints](#table-level-constraints)
   - [Tablespace](#tablespace)

### Table
#### Create
###### Create a table
- **CREATE TABLE** *table_name* (*data* *data_type*);
```sql
CREATE TABLE Person (
   PersonID number(10),
   LastName varchar2(255),
);
```
---
#### Copy
###### Copy from an existing table
- **CREATE TABLE** *table_name* **AS** **SELECT** *columns* **FROM** *existing_table*
```sql
CREATE TABLE TestTable AS
SELECT customername, contactname
FROM customers;
```
---
#### Drop
###### Drop an existing table
- **DROP TABLE** *table_name*;
```sql
DROP TABLE table_name;
```
---
#### Insert
###### Insert records into an existing table
- **INSERT INTO** *table_name* **VALUES** *(val1, val2, val3, ...)*;

```sql
INSERT INTO Persons VALUES (101, 'Person1', 'LastName1', '123 Main St.', 'Manchester');
```
######  Copy _all_ data from one table and insert it into a second table by using a mix of select and insert statements
- **INSERT INTO** employee_copy **SELECT** * **FROM** employee;

######  Copy _some_ data from one table and insert it into a second table by using a mix of select and insert statements
- **INSERT INTO** employee_salary_Info **SELECT** employee_id, first_name, last_name, salary **FROM** employee;
---
#### Update
######  Change existing rows either by adding new data or modifying existing data. It can be used to add values where there was a NULL, fix spelling mistakes, etc
- **UPDATE** table_name **SET** column1 = value1, column2 = value2, ... **WHERE** condition;
```sql
UPDATE Employee SET salary = 25000 WHERE salary < 25000;
UPDATE Employee SET salary = salary + 25000 WHERE salary < 25000;
UPDATE Employee SET salary = 50000 WHERE salary IS NULL;
```
---
#### Delete
###### Delete existing records from an existing table
- **DELETE FROM** *table_name* **WHERE** *PersonID = 101*;
```sql
DELETE FROM Persons WHERE PersonID = 101;
```
---
### Alter
######  Add, delete or modify columns in an existing table/add and drop various constraints on an existing table
- **ALTER TABLE** table_name **DROP** column_name;
- **ALTER TABLE** table_name **ADD** column_name datatype;
- **ALTER TABLE** table_name **MODIFY** column_name datatype;
- **ALTER TABLE** table_name **RENAME COLUMN** column_name **TO** new_column_name;

```sql
ALTER TABLE Persons DROP (PID, DOB);
ALTER TABLE Persons ADD (Email varchar2(255), DOB date);
ALTER TABLE Persons ADD Email varchar2(255);
ALTER TABLE Persons MODIFY DOB varchar2(12);
ALTER TABLE Persons RENAME COLUMN DOB TO DataOfBirth;
```
---
### Select
###### Select data from the database
1. **SELECT FROM**
2. **WHERE**
3. **> < <> >= <= != =**
4. **AND** / **OR**
5. **LIKE**
6. **BETWEEN**
7. **NOT**
8. **IN**
9. **AS**
10. **DISTINCT**
11. **ORDER BY** .. **ASC** / **DESC**
12. **IS NULL** / **IS NOT NULL**
13. **GROUP BY** - often used with aggregate functions below, "groups"/displays by distinct column(s) & its related data
14. **COUNT()** -  returns the _number_ of rows that matches a specified criteria
15. **AVG()** - returns the _average_ of a numeric column
16. **SUM()** - returns the _total sum_ of a numeric column.

```sql
1. SELECT column1, column2 FROM table_name;
2. SELECT column1, column2 FROM table_name WHERE first_name = 'Alice';
3. SELECT column1, column2 FROM table_name WHERE first_name != 'Alice';
4. SELECT column1, column2 FROM table_name WHERE first_name > 'Alice' AND last_name <= 'Log';
5. SELECT column1, column2 FROM table_name WHERE first_name LIKE 'Al_ce' OR first_name LIKE 'Al%';
6. SELECT column1, column2 FROM table_name WHERE first_name BETWEEN 'Alice' AND 'Mary';
7. SELECT column1, column2 FROM table_name WHERE first_name NOT BETWEEN 'Joe' AND 'Leroy';
8. SELECT first_name FROM students WHERE age IN (5, 15, 20);
9. SELECT first_name AS "first", last_name AS "last" FROM employee;
10. SELECT DISTINCT first_name FROM students;
11. SELECT first_name, last_name FROM employee ORDER BY last_name ASC, first_name DESC;
12. SELECT first_name, salary FROM employee WHERE salary IS NULL OR last_name IS NOT NULL;
13. SELECT customer_id FROM customer_order GROUP BY customer_id;
SELECT Customer_id, COUNT(Customer_Id) FROM Customer_Order GROUP BY Customer_id;
SELECT Customer_id, COUNT(Customer_Id) FROM Customer_Order GROUP BY Customer_id ORDER BY COUNT(Customer_id);
14. SELECT COUNT(column_name) FROM table_name WHERE condition;
SELECT COUNT(*) FROM Customer_Order; 
SELECT COUNT(Distinct Customer_Id) FROM Customer_Order;
15. SELECT AVG(column_name) FROM table_name WHERE condition;
SELECT AVG(Price) FROM Products;
SELECT department_id, AVG(Price) FROM Products GROUP BY department_id;
16. SELECT SUM(column_name) FROM table_name WHERE condition;
SELECT SUM(price) FROM product;
SELECT department_id, SUM(price) FROM product GROUP BY department_id;
```
---
### CONSTRAINTS
###### Column constraints
- **Not null**: the column must have a value
- **Unique**: no two rows could have the same value for that column
- **Primary key**: by default, primary keys must be unique and not null
- **Foreign key**: must be a primary key in another table
- **Default** (not really a constraint): assigns a default value if no value is given
- **Check**: used to limit the value range that can be placed in a column
###### Unnamed
```sql
CREATE TABLE Persons (
   PersonID int PRIMARY KEY,
   LastName varchar(255) NOT NULL UNIQUE,
   FirstName varchar(255),
   Address varchar(255),
   City varchar(255),
   Country varchar(50) DEFAULT 'USA',
   Balance number DEFAULT 100,
   Age int CHECK (Age>=18)
);
```
###### Named
```sql
PersonID int CONSTRAINT person_pk PRIMARY KEY
```
###### Table level constraints
```sql
CONSTRAINT age_limit CHECK (Age>=18),
CONSTRAINT check_age_city CHECK (Age>=18 AND City=‘Manchester'),
CONSTRAINT salary_date CHECK (HireDate > ‘01-Jan-2010’ OR Salary > 5000),
CONSTRAINT PID_Valid CHECK (PID LIKE ‘@%’),
CONSTRAINT constraintName PRIMARY KEY (columnNames),
CONSTRAINT fk_emp_dept FOREIGN KEY (department_id) REFERENCES department(department_id)
```
---
### Tablespace
###### Create Tablespace (storage location where actual data can be kept)
- **CREATE TABLESPACE** *name* **DATAFILE** *db_file_name_and_location* **SIZE** *size* **AUTOEXTEND** *yes/no*
```sql
CREATE TABLESPACE tablespace_name
DATAFILE 'c:\users\me\oracle\test_tablespace.dbf'
SIZE 50M
AUTOEXTEND ON NEXT 10M MAXSIZE 250M;
```


# intro-to-database-design
SQL statements learned in my Intro to Database Design class

### Select
###### Select data from the database
- **SELECT** *column1, column2* **FROM** *table_name*;
- SELECT *column1, column2* FROM *table_name* **WHERE** *first_name* = 'Alice';
- SELECT *column1, column2* FROM *table_name* WHERE *first_name* **!=** 'Alice';
- SELECT *column1, column2* FROM *table_name* WHERE *first_name* **>** 'Alice' **AND** last_name **<=** 'Log';
- SELECT *column1, column2* FROM *table_name* WHERE *first_name* **LIKE** 'Al_ce' **OR** *first_name* LIKE 'Al%';
- SELECT *column1, column2* FROM *table_name* WHERE *first_name* **BETWEEN** 'Alice' **AND** 'Mary';
- SELECT *column1, column2* FROM *table_name* WHERE *first_name* **NOT** BETWEEN 'Joe' AND 'Leroy';
- SELECT *first_name* FROM *students* WHERE *age* **IN (5, 15, 20)**;
- SELECT *first_name* **AS** "first", *last_name* **AS** "last" FROM *employee*;
- SELECT **DISTINCT** *first_name* FROM *students*;
- SELECT *first_name*, *last_name* FROM *employee* **ORDER BY** *last_name* **ASC**, *first_name* **DESC**;
- SELECT *first_name*, *salary* FROM employee WHERE salary **IS NULL** OR last_name **IS NOT NULL**;

### Table
###### Create a table
- **CREATE TABLE** *table_name* (*data* *data_type*);

      CREATE TABLE Person (

      PersonID number(10),

      LastName varchar(255),

      FirstName varchar(255),

      Address varchar(255),

      City varchar(255)

      );
###### Copy from an existing table
- **CREATE TABLE** *table_name* **AS** **SELECT** *columns* **FROM** *existing_table*

      CREATE TABLE TestTable AS
      SELECT customername, contactname
      FROM customers;
###### Drop an existing table
- **DROP TABLE** *table_name*;

      DROP TABLE table_name;
      
---
### Tablespace
###### Create Tablespace (storage location where actual data can be kept)
- **CREATE TABLESPACE** *name* **DATAFILE** *db_file_name_and_location* **SIZE** *size* **AUTOEXTEND** *yes/no*

      CREATE TABLESPACE tablespace_name
      
      DATAFILE 'c:\users\me\oracle\test_tablespace.dbf'

      SIZE 50M

      AUTOEXTEND ON NEXT 10M MAXSIZE 250M;



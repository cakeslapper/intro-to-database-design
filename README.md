# intro-to-database-design
SQL statements learned in my Intro to Database Design class

### Select
Select data from the database
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

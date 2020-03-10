# intro-to-database-design
SQL statements learned in my Intro to Database Design class

### Select
Select data from the database
- **SELECT** *column1, column2* **FROM** *table_name*;
- SELECT *column1, column2* FROM *table_name* **WHERE** *first_name* = 'Alice';
- SELECT *column1, column2* FROM *table_name* WHERE *first_name* **!=** 'Alice';
- SELECT *column1, column2* FROM *table_name* WHERE *first_name* > 'Alice' **AND** last_name <= 'Log';
- SELECT *column1, column2* FROM *table_name* WHERE *first_name* **LIKE** 'Al_ce';
- SELECT *column1, column2* FROM *table_name* WHERE *first_name* LIKE 'Al%';

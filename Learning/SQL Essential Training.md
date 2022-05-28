# [SQL Essential Training](ttps://www.linkedin.com/learning/sql-essential-training-3/)

## 1. Installation

## 2. SQL Overview
### 2-1. About SQL 
```SELECT * FROM Countries WHERE Continent = 'Europe';``` (Statement)

FROM clause + WHERE clause (logical expression) // Create + Read + Update + Delete 

1. SELECT: ```SELECT * FROM Customer;```
2. INSERT: ```INSERT INTO customer (name, city, state) VALUES ('Jimi', 'Rento','WA');```
3. UPDATE: ```UPDATE Customer SET address = '123', Zip = '908' WHERE id = 5;```
4. DELETE: ```DELECT FROM customer WHERE id = 4;```

### 2-2. Database Orgainization 
A database has tables, tables has rows and columns; a row is like a record, a column is like a field, a unique key identifies a table row; 

Tables are related by keys.

### 2-3. Statements
1. SELECT: selecting rows and columns
2. COUNTING
3. INSERT
4. UPDATE 
5. DELETE 

### 2-4. Exercise
Q1. **Foreign Key**: is a database key that is used to link two tables together     
    **Primary Key**: is a key in a relational database that is unique for each record
    
Q2. Which statement is true about inserting data to a table?    
A: You must execute the select statement after the insert into statement to see the result with the added row.

Q3. What is the best way to return the number of rows in the student table?   
A: ```SELECT COUNT (*) FROM student;```

Q4. What is an example of a query to get only data containing the word "Apple"?    
A: ```SELECT * FROM Fruits WHERE Name = 'Apple';``` 

## 3. Fundamental Concepts
1. Creating / deleting a table
2. inserting / deleting rows
3. The NULL value
4. constraining columns
5. changing a schema
6. ID columns 
7. filtering data
8. Removing duolicates 
9. Ordering output
10. Conditional expressions


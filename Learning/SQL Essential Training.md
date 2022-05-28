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
**Q1.** **Foreign Key**: is a database key that is used to link two tables together     
    **Primary Key**: is a key in a relational database that is unique for each record
    
**Q2.** Which statement is true about inserting data to a table?    
A: You must execute the select statement after the insert into statement to see the result with the added row.

**Q3.** What is the best way to return the number of rows in the student table?   
A: ```SELECT COUNT (*) FROM student;```

**Q4.** What is an example of a query to get only data containing the word "Apple"?    
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

### Exercise 
**Q1.** To delete a table, use __ statement. A: ```DROP TABLE```    

**Q2.** To insert a blank row use the __ clause. A: ```DEFAULT VALUES``` 

**Q3.** Which statement is true about the ```DROP TABLE``` statement?    
A: The ```DROP TABLE``` statement enables you to delete a table from a database.

**Q4.** Column constraints are applied when the table is created.    A: True 

**Q5.** The WHERE clause is used to: filter query results by row. 

**Q6.** What is the correct format for creating an ID column for the Vehicles table in SQLite?   
A: ```CREATE TABLE vehicles (VehicleID INTEGER PRIMARY KEY);```

**Q7.** Why do you need to be careful and consult documentation when altering an existing table?    
A: Syntax capabilities vary widely from one implementation of SQL to another.

**Q8.** The ```ALTER``` is used to change a table schema.   

**Q9.** Why would you use column constraints?   
A: To make sure that values obey desired rules or behaviours. 

**Q10.** Which statement is true about the id column in a SQL table?   
A: A table can only have one id column.

**Q11.** How do you add a new column and its data type to an existing table?    
A: Once a table has been created, use the ```ALTER TABLE``` statement to add a new column and its data type.

**Q12.** Which constraint ensures a column cannot have any duplicate values including null values?    
A: ```UNIQUE NOT NULL```

**Q13.** To what does a table schema refer?   
A: the number of, titles for, and data types in columns

**Q14.** The ```CREATE TABLE``` statement:   
creates a table, defines the table columns, defines the table schema. 

## 4. Relationships
### 4-1. JOIN 
INNER JOIN, LEFT OUTER JOIN, RIGHT OUTER JOIN, FULL OUTER JOIN 

### 4-2. Exercise
**Q1.** What type of relationship requires the use of a junction table?   
A: many-to-many

**Q2.** A joined query operates on columns from two or more tables in one query. -- True 

**Q3.** What is the result of an inner join?   
A: The results will include the rows from both tables where the join condition is met. 

**Q4.** A joined query can include __ tables.  -- any number of 

**Q5.** Why is a junction table necessary when combining data between tables?   
A: A relationship is provided between the tables so they can be linked.

## 5. Strings 

**Q1.** What are the three arguments for the ```SUBSTR()``` function in SQLite?  
A: string to evaluate, starting position, length of string   
What if only has 2 argument? -- to retrieve a substring from a specified starting point to the end of the string

**Q2.** Remove Space -- RTRIM / LTRIM / TRIM()

**Q3.** If ID='CH297', which code returns the last 3 characters?   
A: ```SELECT SUBSTR(ID,3);```

**Q4.** Which code correctly returns the length of hospital names in the patient table in SQLite?   
A: ```SELECT LENGTH(hospital);```

**Q5.** standard SQL: both ```LENGTH() & SUBSTSR()``` are not!!

**Q6.** What is the result of the following statement? ```SELECT TRIM('The test was a treat','t');```   
A: ```The test was a trea```

**Q7.** Which choice is the best way to represent a string?
A: ```SELECT 'Karen''s Classroom';```

**Q8.** The ```UPPER() & LOWER()``` functions can be used to fold the case of a string for sorting and comparisons.   
-- True 

**Q9.** Why is it important to convert all fields to the same case?   
A: SQLite compares data based on case.




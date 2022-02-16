# HackeRank examples:

## BASIC SELECT
### 1. Weather Observation Station
![image](https://user-images.githubusercontent.com/56160038/152649099-22f8dc08-f73f-48e7-a388-2ec7af1ce4a8.png)

#### 1-1.
Query a list of CITY and STATE from the STATION table.
```MYSQL
SELECT CITY, STATE FROM STATION
```

#### 1-3.
Query a list of CITY names from STATION for cities that have an even ID number.     
Print the results in any order, but exclude duplicates from the answer.
```MYSQL
SELECT DISTINCT CITY FROM STATION
WHERE (ID % 2) = 0
```

#### 1-4. 
Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.
```MYSQL
SELECT (COUNT(CITY)) - (COUNT(DISTINCT CITY)) FROM STATION
```

#### 1-5. 
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name).    
If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.
```MYSQL
SELECT CITY, LENGTH(CITY) FROM STATION
ORDER BY LENGTH(CITY), CITY ASC
LIMIT 1;

SELECT CITY, LENGTH(CITY) FROM STATION 
ORDER BY LENGTH(CITY) DESC
LIMIT 1;
```

#### 1-6. 
Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.
```MYSOL
SELECT DISTINCT CITY
FROM STATION
WHERE REGEXP_LIKE(City, '^[AEIOU]');
```


#### 1-7. 
Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.
```mysql
SELECT DISTINCT CITY FROM STATION 
WHERE REGEXP_LIKE(CITY, '[aeiou]$');
```

#### 1-8.
Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters.    
Your result cannot contain duplicates.
```MYSQL
SELECT DISTINCT CITY FROM STATION 
WHERE REGEXP_LIKE(CITY, '[aeiou]$') AND REGEXP_LIKE(City, '^[AEIOU]');
```

#### 1-9. 
Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.
```MYSQL
SELECT DISTINCT CITY FROM STATION 
WHERE REGEXP_LIKE(CITY, '^[^AEIOU]');
```
#### 1-10.
Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.
```MYSQL
SELECT DISTINCT CITY FROM STATION 
WHERE REGEXP_LIKE(CITY, '[^aeiou]$')
```

#### 1-11. 
Query the list of CITY names from STATION that either do not start with vowels **or** do not end with vowels.    
Your result cannot contain duplicates.
```MYSQL
SELECT DISTINCT CITY FROM STATION 
WHERE REGEXP_LIKE(CITY, '[^aeiou]$') OR REGEXP_LIKE(CITY, '^[^AEIOU]');
```

#### 1-12.
Query the list of CITY names from STATION that do not start with vowels **and** do not end with vowels.    
Your result cannot contain duplicates.
```MYSQL
SELECT DISTINCT CITY FROM STATION
WHERE REGEXP_LIKE(CITY, '[^aeiou]$') AND REGEXP_LIKE(CITY, '^[^AEIOU]');
```

### 2. Higher than 75 marks
![image](https://user-images.githubusercontent.com/56160038/152651751-2cef5342-021a-44d8-a047-852539572233.png)

Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name.    
If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

```MYSQL
SELECT NAME FROM STUDENTS
WHERE MARKS > 75
ORDER BY RIGHT(NAME, 3), ID ASC;
```

## ADVANCED SELECT

### 3. Type of Triangle
![image](https://user-images.githubusercontent.com/56160038/152652862-09355e35-6dc2-4544-8c16-cff1ca4568ee.png)

Write a query identifying the type of each record in the TRIANGLES table using its three side lengths.   
Output one of the following statements for each record in the table:

**Equilateral**: It's a triangle with  sides of equal length.    
**Isosceles**: It's a triangle with  sides of equal length.    
**Scalene**: It's a triangle with  sides of differing lengths.    
**Not A Triangle**: The given values of A, B, and C don't form a triangle.    
```MYSQL 
SELECT CASE             
            WHEN A + B > C AND B + C > A AND A + C > B THEN
                CASE 
                    WHEN A = B AND B = C THEN 'Equilateral'
                    WHEN A = B OR B = C OR A = C THEN 'Isosceles'
                    ELSE 'Scalene'
                END
            ELSE 'Not A Triangle'
        END
FROM TRIANGLES;
```


### 4. Occupation 
![image](https://user-images.githubusercontent.com/56160038/154362598-0c81cd70-8f3b-4916-a8d3-aab8ac542954.png)

Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation.    


# Joining Data in SQL
using SQL to join two or more tables together into a single table. 

## Introduction to INNER JOIN

### 1. INNER JOIN
left_table and right_table ==> Key : Val 
```SQL
SELECT p1.country, p1.continent, prime_minister, president
FROM prime_ministers AS p1
INNER JOIN presidents AS p2
ON p1.country = p2.country;
```
### 2. via USING 
``` sql 
SELECT left_table.is AS L_id, 
       left_table.val AS L_val,
       right_table.val AS R_val
FROM left_table
INNER JOIN right_table
USING(id);

======
SELECT p1.country, p1.continent, prime_minister, president
FROM presidents AS p1
INNER JOIN prime_ministers AS p2
USING(country);
```
### 3. Self-ish joins, just in CASA
```sql 
SELECT p1.country AS country1, p2.country AS country2, p1.continent
FROM prime_ministers AS p1
INNER JOIN prime_ministers AS p2
ON p1.continent = p2.continent
LIMIT 14;


=====
SELECT p1.country AS country1, p2.country AS country2, p1.continent
FROM prime_ministers AS p1
INNER JOIN prime_ministers AS p2
ON p1.continent = p2.continent 
AND p1.country <> p2.country
LIMIT 13;
```

CASE WHEN: 
``` SQL
SELECT name, continent, indep_year,
CASE WHEN indep_year < 1900 THEN 'before 1900'
     WHEN indep_year <= 1930 THEN 'between 1900 and 1930'
     ELSE 'after 1930' END 
     AS indep_year_group
FROM states
ORDER BY indep_year_group;
```

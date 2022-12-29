## 计算函数

### AVG 平均值
通过对表中行数计数并计算其列值之和，求得该列的平均值。   
 AVG() 可用来返回所有列的平均值，也可以用来返回特定列或行的平均值    
 
### COUNT() 计数函数
确定表中行的数目或符合特定 条件的行的数目。   

* 使用 COUNT(*)对表中行的数目进行计数，不管表列中包含的是空值（NULL）还是非空值。 
* 使用 COUNT(column)对特定列中具有值的行进行计数，忽略 NULL 值。

### MAX() & MIN()
返回指定列中的最大/小值，（）需指定要返回最大/小值的列名   

### SUM()
返回指定列的总和

### ROUND() 取整函数 
```ROUND（value，n）```其中 value代表想要限制小数位数的字段，n代表想要限制的小数位数


## GROUP BY & HAVING 分组
1. GROUP BY 子句可以包含任意数目的列，因而可以对分组进行嵌套， 更细致地进行数据分组。
2. 除聚集计算语句外，SELECT 语句中的每一列都必须在 GROUP BY 子句 中同时给出。
3. 如果分组列中包含具有 NULL 值的行，则 NULL 将作为一个分组返回。 如果列中有多行 NULL 值，它们将分为一组。
4. GROUP BY 子句必须出现在 WHERE 子句之后，ORDER BY 子句之前。

* 分组的结果下进行过滤，则使用HAVING！

## Subquery 子查询
嵌套在其他查询中的查询 -- 子查询总是从内向外处理。
```SQL 
SELECT device_id, question_id, result
FROM question_practice_detail
WHERE device_id IN 
// 首先执行这个查询，返回所有学校是UCL的 device_id，
(SELECT device_id FROM user_profile
WHERE university ='UCL')
;
```

## JOIN 连接查询

### Left JOIN 左连接
是以左表为基础，根据ON后给出的两表的条件将两表连接起来。  
结果会将左表所有的查询信息列出，而右表只列出ON后条件与左表满足的部分。

在使用Left join 时，写在前面的表为匹配时的底表，使用on给出匹配条件，匹配条 件可以不唯一。

### Right JOIN 右连接
以右表为基础，返回右表的所有行

### Inner JOIN 
内连接是A表的所有行和B表的所有行在指定条件下得到的交集

### 笛卡尔积
在进行表的连接时，大多数情况下都必须要限制匹配条件(ON);    
如果在匹配时没有限制条件就会导致笛卡尔积。    
笛卡尔积表示两个表中的每一行数据任意结合，表A中有n行 x 表B中有m行 = `m*n` 行

## UNION 组合查询
执行多个SELECT 查询，并将结果合并为一个查询结果返回
1. 在一个查询中从不同的表返回结构数据；
2. 对一个表执行多个查询，按一个查询返回数据。

### UNION ALL
UNION 从查询结果中自动去掉重复的行；如果不去重则使用UNION ALL

## 条件函数
### IF 
``` if(x=n,a,b)，x=n代表判断条件，如果x=n时，那么结果返回a，否则返回b```

### CASE WHEN 
case when可以 对多个条件进行转换，
```sql 
Select
CASE
WHEN SCORE = 'A' THEN '优'
WHEN SCORE = 'B' THEN '良'
WHEN SCORE = 'C' THEN ‘中'
ELSE ‘不及格'
END 
//注意这里需要加end作为结束
```

## 日期函数
常见的日期格式：'yyyy-MM-dd' 和 'yyyyMMdd'

### 时间戳-日期格式转化
时间戳是数据库中自动生成的唯一二进制数字，表明数据库中数据修改发生的相对顺序，其记录形式类似：1627963699     
时间戳和日期格式之间可以利用from_unixtime和 unix_timestamp进行转换。    
* from_unixtime可以将时间戳转换成日期：
```sql
select
from_unixtime(time,'yyyy-MM-dd') as time
From table
```
* unix_timestamp可以将日期转换回时间戳，
```sql
select
from_unixtime('2021-08-01','yyyy-MM-dd') as time
```

### 年月日截取
year(),month(),day()
```sql
select
year('2021-08-01'),month('2021-08-01'),day('2021-08-01')
```

### 日期差计算

#### datediff
datediff的作用为计算两个日期之间的天数间隔    
```datediff(date1, date2)``` 返回起始时间 date1 和结束时间 date2 之间的天数     
date1 > date2：返回正数; date1 < date 2: 返回负数 

#### date_sub
```date_sub (string startdate, interval int day)```   
返回开始日期startdate减少 days天后的日期

### date_add
```date_add(string startdate, interval int day) ```   
返回开始日期startdate增加days天后的日期


## 文本函数

### length 
返回文本字段中值的长度

### concat 
将两个或多个字符串连接起来，形成一个单一的字符串
```sql
select concat(‘abc’,'bcd’) == 'abcbcd'
```

### 分割 -- SUBSTRING_INDEX
将字符串依据某个指定分隔符进行切分，并返回指定位置分隔符前的字符。(字段分割符,位置）   
```sql 
select SUBSTRING_INDEX('180,78kg',',','1') as height
select SUBSTRING_INDEX('180,78kg',',’,'2') as height
```

### 定位 -- instr
instr(substr,str)：返回substr字符串在str里第一次出现的位置，从1开始，没有返回0  
```sql 
select instr('bacd','a') == 2 
```

### 截取 -- substring
```substr（string A，int start，int len）```: 返回字符串A从下标start位置开始，长度为len的字符串    
```substring（string A，int start）```: 在不指定返回字符串长度的情况下，返回字符串A从下标start位置到结尾的字符串
```SQL
select substring(‘bacda’,2)
\\ ’acda’，代码表示返回从第2个字符起到末尾所有的字符串
```









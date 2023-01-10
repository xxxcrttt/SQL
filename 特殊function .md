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

在使用Left join 时，写在前面的表为匹配时的底表，使用on给出匹配条件，匹配条件可以不唯一。

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

### 时间差计算
```TIMESTAMPDIFF(interval, time_start, time_end)```可以计算 (time_start - time_end) 的时间差，单位以指定的 interval 为准   
通常可选: second, minute, hour, day, month, year 


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

## 窗口函数 over ([partition by <row_num>] order by <> ) 

### row_number() over partition by
函数的含义为先分组再排序    
```row_number() over (partition by col1 order by col2)```表示先根据 col1 分组，在分组内部再根据 col2 进行排序


### limit / offset 
```select _column,_column from _table [where Clause] [limit N][offset M]```
* ```limit N```: 返回 N 条记录
* ```offset M```: 跳过 M 条记录，默认 M = 0
* ```limit N,M```: 相当于 limit M offset N , 从第 N 条记录开始, 返回 M 条记录


### RANK 排序
* ```RANK()```: 在计算排序时，若存在相同位次，会跳过之后的为位次 (如：1，1，1，4...)
* ```DENSE_RANK()```: 若存在相同位次，不会跳过之后的位次 (1,1,1,2...)
* ```ROW_NUMBER()```： 赋予唯一的连续位次 (1,2,3,4.... 无论是否相同)


## 插入记录
```SQL
INSERT/REPLACE INTO table_name (column_names) VALUES 
(value1, value2,.... )
```
## 更新记录
```SQL 
UPDATE table_name 
SET tag = '', //不能使用and 分割，直接用逗号分割
WHERE tag = ''
```


## 删除记录
* 根据条件删除: 
```SQL 
DELETE FROM table_name 
[WHERE options]
[[ORDER BY fields] LIMIT n]
```
* 全部删除(清空表): ```TRUNCATE table_name ```

## 创建表单
### 1. 直接创建
```SQL 
CREATE TABLE
[IF NOT EXISTS] tb_name -- 不存在才创建，存在就跳过
(column_name1 data_type1 -- 列名和类型必选
  [ PRIMARY KEY -- 可选的约束，主键
   | FOREIGN KEY -- 外键，引用其他表的键值
   | AUTO_INCREMENT -- 自增ID
   | COMMENT comment -- 列注释（评论）
   | DEFAULT default_value -- 默认值
   | UNIQUE -- 唯一性约束，不允许两条记录该列值相同
   | NOT NULL -- 该列非空
  ], ...
) [CHARACTER SET charset] -- 字符集编码
[COLLATE collate_value] -- 列排序和比较时的规则（是否区分大小写等）
```

### 2. 从另一张表复制
```CREATE TABLE tb_name LIKE tb_name_old```

### 3. 从另一张表的查询结果创建表
```CREATE TABLE tb_name AS SELECT * FROM tb_name_old WHERE options```

### 4. 修改表: 
```SQL 
ALTER TABLE table_name 
{ ADD COLUMN <列名> <类型>  -- 增加列
 | CHANGE COLUMN <旧列名> <新列名> <新列类型> -- 修改列名或类型
 | ALTER COLUMN <列名> { SET DEFAULT <默认值> | DROP DEFAULT } -- 修改/删除 列的默认值
 | MODIFY COLUMN <列名> <类型> -- 修改列类型
 | DROP COLUMN <列名> -- 删除列
 | RENAME TO <新表名> -- 修改表名
 | CHARACTER SET <字符集名> -- 修改字符集
 | COLLATE <校对规则名> } -- 修改校对规则（比较和排序时用到）
```
```sql 
alter table 增加的表格 add 增加列的名称 数据类型 位置;
alter table 表名 change 原列名 修改列名 修改数据类型;
alter table 表明 modify 修改列名称 数据类型 默认值等;
```

### 5. 删除表
```DROP TABLE [IF EXISTS] table1 [, table2]```


## 创建索引

### 1. create 方式创建索引
```sql 
CREATE
  [UNIQUE -- 唯一索引
  | FULLTEXT -- 全文索引
  ] INDEX index_name ON table_name -- 不指定唯一或全文时默认普通索引
  (column1[(length) [DESC|ASC]] [,column2,...]) -- 可以对多列建立组合索引 
```

### 2. 
```DROP INDEX <索引名> ON <表名>```   
```ALTER TABLE <表名> DROP INDEX <索引名>```

### 3. 使用
1. 索引使用时满足最左前缀匹配原则，多以组合索引(col1, col2), 在不考虑引擎优化时，条件必须是 col1 在前 col2 在后，或者只使用col1，索引才会生效
2. 索引不包含有 NULL 的列
3. 一个查询只使用一次索引，如果where中使用了索引，order by 就不会使用
4. like 做字段比较时只有前缀确定时才会使用索引
5. 在列上进行运算后不会使用索引 


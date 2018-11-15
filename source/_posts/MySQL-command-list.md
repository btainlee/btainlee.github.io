---
title: MySQL command list
date: 2018-11-05 21:49:45
tags:
	- Mysql
	- SQL

---

![](https://ws1.sinaimg.cn/large/88370061ly1fwxishqij3j20dw08gwen.jpg)



### LOGIN Mysql

```shell
mysql -uroot -p xxxxx
```



### USE Mysql  

```mysl
SHOW DATABASES;				
USE  XXXdatabase;			
SHOW TABLES;				
SHOW COLUMNS FROM XXXtable;	
```

### Retrieving Data

```sql
SELECT xxxcolumn FROM xxxtable;		
SELECT xxxcolumn, xxxcolumn FROM xxxtable;	
SELECT * FROM xxxtable;		
SELECT DISTINCT xxxcolumn from xxxtable;	
SELECT xxxcolumn FROM xxxtable LIMIT 5;		
SELECT xxxcolumn FROM xxxtable LIMIT 5,5;	
SELECT xxxcolumn FROM xxxdatabase.xxxtable;	
```

### Retireving Data and Sort

```sql
# ORDER BY ONE COLUMN
SELECT xxxcolumn FROM xxxtable ORDER BY xxxcolumn;
SELECT xxxcolumn FROM xxxtable ORDER BY xxxcolumn ASC;
SELECT xxxcolumn FROM xxxtable ORDER BY xxxcolumn DESC;

# ORDER BY MULTI COLUMNS,first sort and group by xxxcolumn1,then sort by xxxcolumn2 in each group.
SELECT xxxcolumn FROM xxxtable ORDER BY xxxcolumn1, xxxcolumn2;
SELECT xxxcolumn FROM xxxtable ORDER BY xxxcolumn1 DESC, xxxcolumn2;

# Retireving most value
SELECT xxxcolumn FROM xxxtable ORDER BY xxxcolumn1 	LIMIT 1;
```

### Filter Data

```sql
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 = "xxx";

# | = | <> | != | < | <= | > | >= | BETWEEEN |
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 < "xxx";
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 <> "xxx";
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 BETWEEN "XX" AND "XX";

# check NULL, NUll is not "",not 0,not " ";
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn IS NULL;
```



### Filter Data2(AND,OR,IN)

```sql
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 = "xx" AND xxxcolumn2 = "xx";
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 = "xx" OR xxxcolumn2 = "xx";

# AND has higher priority level than OR
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 = "xx" OR xxxcolumn2 = "xx" AND xxxcolumn3 = "xx";

SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 IN ("xx","xx");
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 NOT IN("xx","xx");
```

### Wildcard Filter Data(LIKE)

```sql
# % (any charS)
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 LIKE "%xxx";
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn2 LIKE "xxx%";
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn3 LIKE "%xx%";

# _ (just one char)
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 LIKE "_ xx";
```

### Rebuild Information(Concat,AS)

```sql
SELECT Concat(xxxcolumn1, '(', xxxcolumn2, ')') FROM xxxtable;
SELECT Concat(RTrim(xxxcolumn), '(', xxxcolumn2, ')') FROM xxxtable;
SELECT xxxcolumn AS xxxcolumn1 FROM xxxtable;
SELECT xxxcolumn1*xxxcolumn2 AS xxxcolumn3 FROM xxxtable;
```

### Functions

```sql
#String
Left()
Length()
Locate()
Lower()
LTrim()
Right()
RTrim()
Soundex()
SubString()
Upper()

#Date
AddDate()
AddTime()
CurTime()
Date()
DateDiff()
Date_Add()
Date_Format()
Day()
DayOfWeek()
Hour()
Minute()
Month()
Now()
Second()
Time()
Year()

#Number
Abs()
Cos()
Exp()
Mod()
Pi()
Rand()
Sin()
Sqrt()
Tan()
```

### Statistical Functions

```sql
AVG()
COUNT()
MAX()
MIN()
SUM()
```

### Group Data(GROUP BY, HAVING)

```sql
SELECT xxxcolumn,COUNT(*) AS xxxcolumn1 FROM xxxtable GROUP BY xxxcolumn;
SELECT xxxcolumn,COUNT(*) AS xxxcolumn1 FROM xxxtable GROUP BY xxxcolumn HAVING COUNT(*) > 2;
SELECT xxxcolumn,COUNT(*) AS xxxcolumn1 FROM xxxtable GROUP BY xxxcolumn HAVING COUNT(*) > 2 ORDER BY xxxcolumn DESC;

# SELECT -> FROM -> WHERE -> GROUP BY -> HAVING -> ORDER BY -> LIMIT;
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn1 = "xx" GROUP BY xxxcolumn2 HAVING COUNT(*)> 2 ORDER BY xxxcolumn3 DESC LIMIT 1;
```

### SubQuery

```sql
#AS Condition
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn2 IN(SELECT xxxcolumn2 FROM xxxtable2 WHERE xxxcolumn3 = 'xxx');

#As column
SELECT xxxcolumn1,xxxcolumn2,(SELECT COUNT(*) FROM xxxtable2 where xxxcolumn4 = xxxcolumn5 AS count) FROM xxxtable1 ORDER BY  xxxcolumn3;
```

### Join(foreign key)

```sql
SELECT xxxcolumn1,xxxcolumb2,xxxcolumn3 FROM xxxtable1,xxxtable2 WHERE xxxtable1.xxxcolumn1 = xxxtable2.xxxcolumn2;


# Cartesian product: the number of result is equal to lines of table1 times lines of table2.
SELECT xxxcolumn1, xxxcolumn2,xxxcolumn3 FROM xxxtable1,xxxtable2 ORDER BY xxxcolumn;

#Inner join(same result as where condition)
SELECT xxxcolumn1,xxxcolumn2,xxxcolumn3 FROM xxxtable INNER JOIN xxxtable2 ON xxxtable1.xxxcolumn1 = xxxtable2.xxxcolumn2;

#multi table
SELECT xxxcolumn1,xxxcolumn2,xxxcolumn3,xxxcolumn4 FROM xxxtable1,xxxtable2,xxxtable3 WHERE xxxtable1.xxxcolumn1 = xxxtable2.xxxcolumn2 AND xxxtable1.xxxcolumn2 = xxxtable3.xxxcolumn1;

```

### Advance Join

```sql
#AS(easier,use same table name in one SELECT sql more than one time)

#Join self
SELECT xxxcolumn1,xxxcolumn2 FROM xxxtable WHERE xxxcolumn = (SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn = 'xxx');
SELECT p1.xxxcolumn,p1.xxxcolumn2 FROM xxxtable AS p1,xxxtable AS p2 WHERE p1.xxxcolumn1 = p2.xxxcolumn AND p2.xxxcolumn2 = 'xxx';

#OUTER JOIN
SELECT xxxtable.xxxcolumn1,xxxtable.xxxcolumn2 FROM xxxtable1 LEFT OUTER JOIN xxxtable2 ON xxxtable1.xxxcolumn1 = xxxtable2.xxxcolumn2;
[
    xxxtable1		xxxtable2
    1				a
    1				b
    2				null
    
    3				c
    3				d
    4				null
    
    xxxtable1 LEFT OUTER JOIN xxxtable2:
    1a 1b
    2
    3c
    3d
    4
    
    xxxtable1 RIGHT OUTER JOIN xxxtable2:
    a1 b1 c3 d3
]
```

### UNION

```sql
#auto delete same line
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn < x UNION SELECT xxxcolumn FROM xxxtable2 WHERE xxxcolumn ='xx';

# show all line
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn < x UNION ALL SELECT xxxcolumn FROM xxxtable2 WHERE xxxcolumn ='xx';

#order
SELECT xxxcolumn FROM xxxtable WHERE xxxcolumn < x UNION ALL SELECT xxxcolumn FROM xxxtable2 WHERE xxxcolumn ='xx' ORDER BY xxxcolumn;
```


## 创建表

### 	1.数据类型

`INT`

`CHAR(N)`

`VARCHAR(N)`

`DATE`

`TIME`

`FLOAT(N)`

### 	2.列级完整性约束

`PRIMARY KEY`

`NOT NULL` 

`UNIQUE`

`CHECK(条件)`

### 3.表级完整性约束

PRIMARY KEY(列名1, 列名n)	//实体完整性

FOREIGN KEY(列名1)  REFERENCES 被参照表(列名1)	//参照完整性

```sql
CREATE TABLE TAB1
( Sno VARCHAR(10),
Cno NUMBER(10),
Grade INT NOT NULL,
PRIMARY KEY(Sno, Cno),
FOREIGN KEY(Sno) REFERENCES TAB2(Sno)
);
```



## 聚集函数

`COUNT`

`AVG`

`SUM`

`MAX/MIN`

```sql
SELECT name,sex
FROM TAB
WHERE age NOT BETWEEN 20 AND 30;
```



## 字符匹配

`%`表示任意长度（可以为0）的字符串。如a%b，表示以a开头，b结尾的任意长度字符串

`_`表示单个字符

注意：在ASCII码表中，一个汉字的长度为`2`

```sql
select Sname,Sno,Ssex
from Student
where Sname like '刘_ _ _ _';
```

添加转义字符

```sql
SELECT Cno
FROM SC
WHERE Cname LIKE 'DB\_Design' ESCAPE '\';
WHERE 列名 NOT LIKE '字符串' ESCAPE '\';
```



## Group by // having //order by

`group by 列名 having 筛选条件`

```sql
SELECT Sno, Grade
FROM SC
GROUP BY Sno
HAVING AVG(Grade)>=90; 
```

`order by 次序`

```sql
SELECT Sno, Grade
FROM SC
WHERE Cno='3'
ORDER BY Grade DESC;
-- ASC 为升序
-- DESC 为降序
```



## 连接查询

`where 表名1.列名1 比较运算符 表名2.列名2;`

```sql
SELECT Student.*, SC.* //若两个表中有相同名的属性列，自然连接
FROM Student, SC
WHERE Student.Sno = SC.Sno; //用sno作为连接字段，将两个表连接在一起
```

AND用作多重条件

```sql
SELECT Student.Sno, Sname 
FROM Student, SC 
WHERE Student.Sno=SC.Sno AND SC.Cno='2' AND SC.Grade>90;
```

单表连接查询

在Course表中查询先修课的先修课，其中课程号为`Cno`，先修课程号为`Cpno`

```sql
SELECT FIRST.Cno, SECOND.Cpno
FROM Course FIRST, Course SECOND
WHERE FIRST.Cpno=SECOND.Cno;
```

左外连接

```sql
from 表名1 left outer join 表名2 on(连接条件); //on可换using,去掉结果中的重复值
```

右外连接

```sql
from 表名1 right outer join 表名2 on(连接条件); //on可换using,去掉结果中的重复值
```

多表查询

```sql
SELECT Student.Sno, Sname, Cname, Grade
FROM Student, SC, Course
WHERE Student.Sno=SC.Sno AND SC.Cno=Course.Cno;
```

## 嵌套查询

查询块：`SELECT-FROM-WHERE`

### in-子查询

查找与刘晨同一个专业的同学

```sql
SELECT Sdept
FROM Student
WHERE Sname='刘晨';
```

查找在CS专业的同学

```sql
SELECT Sno, Sname, Sdept
FROM Student
WHERE Sdept='CS';
```

两者合并

```sql
SELECT Sno, Sname, Sdept
FROM Student
WHERE Sdept IN
(SELECT Sdept
FROM Student
WHERE Sname='刘晨'); //本例的子查询条件不依赖于父查询，这类子查询称为不相关子查询
```

在`SC`表中找出每个学生`Sno`超过他自己选修课程平均成绩`Grade`的课程号`Cno`

```sql
SELECT Sno, Cno
FROM SC x
WHERE Grade >= 
(SELECT AVG(Grade)
FROM SC y 
WHERE y.Sno=x.Sno); //本例的子查询条件依赖于父查询，这类子查询称为相关子查询,整个查询称为相关嵌套查询
```

exists-子查询

建立量词，离散数学

不存在这样的课程y,学生1号选修了y，而学生x没有选

```sql
SELECT DISTINCT Sno
FROM SC SCX
WEHRE NOT EXISTS
(SELECT *
FROM SC SCY
WHERE SCY.Sno='1' AND NOT EXISTS
(SELECT *
 FROM SC SCZ
 WHERE SCZ.Sno=SCX.Sno AND SCZ.Cno=SCY.Cno)
);
```

基于SC表，查询选修了全部课程（Course表）的学生姓名（Student表）

查询没有任何课程是其不选修的学生y

```sql
SELECT Sname
FROM Student
WHERE NOT EXISTS
(SELECT *
FROM Course
WHERE NOT EXISTS
(SELECT *
FROM SC
WHERE Sno=Student.Sno AND Cno=Course.Cno)
)
```

## INSERT / UPDATE / DELETE

### INSERT

```sql
INSERT
INTO 表名(列名1，列名n)
VALUES(常亮1,常亮n);
```

### UPDATE

```sql
UPDATE TAB1
SET C4='0'
WHERE C1=1;
```

```sql
UPDATE TAB1
SET C3=C3+1;
```

```sql
UPDATE TAB1
SET C4='0'
WHERE C1 IN
(SELECT C1
FROM TAB2
WHERE avg_C2=2;
```

### DELETE

```sql
DELETE
FROM TAB1
WHERE C1=1;
```

带子查询的删除语句

```sql
DELETE
FROM TAB1
WHERE C1 IN
(SELECT C1
FROM TAB2
WHERE avg_C2=2;
```

## 视图VIEW

```sql
CREATE VIEW 视图
AS 子查询
WITH CHECK OPTION; //若添加该句，则表示对视图进行增删查改时要满足子查询中的条件表达式
```

建立TAB1的视图

```sql
CREATE VIEW V_TAB1
AS
SELECT C1, C2, C3, C4
FROM TAB1
WHERE C1=1;
```

建立C4为4时，TAB1的视图，并保证以后每次增删改时都要满足C4为4的条件

```sql
CREATE VIEW V_TAB2
AS
SELECT C1, C2, C3, C4
FROM TAB1
WHERE C4='4'
WITH CHECK OPTION;
```


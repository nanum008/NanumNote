# MySql数据库笔记

## 一、常用命令

### 1. 登录MySql数据库`root`账户

---

1.1 命令

```mysql
mysql -h主机IP/域名 -uroot -proot账户的密码
```

1.2 示例

```sql
C:\Users\null'pointer>mysql -h127.0.0.1 -uroot -p123456
mysql: [Warning] Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.7.14-log MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```



1.3 注意

- 若登录的是本机的MySql数据库可省略主机IP参数；

  ```sql
  mysql -uroot -p密码
  ```

  

- 若不想让密码明文显示在doc命令窗口上可在输入`-p`之后回车再输入密码，此时密码就会以`*`的形式显示在屏幕上,达到保密的效果；

  

### 2. 查看已有的数据库

---

2.1 命令 

```sql
show databases;
```

2.2 示例

```sql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sakila             |
| sys                |
| test               |
| world              |
+--------------------+
7 rows in set (0.00 sec)
```



### 3. 使用数据库

---

3.1 命令

```sql
use 数据库名;
```

3.2 示例

```sql
mysql> use test;
Database changed
```



### 4. 查看当前使用的数据库

---

4.1 命令

```sql
select database();
```

4.2 示例

```sql
mysql> select database();
+------------+
| database() |
+------------+
| test       |
+------------+
1 row in set (0.00 sec)
```



### 5. 查看当前数据库中有哪些表

---

5.1 命令

```sql
show tables;
```

5.2 示例

```sql
mysql> show tables;
+----------------+
| Tables_in_test |
+----------------+
| dept           |
| emp            |
| salgrade       |
+----------------+
3 rows in set (0.00 sec)
```



### 6. 查看其他数据库中有哪些表

---

6.1 命令

```sql
show tables from 数据库名;
```

6.2 示例

```sql
mysql> show tables from world;
+-----------------+
| Tables_in_world |
+-----------------+
| city            |
| country         |
| countrylanguage |
+-----------------+
3 rows in set (0.00 sec)
```





### 7. 查看表的结构

---

7.1 命令

```sql
desc 表名;
```

7.2 示例

```sql
mysql> desc emp;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| EMPNO    | int(4)      | NO   | PRI | NULL    |       |
| ENAME    | varchar(10) | YES  |     | NULL    |       |
| JOB      | varchar(9)  | YES  |     | NULL    |       |
| MGR      | int(4)      | YES  |     | NULL    |       |
| HIREDATE | date        | YES  |     | NULL    |       |
| SAL      | double(7,2) | YES  |     | NULL    |       |
| COMM     | double(7,2) | YES  |     | NULL    |       |
| DEPTNO   | int(2)      | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
8 rows in set (0.00 sec)
```



### 8. 查看创建表的语句

---

8.1 命令

```sql
show create table 表名;
```

8.2 示例

```sql
mysql> show create table emp;
+-------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                                                                                                                                                                                        |
+-------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| emp   | CREATE TABLE `emp` (
  `EMPNO` int(4) NOT NULL,
  `ENAME` varchar(10) DEFAULT NULL,
  `JOB` varchar(9) DEFAULT NULL,
  `MGR` int(4) DEFAULT NULL,
  `HIREDATE` date DEFAULT NULL,
  `SAL` double(7,2) DEFAULT NULL,
  `COMM` double(7,2) DEFAULT NULL,
  `DEPTNO` int(2) DEFAULT NULL,
  PRIMARY KEY (`EMPNO`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 |
+-------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```





### 9. 查看MySql的版本号

---

9.1 命令

```sql
select version();
```

9.2 示例

```sql
mysql> select version();
+------------+
| version()  |
+------------+
| 5.7.14-log |
+------------+
1 row in set (0.00 sec)
```





### 10. 结束一条sql语句

---

10.1 命令

```sql
\c
```

10.2 示例

```sql
mysql> show create table emp
    -> \c
mysql>
```





### 11. 退出MySql数据库

---

11.1 命令

```sql
exit
```

11.2 示例

```sql
mysql> exit
Bye
```



## 二、DQL(数据查询语言)

### 简单的查询语句

---

#### 查询一个字段

---

语法

```sql
select 字段 from 表名;
```

****示例****

```sql
mysql> select ename from emp;
+--------+
| ename  |
+--------+
| SMITH  |
| ALLEN  |
| WARD   |
| JONES  |
| MARTIN |
| BLAKE  |
| CLARK  |
| SCOTT  |
| KING   |
| TURNER |
| ADAMS  |
| JAMES  |
| FORD   |
| MILLER |
+--------+
15 rows in set (0.00 sec)
```





#### 查询多个字段

---

语法

```sql
select 字段1，字段2，字段3，…… from 表名;
```

示例

```sql
mysql> select ename,sal,job from emp;
+--------+---------+-----------+
| ename  | sal     | job       |
+--------+---------+-----------+
| SMITH  |  800.00 | CLERK     |
| ALLEN  | 1600.00 | SALESMAN  |
| WARD   | 1250.00 | SALESMAN  |
| JONES  | 2975.00 | MANAGER   |
| MARTIN | 1250.00 | SALESMAN  |
| BLAKE  | 2850.00 | MANAGER   |
| CLARK  | 2450.00 | MANAGER   |
| SCOTT  | 3000.00 | ANALYST   |
| KING   | 5000.00 | PRESIDENT |
| TURNER | 1500.00 | SALESMAN  |
| ADAMS  | 1100.00 | CLERK     |
| JAMES  |  950.00 | CLERK     |
| FORD   | 3000.00 | ANALYST   |
| MILLER | 1300.00 | CLERK     |
+--------+---------+-----------+
15 rows in set (0.00 sec)
```



#### 查询全部字段

---

语法

```sql
select * from 表名;
```

ps:`*`表示查询所有字段，在实际开发当中不建议使用，因为效率较低;



示例

```sql
mysql> select * from emp;
+-------+--------+-----------+------+------------+---------+---------+--------+
| EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
+-------+--------+-----------+------+------------+---------+---------+--------+
|  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
|  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
|  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
|  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
|  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
|  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
|  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
|  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
|  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
|  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
|  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
|  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
|  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
|  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
+-------+--------+-----------+------+------------+---------+---------+--------+
15 rows in set (0.00 sec)
```



#### 对查询出的字段重命名

---

语法

```sql
select 字段 as 重命名后的字段 from 表名; 
```

示例

```sql
mysql> select ename as 'name',sal as "薪资" from emp;
+--------+---------+
| name   | 薪资    |
+--------+---------+
| SMITH  |  800.00 |
| ALLEN  | 1600.00 |
| WARD   | 1250.00 |
| JONES  | 2975.00 |
| MARTIN | 1250.00 |
| BLAKE  | 2850.00 |
| CLARK  | 2450.00 |
| SCOTT  | 3000.00 |
| KING   | 5000.00 |
| TURNER | 1500.00 |
| ADAMS  | 1100.00 |
| JAMES  |  950.00 |
| FORD   | 3000.00 |
| MILLER | 1300.00 |
+--------+---------+
15 rows in set (0.00 sec)
```

ps：

- 重命名的字段如果是`中文`需要用`单引号`或者`双引号`括起来；

- 用引号括起来字符的表示这是一个字符串；
- 标准的sql语句中字符串**必须使用单引号括起来**；
- 起别名的时候`as`关键字可以省略；

​		

#### 对查询出的数值字段进行数学运算

---

语法：

```sql
select 数值字段 运算符 运算值 from 表名;
```

示例：

```sql
mysql> select ename,sal * 12 as '年薪' from emp;
```



### 条件查询

---

条件查询需要使用`where`关键字，where必须放在from关键字的后面；

条件查询支持的运算符如下：

|     运算符     |                      说明                      |
| :------------: | :--------------------------------------------: |
|       =        |                      等于                      |
|     <>&!=      |                     不等于                     |
|       <        |                      小于                      |
|       >        |                      大于                      |
|       >=       |                    大于等于                    |
|       <=       |                    小于等于                    |
| between……and…… |        在两个值之间，等同于`>= and <=`         |
|    is null     |         是否为`null`,is not null不为空         |
|      and       |                      并且                      |
|       or       |                      或者                      |
|       in       |              包含，相当于多个`or`              |
|      not       | not用于取非，主要用在`is not null`或`not in`中 |
|      like      |      `like`成为模糊查询，支持`%`或`_`匹配      |



基本语法：

```sql
select 字段1,字段2,…… from 表名 where 条件;
```



#### 运算符：`=`、`>`、`>=`、`<`、`<=`

---

示例

```sql
#示例1：查询工资等于5000的员工；
mysql> select ename,job from emp where sal = 5000;

#示例2：查询SMITH的职位和工资；
mysql> select job,sal from emp where ename = 'SMITH';

#示例3：查询工资大于等于3000的员工；
mysql> select ename,job,sal from emp where sal >= 3000;
```



#### 运算符：`<>`&`!=`

---

示例

```sql
#示例1：找出工资不等于3000的员工
mysql> select ename,sal from emp where sal <> 3000;
```



#### 运算符：`between …… and ……`

---

示例

```sql
#找出薪资在2000到3000之间的员工；
mysql> select ename,job,sal from emp where sal between 2000 and 3000;
```

注意

1. between ……and……相当于>= and <=,类似于数学当中的闭区间(`[]`)；
2. `and`左边的数必须小于右边的数！
3. 该运算符可以运用在字符方面(几乎用不到)



#### 运算符：`is null`&`is not null`

---

- 在数据库当中，`NULL`不是一个值，代表什么也没有，为`空`；

- `空`不是一个值，不能用等号衡量！！！

- 必须使用`is null`或者`is not null`;



示例

```sql
#找出那些人津贴不为NULL；
mysql> select ename,sal,comm  from emp where comm is not null;
+--------+---------+---------+
| ename  | sal     | comm    |
+--------+---------+---------+
| ALLEN  | 1600.00 |  300.00 |
| WARD   | 1250.00 |  500.00 |
| MARTIN | 1250.00 | 1400.00 |
| TURNER | 1500.00 |    0.00 |
+--------+---------+---------+
4 rows in set (0.00 sec)
```

注意：`NULL`在数据库当中不是一个值，所以不能用`=`、`!=`运算符进行比较，只能使用`is null`&`is not null`；



#### 运算符：`and`&`or`

---

`and`和`or`分开使用

```sql
#示例1：找出工资在1000到3000之间的员工；
mysql> select ename,sal from emp where sal >=1000 and sal <=3000;
+--------+---------+
| ename  | sal     |
+--------+---------+
| ALLEN  | 1600.00 |
| WARD   | 1250.00 |
| JONES  | 2975.00 |
| MARTIN | 1250.00 |
| BLAKE  | 2850.00 |
| CLARK  | 2450.00 |
| SCOTT  | 3000.00 |
| TURNER | 1500.00 |
| ADAMS  | 1100.00 |
| FORD   | 3000.00 |
| MILLER | 1300.00 |
+--------+---------+
12 rows in set (0.00 sec)

#示例2：找出那些员工没有津贴；
mysql> select ename,comm from emp where comm is null or comm = 0;
+--------+------+
| ename  | comm |
+--------+------+
| 张三   | NULL |
| SMITH  | NULL |
| JONES  | NULL |
| BLAKE  | NULL |
| CLARK  | NULL |
| SCOTT  | NULL |
| KING   | NULL |
| TURNER | 0.00 |
| ADAMS  | NULL |
| JAMES  | NULL |
| FORD   | NULL |
| MILLER | NULL |
+--------+------+
12 rows in set (0.01 sec)
```



`and`与`or`联合使用

```sql
#示例：找出工资大于1000并且部门编号是20或30的员工；
mysql> select ename,sal,deptno from emp where sal >1000 and deptno =20 or deptno = 30;
+--------+---------+--------+
| ename  | sal     | deptno |
+--------+---------+--------+
| ALLEN  | 1600.00 |     30 |
| WARD   | 1250.00 |     30 |
| JONES  | 2975.00 |     20 |
| MARTIN | 1250.00 |     30 |
| BLAKE  | 2850.00 |     30 |
| SCOTT  | 3000.00 |     20 |
| TURNER | 1500.00 |     30 |
| ADAMS  | 1100.00 |     20 |
| JAMES  |  950.00 |     30 |
| FORD   | 3000.00 |     20 |
+--------+---------+--------+
10 rows in set (0.00 sec)
#可以看到员工`JAMES`的工资小于1000，部门编号是30，但是出现在了查询结果集里了，没有达到预期的要求；
#这是因为`and`的优先级要高于`or`，所以`sal >100 and deptno =20`先配对执行了，然后再执行的`or`语句；
#我们可以通过对or语句加`()`的方式来提升其优先级：
mysql> select ename,sal,deptno from emp where sal >1000 and (deptno =20 or deptno = 30);
+--------+---------+--------+
| ename  | sal     | deptno |
+--------+---------+--------+
| ALLEN  | 1600.00 |     30 |
| WARD   | 1250.00 |     30 |
| JONES  | 2975.00 |     20 |
| MARTIN | 1250.00 |     30 |
| BLAKE  | 2850.00 |     30 |
| SCOTT  | 3000.00 |     20 |
| TURNER | 1500.00 |     30 |
| ADAMS  | 1100.00 |     20 |
| FORD   | 3000.00 |     20 |
+--------+---------+--------+
9 rows in set (0.00 sec)
#这样括号里的or语句就先执行了，查询结果符合我们的要求；
```



注意：当运算符的优先级不确定的时候可以加`()`来提升其优先级；



#### 运算符：`in`&`not in`

---

运算符`in`等同于`or`是`在这几个值当中的意思`，在执行效率上和`or`没有区别；

```sql
#示例：找出工作岗位是MANAGER或SALESMAN的员工；
#方式1
mysql> select ename,job from emp where job = 'salesman' or job = 'manager';
+--------+----------+
| ename  | job      |
+--------+----------+
| ALLEN  | SALESMAN |
| WARD   | SALESMAN |
| JONES  | MANAGER  |
| MARTIN | SALESMAN |
| BLAKE  | MANAGER  |
| CLARK  | MANAGER  |
| TURNER | SALESMAN |
+--------+----------+
7 rows in set (0.00 sec)
#方式2
mysql> select ename,job from emp where job in ('salesman','manager');
+--------+----------+
| ename  | job      |
+--------+----------+
| ALLEN  | SALESMAN |
| WARD   | SALESMAN |
| JONES  | MANAGER  |
| MARTIN | SALESMAN |
| BLAKE  | MANAGER  |
| CLARK  | MANAGER  |
| TURNER | SALESMAN |
+--------+----------+
7 rows in set (0.00 sec)
#可以发现二者查询的结果一模一样
```

注意：`字段 in (1000,2000)`并不等同于`字段 >= 1000 and 字段 <= 2000 `，而是等同于`字段 = 1000 or 字段 = 2000`；

​			**括号里的值不是代表一个区间，注意区分**；



`not in`：不在这几个值当中；

```sql
#示例：找出工作岗位不是MANAGER或SALESMAN的员工；
mysql> select ename,job from emp where job not in ('manager','salesman');
+--------+-----------+
| ename  | job       |
+--------+-----------+
| SMITH  | CLERK     |
| SCOTT  | ANALYST   |
| KING   | PRESIDENT |
| ADAMS  | CLERK     |
| JAMES  | CLERK     |
| FORD   | ANALYST   |
| MILLER | CLERK     |
+--------+-----------+
8 rows in set (0.00 sec)
```



#### 模糊查询`like`

---

- `like`用于模糊查询，比如需求`找出姓李的员工`就需要使用到`like`关键字；
- 模糊查询时`_`代表一个字符，`%`代表多个字符；
- 如有特殊需求，可以在`_` `%`前面加反斜杠对其进行转义；



示例

```sql
#示例：找出名字中第二个字母是'a'的员工；
mysql> select ename from emp where ename like '_a%';
+--------+
| ename  |
+--------+
| WARD   |
| MARTIN |
| JAMES  |
+--------+
3 rows in set (0.01 sec)
```





## 三、注意事项

1. 每一条SQL语句都是以`;`结束的，不见`;`，sql语句是不会执行的；

2. 字母不区分大小写；

3. 在MySql当中，字符串用单引号或者双引号括起来都可以，但是在Oracle、Sql Server等数据库当中只能使用单引号；

   尽管在MySql数据库当中可以使用双引号，但是为了保证sql语句的通用性，建议字符串都使用单引号括起来；


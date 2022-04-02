# 数据库笔记

# 第一章：MySQL数据库常用命令

**提醒：**以下命令独属于MySQL数据库，不具备通用性，其他数据库不适用！！！！！！！！！

## 1. 登录MySql数据库(`root`账户)

- **语法格式**

```mysql
mysql -h主机IP/域名 -uroot -proot账户的密码
```

- **示例**

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

见到上面的欢迎界面就说明登录成功了，欢迎界面主要描述了如下的信息：

-  每行sql命令以`;`或`\g`结束；
- `Your MySQL connection id is 5`：你的MySQL连接次数是5，也就是说你到目前为止连接了MySQL5次，每连接一次，记录就会增加一次；
- `Server version: 5.7.14-log MySQL Community Server (GPL)`：你的MySQL版本是社区版5.7.14；
- 接下来是版权所有：Oracle，MySQ现在是Oracle公司的产品；
- 通过命令`help`或者`\h`来查看关于MySQL数据库的命令；
- 通过命令`\c`来结束当前输入的的操作(命令)；



- **注意事项**

  - 1、若登录的是本机的MySql数据库可省略主机IP参数（-h……）；

    ```sql
    mysql -uroot -p密码
    ```

  - 2、若不想让密码明文显示在doc命令窗口上可在输入`-p`之后回车再输入密码，此时密码就会以`*`的形式显示在屏幕上,达到保密的效果；

    ```sql
    mysql -uroot -p
    ```

    

  

## 2. 查看已有的数据库

**语法格式**

```sql
show databases;
```

**示例**

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
```



## 3. 使用数据库

**语法格式**

```sql
use 数据库名;
```

**示例**

```sql
mysql> use test;
Database changed
```



## 4. 查看当前使用的数据库

**语法格式**

```sql
select database();
```

**示例**

```sql
mysql> select database();
+------------+
| database() |
+------------+
| test       |
+------------+
1 row in set (0.00 sec)
```



## 5. 查看当前数据库中有哪些表

**语法格式**

```sql
show tables;
```

**示例**

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



## 6. 查看其他数据库中有哪些表

- **语法格式**

  ```sql
  show tables from 数据库名;
  ```

- **示例**

  ```sql
  mysql> show tables from world;
  +-----------------+
  | Tables_in_world |
  +-----------------+
  | city            |
  | country         |
  | countrylanguage |
  +-----------------+
  ```



## 7. 查看表的结构

- **语法格式**

```sql
desc 表名;
```

- **示例**

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
```



## 8. 查看创建表的语句

- **语法格式**
```sql
show create table 表名;
```

- **示例**

```sql
mysql> show create table emp;
+-------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table | Create Table                                                                                                                                                                                                                                                                                                                                 |
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
```

可以发现结果以表格的形式输出，由于窗口太小，显示得非常混乱，可以加上参数`\G`来美化一下：

```sql
mysql> show create table emp \G
*************************** 1. row ***************************
       Table: emp
Create Table: CREATE TABLE `emp` (
  `EMPNO` int NOT NULL,
  `ENAME` varchar(10) DEFAULT NULL,
  `JOB` varchar(9) DEFAULT NULL,
  `MGR` int DEFAULT NULL,
  `HIREDATE` date DEFAULT NULL,
  `SAL` double(7,2) DEFAULT NULL,
  `COMM` double(7,2) DEFAULT NULL,
  `DEPTNO` int DEFAULT NULL,
  PRIMARY KEY (`EMPNO`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
1 row in set (0.00 sec)
```

注意加上`\G`之后结尾**没有分号**，加上分为会报错；

## 9. 查看MySQL的版本号

- **语法格式**

```sql
select version();
```

## 10. 结束（取消执行）一条语句

- **语法格式**

  ```sql
  命令一：\c
  命令二：clear
  ```



## 11. 退出MySql数据库

- **语法格式**

  ```sql
  exit
  ```


- **示例**

```sql
mysql> exit
Bye
```



## 12. 创建数据库

- **语法格式**

  ```sql
  create database 数据库名;
  ```



## 13. 执行SQL脚本文件

> sql脚本文件当中的数据量太大的话可以使用`source`命令来初始化数据库；
>
> 注意：在执行该命令之前需要创建并选中数据库（use database）；

- **语法格式**

  ```sql
  source  sql脚本文件路径;
  ```

  

- **示例**

  ```sql
  source D:/oa.sql 
  ```



## 14. 强制退出命令

> 当前SQL语句出现错误而又不想它执行时，组合键`ctrl+C`可以强制退出当前操作；



# 第二章：DQL(数据查询语言)

> DQL（Data Query language）数据查询语言，主要用于从数据库表里查数据，使用`SELECT`命令；
>
> 在所有的SQL语句当中`SELECT`查询语句最复杂，最重要；

## 1、 简单查询

### 1）查询一个字段

- **语法**

  ```sql
  select 字段 from 表名;
  ```

- **示例**

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

  

### 2）查询多个字段

- **语法**

  ```sql
  select 字段1，字段2，字段3，…… from 表名;
  ```

- **示例**

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



### 3）查询所有字段

- **语法格式**

  ```sql
  select * from 表名;
  ```

- **注意**

  通配符：`*`表示查询所有字段，在实际开发当中不建议使用，因为效率较低;

- **示例**

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



### 对查询出的字段重命名

---

- **语法**

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

### 对查询出的数值字段进行数学运算

---

语法：

```sql
select 数值字段 运算符 运算值 from 表名;
```

示例：

```sql
mysql> select ename,sal * 12 as '年薪' from emp;
```



## 2、条件查询

> 条件查询使用`where`关键字，where必须放在`from`关键字的后面；

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



- **基本语法**

  ```sql
  select 字段1,字段2,…… from 表名 where 过滤条件;
  ```



### 运算符：`=`、`>`、`>=`、`<`、`<=`

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



### 运算符：`<>`&`!=`

---

示例

```sql
#示例1：找出工资不等于3000的员工
mysql> select ename,sal from emp where sal <> 3000;
```



### 运算符：`between …… and ……`

---

示例

```sql
#找出薪资在2000到3000之间的员工；
mysql> select ename,job,sal from emp where sal between 2000 and 3000;
```

注意

1. between ……and……相当于>= and <=,类似于数学当中的闭区间(`[]`)；
2. `and`左边的数必须小于右边的数！
3. 该运算符可以运算字符串(几乎用不到)



### 运算符：`is null`&`is not null`

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



### 运算符：`and`&`or`

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



### 运算符：`in`&`not in`

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



### 模糊查询`like`

---

- `like`用于模糊查询，比如需求`找出姓李的员工`就需要使用到`like`关键字；
- 模糊查询时`_`代表一个字符，`%`代表多个字符；
- 如有特殊需求，可以在`_` 、`%`前面加反斜杠对其进行转义；



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





## 3、分页查询（limit）

> 1、不通用，limit是**MySQL中特有的**，Oracle中有一个类似的机制：rownum；
>
> 2、作用：选取结果集中的**部分数据**；
>
> 3、limit在`SELECT`语句中是最后执行的；

- **语法**

  ```sql
  limit startIndex , length;
  ```

  startIndex：起始位置；

  length：长度，取几个；

  



## 3、数据排序

当数据被我们从数据库查出来后我们可以再对其进行排序，排序使用的是`order by`命令；

**升序排列**

示例

```sql
#示例：展出员工的薪资和名字，并且按照员工的工资升序排序；
#方式1：使用`order by`关键字，默认是升序排列；
mysql> select ename,sal from emp order by sal;
#方式2：添加`asc`关键字，asc代表升序排列；
mysql> select ename,sal from emp order by sal asc;

#结果
+--------+---------+
| ename  | sal     |
+--------+---------+
| SMITH  |  800.00 |
| JAMES  |  950.00 |
| ADAMS  | 1100.00 |
| WARD   | 1250.00 |
| MARTIN | 1250.00 |
| MILLER | 1300.00 |
| TURNER | 1500.00 |
| ALLEN  | 1600.00 |
| CLARK  | 2450.00 |
| BLAKE  | 2850.00 |
| JONES  | 2975.00 |
| SCOTT  | 3000.00 |
| FORD   | 3000.00 |
| KING   | 5000.00 |
+--------+---------+
```



**降序排列**

示例

```sql
#使用`desc`关键字指定降序排列；
#示例：找出员工名字和其工资，按照工资的降序排列；
mysql> select ename,sal from emp order by sal desc;
+--------+---------+
| ename  | sal     |
+--------+---------+
| SCOTT  | 3000.00 |
| FORD   | 3000.00 |
| JONES  | 2975.00 |
| BLAKE  | 2850.00 |
| CLARK  | 2450.00 |
| ALLEN  | 1600.00 |
| TURNER | 1500.00 |
| MILLER | 1300.00 |
| WARD   | 1250.00 |
| MARTIN | 1250.00 |
| ADAMS  | 1100.00 |
| JAMES  |  950.00 |
| SMITH  |  800.00 |
+--------+---------+
```



### 1）多字段排序

---

> 多个字段参与排序，`order by`关键字后越靠前的字段优先级越高；

示例

```sql
#多个字段参与排序，`order by`关键字后越靠前的字段优先级越高；
#示例：找出员工的名字和工资，按照员工的工资降序排列，工资相同的员工按照名字升序排列；
mysql> select ename,sal from emp order by sal desc,ename asc;
+--------+---------+
| ename  | sal     |
+--------+---------+
| KING   | 5000.00 |
| FORD   | 3000.00 |
| SCOTT  | 3000.00 |
| JONES  | 2975.00 |
| BLAKE  | 2850.00 |
| CLARK  | 2450.00 |
| ALLEN  | 1600.00 |
| TURNER | 1500.00 |
| MILLER | 1300.00 |
| MARTIN | 1250.00 |
| WARD   | 1250.00 |
| ADAMS  | 1100.00 |
| JAMES  |  950.00 |
| SMITH  |  800.00 |
```



### **2）按照查询出的字段的顺序排列**

---

示例

```sql
#关键字`oeder by`后面可以指定具体的字段，也可以写查询出的字段的顺序；
#示例：找出员工的名字和工资，按照员工的工资降序排列；
mysql> select ename,sal from emp order by 2 desc;
+--------+---------+
| ename  | sal     |
+--------+---------+
| KING   | 5000.00 |
| SCOTT  | 3000.00 |
| FORD   | 3000.00 |
| JONES  | 2975.00 |
| BLAKE  | 2850.00 |
| CLARK  | 2450.00 |
| ALLEN  | 1600.00 |
| TURNER | 1500.00 |
| MILLER | 1300.00 |
| WARD   | 1250.00 |
| MARTIN | 1250.00 |
| ADAMS  | 1100.00 |
| JAMES  |  950.00 |
| SMITH  |  800.00 |
+--------+---------+
#sal语句当中`2`代表的就是要查询的字段`ename,sal`当中的第二个字段(sal)；
#不建议在实际开发当中使用；
```



## 4、数据去重

---

> 当我们不希望看到有重复的数据的时候我们就可以使用`distinct`命令来去除重复的记录；

**语法格式**

```sql
select distinct	字段1,字段2,…… from table_name;
```

**注意**

`distinct`只能出现在所有字段的最前面，表示后面所有的字段联合起来去重；以下SQL是错误的：

```sql
select name,distinct job from emp;
```

**示例**

统计岗位的数量：

```sql
select count( ditsinct job )	from emp;
1、没有添加group by 关键字，这张表所有的记录算作一组；
2、先对重复的字段去重，然后在再使用分组函数【多行处理函数】：count()函数统计记录条数；
```





## 5、分组查询&having过滤

> 我们可以使用`group by`将字段值相同的记录分为一组，结合分组函数查询；



**单个字段分组查询**

```sql
#查询各个部门的最高薪资；
mysql> select deptno,max(sal) from emp group by deptno order by deptno;
+--------+----------+
| deptno | max(sal) |
+--------+----------+
|     10 |  5000.00 |
|     20 |  3000.00 |
|     30 |  2850.00 |
+--------+----------+ 


```



**多个字段分组查询**

```sql
#找出每个部门不同工作岗位的最高薪资
mysql> select deptno,job,max(sal) from emp group by deptno,job order by deptno;
+--------+-----------+----------+
| deptno | job       | max(sal) |
+--------+-----------+----------+
|     10 | CLERK     |  1300.00 |
|     10 | MANAGER   |  2450.00 |
|     10 | PRESIDENT |  5000.00 |
|     20 | ANALYST   |  3000.00 |
|     20 | CLERK     |  1100.00 |
|     20 | MANAGER   |  2975.00 |
|     30 | CLERK     |   950.00 |
|     30 | MANAGER   |  2850.00 |
|     30 | SALESMAN  |  1600.00 |
+--------+-----------+----------+


```



**注意**

当一条SQL语句当中有`group by`的话，`select`后面只能写分组函数和参与分组的字段；



**Having过滤**

> having用于对group by分组后的数据进行再次筛选；

```sql
#找出每个部门的最高薪资，要求显示薪资大于2900的数据；
#方式一：
mysql> select deptno,max(sal) from emp group by deptno having max(sal) > 2900;
#方式二：
mysql> select deptno,max(sal) from emp where sal > 2900 group by deptno;
```

两种方式查询到的结果都是一样的，但是方式二的效率更高；在实际使用当中，能用where子句提前筛选就使用where，不能使用where子句筛选再考虑使用having；




## 8、 DQL语句执行顺序

---

一条完整的DQL语句的执行顺序如下：

```sql
SELECT			5
	……
FROM			1
	……
WHERE			2
	……
GROUP BY		3
	……
HAVING			4
	……
ORDER BY		6
	……
```



# 第三章：SQL函数

SQL 中的函数一般是在数据上执行的，可以很方便地转换和处理数据。

SQL函数分为内置函数和我们自定义的函数，内置函数的支持情况和实现原理等都是由`DBMS`来决定的，因此我们在使用内置的SQL函数时应该注意SQL代码具体的运行环境(DBMS)；

实际上只有很少的函数是被DBMS同时支持，比如：大多数`DBMS`使用运算符 `||`或`+` 来做字符串的拼接，而MySQL数据库使用的是内置函数`CONCAT()`。大部分DBMS都有自己特定的内置函数，这就意味着使用内置SQL函数的SQL代码是`可移植性差`的。从SQL的通用性来看，不建议使用内置函数；



## 1、单行处理函数

> 多行处理函数也叫分组函数，可以对每一组当中的所有记录的字段进行处理；
>
> 多行处理函数：多个输入对应一个输出；
> 



**单行处理函数详细**

| 单行处理函数                                                 | 作用                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| lower（name【字段、常量……】）                                | 转换小写；                                                   |
| upper（name【字段、常量……】）                                | 转换大写；                                                   |
| substr（name【字段……】，1【起始下标，从1开始】，1【截取的长度】） | 截取字符串；                                                 |
| length（name【字段、常量……】）                               | 获取长度；                                                   |
| trim（name【字段、常量……】）                                 | 去除空格；                                                   |
| round（sal【数字、字段……】，0【保留小数位的个数，0表示保留整数位，负数顺理往前移】） | 四舍五入；                                                   |
| rand（）                                                     | 生成随机数； 例：0.5942256772836909                          |
| now（）                                                      | 返回当前的日期以及时间，示例：2001-11-01 12:00 ；            |
| ifnull（字段，为空时转换的值）                               | 当字段为NULL的时候将NULL值转换为一个固定的值；该函数用于处理字段可能会出现NULL的情况； |
| case 表达式 when 表达式 then 表达式 when 表达式 then 表达式 else 表达式 end | 就是SQL中的条件选择语句：if…… else if…… else……               |
|                                                              |                                                              |
|                                                              |                                                              |



## 2、聚合函数

> 聚合函数也叫多行处理函数；

示例

```sql
#多行处理函数对每一行的字段进行处理后输出一行；

#示例：统计有多少员工；
mysql> select count(ename) from emp;
mysql> select count(*) from emp;
#区别：`count(*)`统计的是总记录条数与字段无关，`count(ename)`统计的是字段`ename`不为空的数据的个数；

#示例：找出哪个员工的工资最低；
mysql> select min(sal) from emp;

#示例：找出哪个员工的工资最高；
mysql> select max(sal) from emp;

#示例：找出员工的平均工资；
mysql> select avg(sal) from emp;
```



多行处理函数也能组合使用

```sql
mysql> select count(*),min(sal),max(comm) from emp;
```



重点：

- **多行处理函数自动忽略`NULL`！！！**
- 多行处理函数不能直接写在`where`子句后面；
- 使用分组函数但是未使用`group by`语句，那么会将`where`子句查询到的记录自动分为一组，输出一行；





# 第五章：约束

## 1、非空约束



**注意**

非空约束只有列级约束，没有标记约束；

## 2、唯一性约束

> 唯一性约束控制字段不能重复，但是可以为**NULL**；



## 3、主键约束

> 主键约束控制字段不能重复，且能不为**NULL**；
>

### **主键的分类**

- 按照主键字段的数量来区分
  - 单一主键：一个字段作为主键【推荐且常用】
  - 复合主键：多个字段联合起来为一个主键约束【不推荐】
    - 不建议使用，因为违背数据库设计三范式中的第二范式，会产生`部分依赖`；
- 按照主键的性质来区分
  - 自然主键：主键值是和业务没有关系的自然数【推荐】
  - 业务主键：主键值和系统的业务挂钩【不推荐】
    - 例如：银行卡的卡号作为主键、身份证号作为主键……
    - 不推荐使用，因为主键值和系统业务挂钩的话，一旦业务发生变化，主键值可能也会随之发生变化。有的时候可能没法变化因为变化后可能会导致主键值重复；

### **主键自增**





**注意**：一张表的主键约束只能有一个，主键字会自动添加索引`index`；

## 4、外键约束

外键约束主要是用来做关联查询，使用外键约束可以将表与表之间建立联系；





# 第六章：数据库设计三范式【重点】

## 1、什么是三范式？

三范式就是设计数据库表的**依据**。依据三范式设计出来的表不会出现冗余数据；

## 2、三范式都有哪些？

- 第一范式：任何一张表都应该有主键，并且每一个字段原子性不可再分；

- 第二范式：建立在第一范式的基础之上，所有非主键字段完全依赖主键字段，不能产生部分依赖；

  复合主键就违反了第二范式，会产生数据冗余；

  **多对多，三张表，关系表加两个外键；**

- 第三范式：建立在第二范式的基础之上，所有非主键字段直接依赖主键，不能产生传递依赖；

  **一对多，两张表，多的加外键；**
  
  

**注意**：三范式只是**理论**上的方法，而在实际开发过程（**实践**）当中不一定要完全遵守三范式，因为完全遵守三范式会导致创建很多张表，多张表连接查询会导致查询速度变慢（连接查询产生笛卡尔积）。这时候为了满足客户的需求，会选择空间（冗余数据）来换速度；

## 3、一对一关系的设计方案？

> 一对一的设计方案有两种，分别为：1主键共享、2外键唯一；

**主键共享【不推荐】**

第二张表的主键添加外键，引用第一张表的主键，就是主键共享；

**外键唯一【推荐】**

两张表，多的一方额外添加一个字段，这个字段添加唯一外键；





# 第五章：注意事项
- 每一条SQL语句都是以分号（`;`）结束的，不见分号（`;`），sql语句不会执行；

- SQL语句不区分大小写；

- 在MySql当中，字符串用单引号或者双引号括起来都可以，但是在Oracle、Sql Server等数据库当中只能使用单引号；尽管在MySql数据库当中可以使用双引号，但是为了保证sql语句的通用性，建议字符串都使用单引号括起来；

- 在数据库当中只要数学表达式当中有`NULL`参与，结果必定是`NULL`；





# 第六章：数据库的安装

## 1、MySQL数据库的安装

### 1）MySQL在Linux上的安装

> 在Linux上安装MySQL有以下三种方式：1RPM、2YUM、3编译源码；









### 2）MySQL在Windows上的安装

- 1、去[官网](https://dev.mysql.com/downloads/mysql/)下载安装包

![][mysql之windows安装01]



![][mysql之windows安装02]





















































































```
Base64：
```

[mysql之windows安装01]:data:image/png;base64,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qEVEREREREScoIRaRERERERExAlKqEVEREREREScoIRaRERERERExAlKqEVEREREREScoIRaRERERERExAlKqEVEREREREScoIRaRERERERExAlKqEVEREREREScoIRaRERERERExAlKqEVEREREREScoIRaRERERERExAlKqEVEREREREScoIRaRERERERExAlKqEVEREREREScoIRaRERERERExAlKqEVEREREREScoIRaRERERERExAlKqEVEREREREScoIRaRERERERExAlKqEVERERERESc4HahAxAREREREeedOnWKkpMnKSkpobS09EKHI9JguLi4YDAYMLi54erqXK1ZCbWIiIiISANltVg4efLkhQ5DpEEqLS3l5MmTnDx5Ejc3N4wmU733oZZvEREREZEG6MSJE0qmRc6SkydPcuLEiXpvp4RaRERERKSBsVosnCopudBhiPypnCopwWqx1GubP3FCncnrIa+ReaHDEBERERE5i06dOqXKtMg5cvLkSU6dOlXn8Q0kobZg/mg29w3sz6ioPvSNGs/sTYXndsoSM5kZxbUOKfw6nqei+jNgxEgGDBzOU3HpFF6AHwrNGZlURJpFwvh4Muv3w0qtCrfHM3Fgf4aP6E/fgSN5ankWTu2+KJPMA2cvLhEREZG/ohIl0yLnVH3+jTWMRcmyE5i4PoA3P5yErwEoKabY4nFu5/whhRX7BxEYVP3bhesmMnx9OO8u+QQ/+7XreeumMv7JQua9HInXuY3OQRYpq3IYFBRofx5A9LyAs7f74hRem/470Ss+IbgJUGKh+CjU/3J9KN6+nBSvQAJbn73wRERERP5qStTqLXJOlZSUYKzj2AZRoS7e/yMEBdiSaQCDBx5N7I9L8kiJHcuAgcMZMHA8Cd/XUDv9OYXZY/ozIKo/Ax5JIOtYxVuW7xNsleao/vQd+Bbpu1cwcfoSUt5+jFH3jmTW+irV8JIsEt82MWnqoPJkGsB3wJOMMb1F4ve255lzx5OwcQXTooYzfGAfBjzhOK+FrMUTGTBwOMMHjmTW+rzy/WTOnUjiD1kkPDKcAQPfIhMo3Gir0A+P6kPfMbNJKQDIYuVjM0nY9BYT7x3JqOdTKKzU6p7J6/cmsGX9bO4bMZLhEX24Ly6zorrscE56hYTQPSSE7nOrNMn/bCazc2cCys63wYSHhwm+j2dw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H2NWTjBegOXnwwSMn0Sk9xm2/VtnIt0TSPrXZGbnBNLoh43lbcvgS9jAMEzPvcW0p38n/G8m4DBZjfoxZ3QgASH+MC+OWc/9Tmjrw6S/l0ftCXUOKYveIs/DQt6mFSRlmwh4YAz9vAECCL/bn4S4l5j8fC7B7mZSVoEpchChXgCdCbsGXvvkQ+gfiz9Q3D6MvJc+4SBhTAqs+kNCHRhqnzPPwxc4yM71S5i/NY/0dQ4pe63nDSwH0knP8SAgNAAv3YpNRERERETqoEEuSoZ3JI+OD8SyaQavJReCdySxcVO403MnK+LiiY9bSbrBy9YW3D6GOS8MI/BoKglx8SRsAn9fE5gCGffWPMZdn8encfEkZDTjzqlLmNLHiUSvvsrmDjlMSlw88XEJfJrXDK8mddjWM5xHn48mkHRWrkrnROQEJnWqeNtrQCyLpw7D47sVxMfFE78qnUZetjbngOGxTIr0ICdpBYnZfox7ZtgZqsR5bFkeT3xcIlmXhjNh7ocsGlt2yywTgffN480HupGXHE/80nQ8hk5h8TPhtoXi8CMg2ITlqIXgAH9MgFfbzvgetWC5JpTOZ/rhoPoTV+ucAcNnMK5TIzI/SCBxfwcmvfIo5TdVq/W8FZO+aDITp65k59FqJxYRERERETmNS2lpaem52vn27dsJ6tLlXO1eRERERERE5IJpmBVqERERERERkQtMCbWIiIiIiIiIE5RQi4iIiIiIiDhBCbWIiIiIiIiIE5RQi4iIiIiIiDhBCbWIiIiIiIiIE5RQi4iIiIiIiDhBCbWIiIiIiIiIE5RQi4iIiIiIiDhBCbWIiIiIiIiIE5RQi4iIiIiIiDhBCbWIiIiIiIiIE5RQi4iIiIiIiDhBCbWIiIiIiIiIE9wudAB1cezo0QsdgoiIiIj8xTVr1uyc7bvk1Klztm8ROXdUoRYRERERERFxghJqEREREREREScooRYRERERERFxghJqEREREREREScooRYRERERERFxghJqEREREREREScooRYRERERERFxghJqEREREREREScooRYRERERERFxghJqEREREREREScooRYRERERERFxghJqEREREREREScooRYRERERERFxghJqEREREREREScooRYRERERERFxghJqEREREREREScooRYRERERERFxgtuFDkBERET+PLLzD/HupmwCfS/l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



[mysql之windows安装02]:data:image/png;base64,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FkN+5kc2EZHTTWFhIfHxGhb9S9AQzeao2MiqL3qR/JtT9qvssSkpZFd0LPVv6S/ctRMiNLWYNKWCjZ+spVdyr1M33MFp8f6uPlhIRUxMbbjDU8H+nfsCJzOREFXNwQMVgbMbV+xn5/4YInX5RUTkOGiIZpMKWfXUY7z1QwRDpkw7cTesnyrOGsId7Z/h3rtexRphobgEOvcfw7Qb9euKNKzw/57gsXfziLhoKtOOezKIk+w0eH9bkkYxat2TTJxSTmRYNcVVsfQYNoEJyadOCJWTxUK/q0eR+8xEJpZFEuktpjymB5eNn3Bs6xyKiIjU0BBNERERERE5qTRE85ejIZoiIiIiIiIhQgFPREREREQkRCjgiYiIiIiIhAgFPBERERERkRChgCciIiIiIhIiFPBERERERERChAKeiIiIiIhIiFDAExERERERCREKeCIiIiIiIiFCAU9ERERERCREKOCJiIiIiIiECAU8ERERERGREKGAJyIiIiIiEiLMv3YDfmmFhYW/dhNEREREREROCoPP5/P92o0QERERERGR46chmiIiIiIiIiFCAU9ERERERCREKOCJiIiIiIiECAU8ERERERGREKGAJyIiIiIiEiIU8EREREREREKEAp6IiIiIiEiIUMATEREREREJEQp4IiIiIiIiIUIBT0REREREJEQo4ImIiIiIiIQIBTwREREREZEQoYAnIiIiIiISIhTwREREREREQoQCnoiIiIiISIhQwBMREREREQkRCngiIiIiIiIhQgFPREREREQkRCjgiYiIiIiIhAgFPBERERERkRChgCciIiIiIhIiFPBERERERERChAKeiIiIiIhIiFDAExERERERCREKeCIiIiIiIiFCAU9ERERERCREmBt6sqhDl1+6HSIiJ0Tc7u9/7SaIiIiI/GrUgyciIiIiIhIiGuzBO0y/hIvI6UIjD0RERETUgyciIiIiIhIyFPBERERERERChAKeiIiIiIhIiFDAExERERERCREKeCIiIiIiIiFCAU9ERERERCREKOCJiIiIiIiECAU8ERERERGREKGABxQsX4AhcwFvHDj1y9668E0M095hXv6JKe+/WwFvPP46hsxlrP0Fa1372smp01/uyXkfi4iIiMjp4RQPeJuZmfk6hszXSXptM5VHPv/a5mMos4CVC5ezdM+Ja+UvqcdFvVkyMom0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

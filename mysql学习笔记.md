# Mysql学习笔记

- 查看mysql有哪些数据库

  show databases;

- 选择数据库 use 

- 创建数据库：create database xxx;

  - 行：记录
  - 列：字段

## 1. SQL的分类

- DQL(Data Query Language：数据查询，带sql的

- DML( Data Manipulation Language：数据操作语言，增删改查表
  - insert delete update
- DDL(Data Definition Language：数据定义语言，创建删除修改数据库
  - create, alter, drop
- DCL(Data Control Language：数据库管理语言，备份、恢复、性能优化
- TCL(Transaction Control Language): commit, rollback, savepoint



## 2. 导入数据库

source /.../.../....sql

查看编码：show variables like 'char%';

只看表结构 **desc** tablename;





## 3. 创建表

CREATE TABLE table_name (column_name column_type);



CREATE TABLE IF NOT EXISTS `student`(   `stuID` INT UNSIGNED AUTO_INCREMENT,   `stuNAME` VARCHAR(100) NOT NULL,   `stuCLASS` VARCHAR(40) NOT NULL,   `date` DATE,   PRIMARY KEY ( `stuID` ) )engine=InnoDB DEFAULT CHARSET=utf8;



## 4. 插入数据（增

INSERT INTO table_name ( field1, field2,...,fieldN)

​					VALUES

​					（value,  value2, ..., valueN);

INSERT INTO student ( stuID, stuNAME, stuCLASS, date)

​					VALUES

​					(1, "JZ", "3", CURDATE());

## 5. 删除数据（删

- DELETE FROM <表名> [WHERE 子句] 删除一行或多行数据

- 删除表和数据库都用drop：
  - drop table table_name;
  - drop database database_name;



## 6. 改变数据（改

- UPDATE table_name SET field=new-value, field=new-value2 [WHERE Clause]



## 7. 查询数据（查

1. 简单查询: SELECT * FROM table

2. 带条件查询：SELECT * FROM table WHERE 列名=列名类型的值

3. 分组查询与排序

   1. 排序：SELECT * FROM table ORDER BY ASC/DESC升序或降序

   2. GROUP BY: SELECT column_name, function(column_name)

      ​			FROM table_name

      ​			WHERE colunm_name OPRATOR value

      ​			GROUP BY column_name;

4. 复杂查询：

   1. 连接查询：

      ```sql
      SELECT teacher.no, tn, course_n
      FROM teacher, tc
      WHERE (teacher.tno = tc.tno) and (tn = "刘老师")







## 8. 记忆！

敲着背一遍

mysql数据库学到什么程度就能找工作? - 跟大彬学编程的回答 - 知乎
https://www.zhihu.com/question/481900938/answer/3140726797



### 8.1 什么是MySQL

是一个关系型数据库，用表的形式来存储数据。

表结构是行和列，行代表一行数据，列代表数据中的每个值。

列上值的数据类型有整数、字符串、日期等



### 8.2 数据库三大范式

- 第一范式1NF：确保数据库表字段的原子性。

  - 例如：userInfo: 广东省 10086：需要拆分成两个字段，保证原子性

- 第二范式2NF：

  - 满足第一范式

  - 表必须有主键primary key; 

  - 非主键列必须完全依赖主键，不能只依赖于主键的一部分

  - 例：假设选课关系表为student_course(stu_no, stu_name, age, course_name, grade, credit)，主键为(stu_no, course_name)。 

    credit学分完全依赖于course_name，而stu_name和age完全依赖于stu_no, 违反了第二范式。

    会导致：

    1. 数据冗余：学生选了n门课，stu_name和age会有n条记录

    2. 插入异常：插入一门新课，但是一般不会带上学生的stu_no，所以没办法插入！

       所以应该拆分表：

       - student(stu_no, stu_name, age)
       - course(course_name, credit)
       - enrollment(stu_no, course_name, grade)

- 第三范式3NF：

  - 满足第二范式

  - 非主键必须直接依赖主键，不能存在依赖传递：非主键A依赖于非主键B，非主键B依赖于主键

  - 例：假设学生关系表student(stu_no, stu_name, age, academy_id, adacemy_contact)，

    ​	学院电话依赖于academy_id学院id，学院id依赖于学号，所以有传递依赖，不符合第三范式。

    拆分表：student(stu_no, stu_name, academy_id), academy(academy_id, academy_contact)



### 8.3 事务的四大特性

事务transaction也就是一组数据库操作（例如插入、更新）的逻辑单元，最小且不可分割。事务的目的是确保数据库操作的完整性和一致性。

- 原子性Atomicity：一个事务包含的所有操作要么全部成功，要么全部失败回滚
- 一致性consistensy:一个事务执行前、执行后必须处于一致性状态。比如啊a与b账户总额1000块，两个人之前转账成功或失败，账户总和还是1000
- 隔离性Isolation：两个事务不互相干扰，独立执行
- 持久性Durability：一个事物一旦被提交，那么对数据库中的数据改变是永久的，即使数据库 遇到故障，也不会丢失提交事务的操作。


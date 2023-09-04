# MySQL

# 数据库

## SQL概述

SQL一般发音为 sequel，SQL 的全称 Structured Query Language)，SQL 用来和数据库打交道，完成和数据库的通信，SQL是一套标准。但是每一个数据库都有自己的特性别的数据库没有,当使用这个数据库特性相关的功能,这时 SQL语句可能就不是标准了.(90%以上的 SQL 都是通用的)

### 什么是SQL

SQL（Structured Query Language）是结构化查询语言的简称，它是一种数据库查询和程序设计语言，同时也是目前使用最广泛的关系型数据库操作语言。在数据库管理系统中，使用SQL语言来实现数据的存取、查询、更新等功能。SQL是一种非过程化语言，只需要提出“做什么”，而不需要指明“怎么做”。

SQL是一套标准，程序员主要学习的就是SQL语句

## 什么是数据库

数据库（Database）是按照数据结构来组织、存储和管理数据的仓库，它产生于距今六十多年前，随着信息技术和市场的发展，特别是二十世纪九十年代以后，数据管理不再仅仅是存储和管理数据，而转变成用户所需要的各种数据管理的方式。数据库（Database）是按照数据结构来组织、存储和管理数据的仓库

## 什么是数据库管理系统（DBMS）

用来管理数据库的计算机系统称为**数据库管理系统**（Database Management System，DBMS）

1. 常见的数据库管理系统：
   
   1. MySQL
   2. Oracle
   3. MS
   4. SQLServer
   5. DB2
   6. ...

# MySQL的常用命令

1. 启动MySQL服务
   
   1. net stop mysql：停止mysql服务(windows)
   2. net start mysql：启动mysql服务(windows)

2. 登录\退出MySQL
   
   1. mysql -u[username] -p [password]：登录MySQL
   2. exit：退出MySQL

3. 数据库基本命令
   
   1. show databases：查询所有数据库
   2. use [database]：使用数据库
   3. show tables：查看数据库下所有表
   4. create database [databasename]：创建数据库
   5. source [SqlFilePath]：导入数据库脚本语句（！！！注意路径中不能有中文）
   6. desc [tablename]：不看数据库中的数据，只看表结构
   7. select version()：查看数据库版本
   8. select database()：查看当前使用的数据库

## 数据库中的最基本的单元

数据库中最基本的单元是 **表(table)，因为表比较直观。**

1. 任何一张表都有行和列
   
   1. 行(row\)：被称为数据/记录。
   2. 列(column)：被称为字段

2. 了解一下
   
   1. 每个字段都有：字段名、数据库类型、约束等属性
   
   2. 字段名可以理解，是一个普通的名字，见名知意就行。
   
   3. 数据类型: 字符串，数字，日期等，后期讲。
   
   4. 约束: 
      
      1. 约束也有很多，其中一个叫做唯一性约束这种约束添加之后，该字段中的数据不能重复

# SQL的分类

SQL语句有很多，最好分门别类，这样更容易记忆

* SQL的类型
  
  1. DQL： 数据查询语言 (凡是带有select关键字的都是查询语句)select...
  
  2. DML：数据操作语言(凡是对表当中的数据进行增删改的都是DML)
  
  3. DDL：数据定义语言凡是带有create、 drop、 alter的都是DDL。DDL主要操作的是表的结构。
     
      不是表中的数据  
      create: 新建，等同于增  
      drop: 删除  
      alter: 修改  
      这个增删改和DMM不同，这个主要是对表结构进行操作。
  
  4. TCL：事务控制语言
  
  5. DCL：数据库控制语言。例如:授权grant、撤销权限revoke..

# MySQL查询语句(DQL)

## 简单查询

1. 查询字段
   
   1. select [columnName] from [tableName]：查询一个字段
   2. select [columnName1],[columnName2]... from [tableName]：查询多个字段(用逗号隔开字段)
   3. select * from [tableName]：查询所有字段（不推荐！！！，效率低）

2. 给查询字段起别名
   
   1. select [columnName] as [nickname] from [tableName]：使用 as 给字段起别名。
      
       （！！！注意：as 只是给字段名起个别名显示，原表字段该叫啥还是叫啥。select语句永远只能查询不能修改）

3. 列(column)参与数学运算
   
   1. select [column*12] from [tablename]：结论字段是可以使用数学表达式

## 条件查询

* 条件查询需要用到where语句，where必须放到from语句表的后面

* 支持如下运算符
  
  | 运算符              | 说明                        |
  | ---------------- | ------------------------- |
  | =                | 等于                        |
  | <>或!=            | 不等于                       |
  | <                | 小于                        |
  | <=               | 小于等于                      |
  | >                | 大于                        |
  | >=               | 大于等于                      |
  | between … and …. | 两个值之间,等同于 >= and <=       |
  | is null          | 为null（is not null 不为空）    |
  | and              | 并且                        |
  | or               | 或者                        |
  | In               | 包含，相当于多个or（not in不在这个范围中） |
  | Not              | not可以取非，主要用在is 或in中       |
  | like             | like称为模糊查询，支持%或下划线匹配      |
1. where

2. select [columnName1],[columnName2],[columnName3]...from [tableName] where [columnName1] = [[prerequisite]()]：使用where字段给查询添加条件

3. and
   
   1. select [columnName1],[columnName2],[columnName3]...from [tableName] where [columnName1] = [[prerequisite]()] and [columnName2] = [[prerequisite]()]：where语句给字段添加条件，还可以加上and（并且）语句增加条件
      
       （！！！注意在数据库中不能使用等号衡量，需要使用is null 因为数据库中的nu11代表什么也没有，它不是一个值，所以不能使用等号衡量。）

4. or
   
   1. select [columnName1],[columnName2],[columnName3]...from [tableName] where [columnName1] = [[prerequisite]()] or [columnName2] = [[prerequisite]()],or [columnName3] = [[prerequisite]()]：where语句给字段添加条件，还可以加上or（或者）语句增加条件

5. in 包含，相当于多个 or(not in 不在这个范围中)

6. not not 可以取非，主要用在 is 或 in 中

7. like like 称为模糊查询，支持8或下划线匹配
   
   1. select [columnName1],[columnName2],[columnName3]... from [tableName] like '%[prerequisite]()%'

8. &匹配任意个字符下划线，一个下划线只匹配一个字符

9. 排序order by
   
   1. select [columnName1],[columnName2],[columnName3]... from [tableName] order by [column1]：给[column1]进行排序（默认是升序）
   2. select [columnName1],[columnName2],[columnName3]... from [tableName] order by [column1] desc：给[column1]进行排序（desc：指定为降序）
   3. select [columnName1],[columnName2],[columnName3]... from [tableName] order by [column1] aesc：给[column1]进行排序（aesc：指定为升序）

## 数据处理函数\单行处理函数

* [ ] 数据处理函数又被称为单行处理函数  
  单行处理函数的特点:一个输入对应一个输出。  
  和单行处理函数相对的是: 多行处理函数。（多行处理函数特点: 多个输入，对应1个输出!）

* [ ] 常见的单行处理函数
  
  1. lower：转小写
     
     1. select lower([columnName]) from [tableName]：（14个输入，最后还是14个输出。这是单行处理函数的特点。）
  
  2. upper：转大写
     
     1. select upper([columnName]) from [tableName]
  
  3. substr：取字符串（substr( 被截取的字符串，起始下标,截取的长度)）
     
     1. select substr([columnName],1,1) from [tableName];
  
  4. lengtn：取长度
     
     1. select lengtn([columnName]) from [tableName];
  
  5. trim：去除空格
     
     1. select [columnName] from [tableName]where [columnName]= trim('             [[prerequisite]()]')
  
  6. str_to_date：将字符串转为日期
  
  7. date_format：格式化日期
  
  8. format：设置千分位
  
  9. round：四舍五入
  
  10. rand()：生成随机数
  
  11. ifnull：将null转为一个具体的值

## 分组函数（多行处理函数）

多行处理函数的特点: 输入多行，最终输出一行

* [ ] 一共有五个
  
  1. count：计数
     
     1. select count([column]) from [tableName]
  
  2. sunm：求和
     
     1. select sunm([column]) from [tableName]
  
  3. avg：求平均值
     
     1. select avg([column]) from [tableName]
  
  4. max：求最大值
     
     1. select max([column]) from [tableName]
  
  5. min：求最小
     
     1. select min([column]) from [tableName]

* [ ] ！！！注意:
  
  1. 分组函数在使用的时候必须先进行分组，然后才能用。如果你没有对数据进行分组，整张表默认为一组。
  
  2. 分组函数会自动或略null
  
  3. 分组函数中count(*)和count(具体字段) 有什么区别?
     
     1. count(具体字段)：表示统计该字段下不为null元素的总数
     2. count(*)：表示统计当表中的总行数（只要有一行数据count则++）

## 分组查询(group by)

* [ ] 什么是分组查询
  
  在实际的应用中，可能有这样的需求，需要先进行分组，然后对每一组的数据进行操作。这个时候我们需要使用分组查询，怎么进行分组查询呢 ?

* [ ] 将之前的关键字全部组合在一起，来看一下他们的执行顺序?
  
  ```sql
  select ...
  from ...
  where ...
  group by
  ...
  order by
  ...
  ```
  
  需要记忆。以上关键字的顺序不能颠倒，执行顺序是什么
  
  1. from
  2. where
  3. group by
  4. order by
  
  为什么分组函数不能直接使用在where后面?

* [ ] ```sql
  select ename,sal from emp where sal > min(sal)//报错
  //因为分组函数在使用的时候必须先分组之后才能使用。
  where执行的时候，还没有分组。所以where后面不能出现分组函数。
  select sum(sal) from emp ;
  //这个没有分组，为啥sum 函数可以用呢?
  //因为select在qroup by之后执行。
  ```
1. 列子：
   
   1. 找出每个工作岗位的工资总和？
      
      ```sql
      <!--实现思路：按照工作岗位分组，然后对工资求和-->
      select job,sum(sal) from emp group by job;
      ```
      
      重点总结：
   
   2. 在一条select语句当中，如果有group by语句的话select后面只能跟: 参加分组的字段，以及分组函数。其它的一律不能跟。

2. having：对于分完组之后的数据再次进行过滤
   
   ```sql
    select [columnname1],max([columnname2]) from [tableName] group by [columnname1] having max([columnname2]) > 3000;
   ```

3. distinct：取出重复字段（！！！distinct只能出现字段的最前方）
   
   ```sql
   <!--distinct只能出现字段的最前方-->
   select distinct [columnname] from [tablename]
   ```

## 连接查询

* 什么是连接查询？
  
  * 从一张表中单独查询，称为单表查询。
  * table1和table2表联合起来一起查询数据，比如从table1中取出员工名字，从table2中取出部门名字。这种跨表查询，多表联合起来一起查询数据被称为连接查询

* 连接查询的分类？
  
  * SQL92：1992年的时候出现的语法
  * SQL99：1999年的时候出现的语法

* 根据连接的方式分类
  
  * 内连接
    
    * 等值连接
    * 非等值连接
    * 自连接
  
  * 外连接
    
    * 左外连接
    * 右外连接
  
  * 全连接

### 笛卡儿积

1. 当两张表进行连接查询时，没有任何条件的限制会发生什么现象?

2. 案例：查询每个员工所在部门名称
   
   1. 两张表连接没有任何限制
      
      ```sql
      select * from emp,dept;
      <!--这个时候我们查询出来了许多不该出现的数据-->
      56 rows in set (0.00 sec)
      14 * 4 = 56
      ```
      
       当两张表进行连接查询，没有任何条件限制的时候，最终查询结果条数，是两张表条数的乘积，这种现象被称为: 笛卡尔积现象。(笛卡尔发现的，这是一个数学现象。)
   
   2. 怎么避免笛卡尔积现象？
      
      1. 连接时加条件，满足这个条件的记录被筛选出来!
         
         ```sql
         select * from emp,dept where emp.deptno = dept.deptno;
         14 rows in set (0.00 sec)
         ```
      
      2. 思考:
         
         1. 最终查询的结果条数是14条，但是匹配的过程中，匹配的次数减少了吗?还是56次，只不过进行了四选一。次数没有减少。
      
      3. 注意：
         
         1. 通过笛卡尔积现象得出，表的连接次数越多效率越低，尽量避免表的连接次数。

### 内连接

#### 等值连接

1. 案例:查询每个员工所在部门名称，显示员工名和部门名?
   
   1. SQL92语法：
      
      ```sql
      select 
          e.ename,d.dname 
      from 
          emp as e ,dept as d 
      where 
          e.deptno = d.deptno;
      ```
      
       缺点：结构不清晰，表的连接条件，和后期进一步筛选的条件，都放到了where后面
   
   2. SQL99语法：
      
      ```sql
      select 
          e.ename,d.dname 
      from 
          emp as e
      join 
          dept as d 
      on 
          e.deptno = d.deptno;
      ```
      
       优点: 表连接的条件是独立的，连接之后，如果还需要进一步筛选，再往后继续添加where

#### 非等值连接

1. 案例:找出每个员工的薪资等级，要求显示员工名、薪资、薪资等级?
   
   ```sql
   select e.ename,e.sal,s.grade from emp e join salgrade s on e.sal between s.losal and s.hisal
   ```
   
    条件不是一个等量关系，称为非等值连接

#### 自连接

1. 案例:查询员工的上级领导，要求显示员工名和对应的领导名?
   
   ```sql
   select a.ename as '员工名',b.ename as '领导名' from emp a join emp b on a.MGR= b.EMPNO;
   ```
   
    技巧：一张表看成两张表

2. 以上就是内连接的自链接

### 外连接

内连接特点：完全能匹配上这个条件的数据库给查询出来。两张表平等没有主次关系

1. 外连接
   
   ```sql
   select e.ename,d.dname from emp e right join dept d on e.deptno = d.deptno;
   ```
   
   1. right（右外连接）代表什么:表示将join关键字右边的这张表看成主表，主要是为了将  
       这张表的数据全部查询出来，捎带着关联查询左边的表。产生了主次关系。在外连接当中，两张表连接，
   2. left（左外连接）

## 子查询

1. 什么是子查询？
   
    select语句中嵌套select语句，被嵌套的select语句被称为**子查询**

2. 子查询都可以出现在哪呢？
   
   1. select...(select)
   2. from...(select)
   3. where...(select)

3. where子语句中的子查询
   
   1. 案例:找出比最低工资高的员工姓名和工资 ?
   
   2. 实现思路：
      
      1. 查询最低工资
         
         ```sql
         select min(sal) from emp;
         ```
      
      2. 找出大于800的
         
         ```sql
         select ename.sal from emp where sal > 800
         ```
      
      3. 合并
         
         ```sql
         select ename,sal from emp where sal > (select min(sal) from emp);
         ```

4. from子句中的子查询
   
    ！！！from后面的子查询，可以将子查询的查询结果当做一张临时表。注意:(技巧)
   
   1. 案例：找出每个岗位的平均工资的薪资等级
   
   2. 第一步：找出每个岗位的平均工资（按照岗位分组求平均值）
      
      ```sql
      select job,avg(sal) from emp group by job;
      ```
   
   3. 第二步:克服心理障碍，把以上的查询结果就当做一张真实存在的表t。  
       （薪资等级表 s）select * from salarade: s
      
       t表和s表进行表连接。 条件: t表avg(sal) between s.losal and s.hisal;
      
      ```sql
      select from t.* join salarade s on t.avg(sal) between s.losal and s.hisal;
      ```
   
   4. 第三部：合并
      
      ```sql
      select t.*,s.GRADE from (select job,avg(sal) as salavg from emp group by job) as t
       join salgrade s on t.salavg between s.losal and s.hisal;
      ```
      
      ‍
      
      ‍

5. select子句中的子查询
   
   1. 案例找出每个员工的部门名称，要求显示员工名、部门名

6. union：MySQL UNION 操作符用于连接两个以上的 SELECT 语句的结果组合到一个结果集合中。多个 SELECT 语句会删除重复的数据。

7. limit：是将查询结果集的一部分取出来，通常使用在分页查询当中。
   
   1. limit的使用
      
       案例：按照薪资降序，取出排名在前5名的员工
      
      ```sql
      <!--完整用法：
          limit startIndex,length
          startIndex：起始下标
          length：长度
      -->
      select ename, sal from emp order by sal desc limit 0,5;
      
      <!--省略用法：
          limit 5
      -->
      select ename, sal from emp order by sal desc limit 5;
      ```
   
   2. ！！！注意：MySQL当中limit是在order by之后执行
   
   3. 通用分页
      
      1. 取出工资排名在[5-9]名的员工?
         
         ```sql
         select ename, sal from emp order by sal desc limit 4,5;<!--长度length：9-5+1-->
         ```
   
   4. 分页
      
      * 每页显示3条记录
        
        * 第一页：limit 0,3 [0,1,2]
        * 第二页：limit 3,3 [3，4，5]
        * 第三页：limit 6,3 [6，7，8]
      
      * 每一页显示pageSize条记录
        
        * 第pageNo页：limit （pageNo - 1 ）* pageSize , pageSize
      
      * ！！！记住公式**​ limit (pageNo -1 ) pageSize,pageSize**

# 表的创建（DDL语句）

## 创建表

1. 表的语法格式：(建表语句数据与DDL，DDL包括：create、drop、alter)
   
   ```sql
   create table [tableName]([conlumnName1] [columnType],[conlumnName2] [columnType],[conlumnName3] [columnType]...)
   ```

## MySQL中的数据类型

1. MySQL常见的数据类型
   
   1. varchar
      
       可变长度的字符串，会根据实际的数据长度动态的分配空间
   
   2. char
      
       定长字符串，不管实际的数据长度都会分配固定的数据长度，使用不当会当值数据的浪费
   
   3. int
      
       数字中的整数型，等同于Java中的int
   
   4. bigint
      
       数字中的长整型，等同于Java中的Long
   
   5. float
      
       单精度浮点
   
   6. double
      
       双精度浮点
   
   7. date
      
       段日期类型
   
   8. datetime
      
       长日期类型
   
   9. clob
      
       字符大对象，最多可以存储4个g的字符串。
      
       超过255个字符串的都得采用clob
   
   10. blob
       
        二进制大对象，专门用来存储二进制文件比如图片、视频、声音等流媒体数据
       
        往blob类型字段上插入数据的时候，必须使用IO流

## 删除表

1. 删除表的语法格式
   
   ```sql
   <!--这样删除当这样表不存在的时候会报错-->
   drop table [tableName];
   <!--如果这张表存在的话删除-->
   drop table if exists [tableName];
   ```

# 插入数据insert（DML）

1. 语法格式
   
   ```sql
   insert into [tableName]([columnName1],[columnName2],[columnName3]) value([key1],[key2],[key3])
   ```
   
   * ！！！注意：字段名和值要一一对应，什么是一一对应？
     
     * 数量要对应，数据类型要对应

# 修改update(DML)

1. 语法格式：
   
   ```sql
   update [tableName] set [columnName1]=[value1],[columnName2]=[value2]...where 
   ```

2. ！！！注意：没有条件限制会导致所有数据更新

# 删除delete(DML)

1. 语法格式：
   
   ```sql
   delete from [tableName] where ...
   ```

2. ！！！注意：没有条件限制会导致所有数据删除

# 约束

## 什么是约束(constraint)

在创建表的时候，我们可以给表中的字段加上一些约束，来保证这个表中数据的完整性、有效性!! 

**约束的作用就是为了保证:表中的数据有效! !**

## 有哪些约束

1. 非空约束(not null)
2. 唯一性约束(unique)
3. 主键约束(primary key)
4. 外键约束(foreign key)
5. 检查约束(check):这个约束mysql不支持，Oracle支持。

### 非空约束（not null）

非空约束not null 约束的字段不能为null

1. 语法：
   
   ```sql
   drop table if exists t_vip;
   create table t_vip(
       id int,
       name varchar(255) not null <!--表示name字段不能为空null-->
   )
   ```

### 唯一性约束(unique)

唯一性约束unique约束的字段不能重复，但是可以为null

1. 语法：
   
   ```sql
   drop table if exists t_vip;
   create table t_vip(
       id int unique,<!--表示id字段必须是唯一的不能重复-->
       name varchar(255)
   )
   ```

2. 字段联合唯一性
   
   ```sql
   drop table if exists t_vip;
   create table t_vip(
       id int,<!--表示id字段必须是唯一的不能重复-->
       name varchar(255),
       age int
       unique(name,age) <!--表示name字段和age字段联合起来唯一-->
   )
   ```

3. ！！！注意：
   
   1. 约束直接加在列后面的叫做列及约束
   
   2. 约束没有添加在列的后面这种约束叫做表及约束
   
   3. 什么时候使用表及约束？
      
      1. 需要给多个字段联合起来添加某一个约束的时候，需要使用表级约束

### 主键约束(primary key简称 PK)

* 主键约束的相关术语
  
  1. 主键约束：一种约束
  2. 主键字段：该字段上添加了主键约束，这样的字段叫做主键字段
  3. 主键值：主键字段的每一个值叫做主键值

* 什么是主键？
  
  1. 主键值是每一行记录的唯一标识

* ！！！注意：任何一张表必须都得有主键，没有主键则表无效

* 主键特征：not null + unique （主键不能为null 同时也不能重复）

* 语法
  
  ```sql
  drop table if exists t_vip;
  create table t_vip(
      id int primary key,<!--给字段id设置为主键字段-->
      name varchar(255),
      age int
  )
  ```

### 自增（auto_increment）

这是MySQL中的一个机制，可以帮助我们自动维护一个主键值

1. 语法：
   
   ```sql
   drop table if exists t_vip;
   create table t_vip(
       id int primary key auto_increment<!--给字段id设置为主键字段,并且自增-->
       name varchar(255),
       age int
   )
   ```

### 外键约束（foreign key简称 FK）

* 外键约束的相关术语：
  
  1. 外键约束：一种约束
  2. 外键字段：该字段上添加了外键约束
  3. 外简直：外键字段中的每一个值

* 语法：
  
  ```sql
  drop table if exists t_student;
  drop table if exists t_class;
  create table t_class(
      classno int primary key,
      classname varchar(255)
  );
  
  create table t_student(
      no int primary key auto_increment,
      name varchar(255),
      cno int,
      foreign key references t_class(classno)<!--foreign key references t_class(classno) 表示引用t_class表中的classno字段为外键约束-->
  );
  ```

* ！！！注意：
  
  1. 外键约束是有父子关系的，引用外键的是子表，被引用则是父表
  
  2. 删除表的顺序？
     
      先删除子表，在删除浮标的
  
  3. 创建表的顺序
     
      先创建父表，在创建子表
  
  4. 删除数据的顺序
     
      先删除子表数据，在删除夫表数据
  
  5. 插入数据的顺序
     
      先插入父表数据，在插入子表数据

# 存储引擎

## 什么是存储引擎？

存储引擎是MySQL中特有的一个术语，其它数据库中没有。

实际上存储引擎是一个表存储/组织数据的方式。  
不同的存储引擎，表存储数据的方式不同。

## 添加存储引擎\指定存储引擎

可以在建表的时候给表添加指定存储引擎

我们可以通过`show create table [tableName]`​语句来查看建表的结构

1. 得出结论：
   
   1. mysql默认存储引擎是：InnoDB
   2. mysql默认字符编码是：utf8

# 事务（transaction）

## 什么是事务？

一个事务其实就是一个完整的业务逻辑。

1. 列子：
   
   假设转账，从A账户向B账户中转账10000将A账户的钱减去10000
   (update语句)将B账户的钱加上10000 (update语句)这就是一个完整的业务逻辑。
   
   这就是一个完整的业务逻辑
   
   要么同时失败，不可再分以上的操作是一个最小的工作单元，要么同时成功，这两个update语句要求必须同时成功或者同时失败，这样才能保证钱是正确的。

2. 只有DM语句才会有事务这一说，其它语句和事务无关! ! !
   
   1. insert
   2. delete
   3. update

3. 事务是怎么做到多条DM语句同时成功和同时失败的呢?
   
   1. InnoDB存储引擎: 提供一组用来记录事务性活动的日志文件
   2. 每一条DMM的操作都会记录到“事务性活动的日志文件”中。
   3. 在事务的执行过程中，在事务的执行过程中，我们可以提交事务，也可以回滚事务。

4. 提交事务、回滚事务
   
   1. **提交事务：commit**
   
   2. **回滚事务：rollback**

5. 案例1：
   
   ```sql
   <!--我们先插入一条数据-->
   insert into Seat(id,name) values(6,'lkj');
   <!--在回滚事务-->
   rollback;
   ```
   
   1. 通过案例1我们发现rollback失败了！insert语句还是插入了进去。这里我们得出结论，mysql默认情况下是自动提交事务的

6. 什么时候提交
   
   1. 没执行一条DML语句，则自动提交

7. 关闭自动提交事务：
   
   1. ```sql
      start transaction
      ```

## 事务的四个特性

1. A:原子性
   1. 事务是最小的工作单元，不可在分
2. C:一致性
   1. 所有事务必须一致，所有操作必须同时成功、失败保证事务的一致性。
3. I:隔离性
   1. 两个事务之间具有一定的隔离。教室A和教室B之间有一道墙，这道墙就是隔离性，事务A和事务B同时操作这样表的时候会怎么样？也就是多线程并发访问同一张表
4. D:持久性
   1. 事务最终结束的一个保障，事务的提交，就是相当于讲没有保存到硬盘的上的数据保存到硬盘上！

### 事务的隔离性

- MySQL支持四个不同的事务隔离级别，这些级别从低到高分别为：读未提交（READ UNCOMMITTED）、读提交（READ COMMITTED）、可重复读（REPEATABLE READ）和串行化（SERIALIZABLE）。
  
  1. 读未提交（READ UNCOMMITTED）：这是事务隔离级别最低的级别。在这种隔离级别下，一个事务可以看到其他未提交事务的变动。这种隔离级别允许脏读、不可重复读和幻读情况的发生。
  2. 读已提交（READ COMMITTED）：比READ UNCOMMITTED稍高的隔离级别。在这个隔离级别下，一个事务只能看到其他事务已经提交的变动。这种隔离级别禁止了脏读，但允许不可重复读和幻读情况的发生。
  3. 可重复读（REPEATABLE READ）：这是MySQL默认的事务隔离级别。在这个隔离级别下，同一事务中多次读取同一数据返回的结果是一致的，除非数据被本事务自己改变。这种隔离级别禁止了脏读和不可重复读，但仍然可能发生幻读情况。
  4. 串行化（SERIALIZABLE）：这是最高的事务隔离级别。在这个隔离级别下，事务串行化顺序执行，可以避免脏读、不可重复读和幻读的情况。但是，这种隔离级别效率低下，因为事务通常需要等待前一个事务完成，然后再继续执行。

- mysql8查看事务隔离级：
  
  ```sql
  select @@transaction_isolation;
  ```

# 索引

## mysql的查找方式

1. 全表查找
2. 索引查找

## 什么是索引？

```
 索引是在MySQL数据库中用于加速查询的一种数据结构。它可以帮助数据库系统更快地检索数据，特别是在大型数据表中。
```

​ 索引是在数据库表中的字段上添加的，是为了提高查询效率而存在的一种机制。一张表的一个字段可以添加一个索引，当然多个字段联合起来也可以添加索引。

对于以本字典来说，查找汉字有两种方式：

1. 一页一页的查找直到找到为止，这种在mysql中就是属于全局查找效率极其低下。
2. 先通过目录（索引）去定位某个范围，然后在定位这个位置，做局域查找。这种方式在mysql中就是索引检索，效率较高
- 在MySQL中，索引主要有以下几种类型：
  1. B-Tree索引：B-Tree（平衡多路查找树）是MySQL中最常用的索引类型，几乎所有的存储引擎都支持这种索引。它能够处理各种数据类型，包括整数、浮点数、字符串、日期等。B-Tree索引可以用于全值匹配和范围查询。
  2. 哈希索引：哈希索引基于哈希表实现，适用于等值查询。它的查找速度非常快，但并不支持范围查询。哈希索引在MySQL的Memory存储引擎中得到支持。
  3. 空间索引：空间索引（R-Tree）是一种专门用于处理地理空间数据的索引类型。它适用于点、线和多边形等空间对象的查询。空间索引主要在MySQL的MyISAM存储引擎中得到支持。
  4. 全文索引：全文索引用于在大量文本数据中进行快速搜索。它包括两部分：用于搜索的倒排索引和用于获取相关信息的正排索引。全文索引主要在MySQL的MyISAM和InnoDB存储引擎中得到支持。
- 在MySQL中创建索引时，需要考虑以下几个因素：
  1. 表的行数：表的行数越多，索引的效果越明显。
  2. 查询条件：只有当查询条件涉及到的列有索引时，索引才会发挥作用。
  3. 索引列的选择：选择经常被用于查询条件的列作为索引列。
  4. 索引类型选择：根据查询类型和数据分布选择合适的索引类型。
  5. 索引的创建和维护开销：在创建和维护索引时，需要权衡查询性能的提升和索引维护的开销。

## 索引的实现原理

<div style='color: red'>
    提醒1：在任何数据库中主键上都会自动添加索引对象，id字段上自动会有索引，因为id是PK.宁外字段上如果有unique约束的话，也会自动创建索引对象
</div>

<div style='color:red'>
    提醒2：在任何数据中，任何一张表中任何一条记录在硬盘上都有一个物理存储编号
</div>

![](/home/lkj/.config/marktext/images/2023-09-04-15-04-16-image-20230901191915811.png)

## 索引的创建与删除

1. 创建索引
   
   1. 语法：
      
      ```sql
      create index [indexName] on [tableName](columnName)
      ```

2. 删除索引
   
   1. 语法：
      
      ```sql
      drop index [indexName] on [tableName]
      ```

3. MySQL查看SQL语句是否使用了索引进行检索
   
   1. 语法：
      
      ```sql
      <!--解释sql是否使用了索引检索-->
      explain select * from [tableName] where [columnName] = valueName
      ```

## 索引失效

1. 模糊查询使索引失效
   
   1. 在使用 以下SQL时索引会失效
   
   ```sql
   select * from [tablName] where [columnName] like '%valueName%'
   ```
   
   ​ 以上SQL即使[columnName]添加了索引也会失效，因为在模糊匹配中以[%]开头了所以索引找不到了。

2. 使用or字段的时候失效
   
   1. 使用or有时也会失效，如果使用or那么要求or两边的条件字段都有索引，才会走索引

3. 复合索引
   
   1. 使用复合索引，或者更多的字段联合起来添加一个索引，叫做复合索引

4. ...

# 视图(View)

## 什么是视图？
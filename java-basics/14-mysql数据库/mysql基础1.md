<p align = "center" ><font size = 10， color = "#009999">mysql基础1</font></p>

## 1、数据库

**数据库：指长期保存计算机的存储设备上，按照一定的规则组织起来，可以被各种用户或应用共享的数据集合**

**数据库就是数据的仓库，用来保存数据的**

常见的数据库：

Mysql：开源免费，中小型数据库

Oracle：收费的大型数据库

SqlServer：收费的中型数据库

### 2、数据库结构

数据库管理程序（DBMS）可以管理多个数据库，一般开发人员会针对每一个应用创建一个数据库，为了保存应用中实体的数据，一般会在数据库中创建多个表

小结：

1. 一般情况下，一个系统（项目，软件）就会设计一个数据库
2. 一个数据库中有多张表，**一个实体Java对应一张表**
3. 一张表中有多条记录，一个对象对应一条记录

## 2、SQL概述

SQL：Structured Query Language(结构化查询语句)，通过**sql操作数据库（包括操作数据库，操作表，操作记录）**

### 2.1 sql语法

每条语句以分号结尾（命令行里面需要）

sql再windows中不区分大小写

### 2.2 sql分类

Data Definition Langeage(DDL数据定义语言)：操作数据库，操作表的

Data Manipulation Langeage(DML数据操作语言)：对表中的记录操作增删改查

Data Query Langeage(DQL数据查询语言)：对表中的记录查询操作

Data Control Langeage(DCL数据控制语言)：对用户权限设置

## 3、DDL操作数据库

### 3.1 创建数据库create

```sql
create database 数据库名[character set 字符集];
```

创建一个day16的数据库（默认字符集）

```sql
creat database day16;
```

创建一个day16_01的数据库（指定字符集为gbk）

```sql
creat database day16_01 character set gbk;
```

### 3.2 查看数据库show

查看所有数据库

```sql
show databases;
```

查看数据库的定义

```java
show create database 数据库名;
```

### 3.3 删除数据库drop

```sql
drop database 数据库名;
```

### 3.4 修改数据库alter

```
alter database 数据库名 character set 字符集;
不是修改数据库的名称，而是修改数据库使用的字符集
```

### 3.5 其他操作

1. 切换（使用）数据库

```sql
use 数据库名;
```

2. 查看正在使用的数据库

```
select database();
当前若是没有使用任何数据库，则返回 NULL
```

## 4、DDL操作表

### 4.1 创建表creat

语法：

```sql
create table 表名(
    字段名 字段类型[约束],
    字段名 字段类型[约束],
    ...
    字段名 字段类型[约束]  // 最后一个不写逗号
);
```

### 4.2 数据类型

#### 4.2.1 字符串类型

| 类型          | 说明                                                         |
| :------------ | ------------------------------------------------------------ |
| CHAR（size）  | 用于表示固定长度的字符串，该字符串可以包含数字、字母和特殊字符。size 的大小可以是从 0 到 255 个字符，默认值为 1。 |
| VARCHAR(size) | 用于表示可变长度的字符串，该字符串可以包含数字、字母和特殊字符。size 的大小可以是从 0 到 65535 个字符。 |
| TEXT（size）  | 表示一个最大长度为 65,535（216-1）的字符串文本，也即 64KB。  |
| TINYINT       | 带符号的范围是-128-127，无符号0-255                          |
| SMALLINIT     | 2的16次方                                                    |

#### 4.2.2 整数类型

| 类型   | 范围（有符号与无符号）                               | 说明   |
| ------ | ---------------------------------------------------- | ------ |
| INT    | (-2 147 483 648, 2 147 483 647)， (0, 4 294 967 295) | 整数   |
| BIGINT | (-263, 263-1)， (0, 264-1)                           | 大整数 |

#### 4.2.3 布尔类型

| 类型            | 说明                                                 |
| --------------- | ---------------------------------------------------- |
| BOOL（BOOLEAN） | 只有true与false两个有效值，0被认为是false，非0是true |

#### 4.2.4 小数类型

| 类型   | 说明   |
| ------ | ------ |
| DOUBLE | 双精度 |
| FLOAT  | 单精度 |

#### 4.2.5 日期和时间型

| 类型     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| Date     | 以'YYYY-MM-DD'格式显示Date类型，任何标点字符都可以用作日期部分之间的分隔符。例如，'2012-12-31'、'2012/12/31' |
| DateTime | DATETIME类型是Date和Time的组合，格式为“YYYY-MM-DD hh:mm:ss”或“YY-MM-DD hh:mm:ss”字符串。任何标点字符都可以用作日期部分或时间部分之间的分隔符。例如，'2012-12-31 11:30:45'、'2012^12^31 11+30+45' |

1. 整型一般用int或者bigint

2. 字符串：VARCHAR

   ​	固定长度：name char（20）：最大能存20个字符，就算是’aaa‘都是占20个字符

   ​	可变长度：name varchar（20）：最大能存20个字符，’aaa‘是占3个字符

3. 大文件：一般很少在数据库中存文件的内容，一般是存文件的路径

4. 日期：

   ​	DATA：只有日期

   ​	DATATIME：有日期和时间

### 4.3 约束

规则，限制

作用：保证用户插入的数据保存到数据库中是符合规范的

| 约束     | 约束关键字     |
| -------- | -------------- |
| 主键     | primary key    |
| 唯一     | unique         |
| 非空     | not null       |
| 自动增长 | auto_increment |

not null ：非空，username varchar(40) not null，表示这个字段不能为空，必须要有数据

unique：**唯一约束，后面的数据不能和前面重复**，cordNo char(18) unique，表示这个字段不能出现重复的数据

primary key：主键约束，一个字段若想称为主键，**必须非空且唯一**，一般用在表的id上，一张表基本上都有id

auto_increment：自动增长，必须是设置了primary Key之后，才可以使用auto_increment

**注意：**

先设置**primary key再设置auto_increment**

### 4.4 练习

练习：创建一张表

```sql
create table teacher(
	id int primary key auto_increment,
	name varchar(20) not null,
	sex boolean not null,
	age int
);
```

### 5.5 查看表show & desc

查看当前数据库所有的表

```sql
SHOW TABLES;
```

查看表的定义结构

```sql
DESC 表名;
```

### 5.6 修改表alter

```sql
增加列：ALTER TABLE 表名 ADD 字段 类型 约束;
	alter table 表名 add 字段名 类型 修饰 after 某列【把新列加在某列后面】
	alter table 表名 add 字段名字 类型 参数 first【把新列加在最前面】

修改列的类型与约束：ALTER TABLE 表名 modify 字段 类型 约束;

修改列的名称，类型，约束：ALTER TABLE 表名  CHANGE 旧列 新列 类型 约束;

删除列：ALTER TABLE 表名 drop 列名;

修改表名：rename table 旧表名 to 新表名;
```

### 5.7 删除表drop

语法：

```sql
drop table 表名; 
	一般都不会轻易删除表
```

## 6、DML操作表记录---增删改

### 6.1 增加记录insert into

新建一个表

```sql
create table product(
	pid int primary key auto_increment,
	paname varchar(20),
	price double,
	num int
);
```

插入记录

两种方式插入记录

```sql
insert into 表名(列，列) values(值，值);
例如：
pname price
insert into product(pname, price) values("mac", 1000);
```

插入所有的列

```sql
INSERT INTO product VALUES(NULL, 'ipad', 5444.5, 10);
INSERT INTO product VALUES(NULL, 'HUAWEI', 5442, 20);
INSERT INTO product VALUES(NULL, 'XiaoMi', 5644, 30);
```

### 6.2 更新记录update set

```sql
update 表名 set 列=值，列=值[where 条件]
```

```sql
将所有商品的价格修改为5000
UPDATE product set price = 5000;

将ipad的价格修改为5400
UPDATE  product set price = 5400 WHERE paname = 'ipad';

将iPad的价格修改为5500，数量修改为25
UPDATE product set price = 5500, num = 25 WHERE paname = 'ipad';

将HUAWEI的价格在原有的基础上打8折
UPDATE product set price = price * 0.8 WHERE paname = 'ipad';
```

### 6.3 删除记录delete

delete删除

```sql
delete from 表名[where 条件]
```

```sql
删除XiaoMi
DELETE FROM product WHERE paname = 'XiaoMi';

DELETE FROM product WHERE price < 5000;

不加条件删除所有
DELETE FROM product;
```

truncate删除

```sql
truncate table 表名;
TRUNCATE TABLE product;
```

delete与truncate的区别：

1. delete删除表中的数据，表结构还在，以前已经使用过的id数据编号不能使用
2. truncate删除表中的数据，并且表的结构已经不存在，就代表以前使用过的id重新开始编号

## 7、DQL操作表记录---查询

### 7.1 单表查询

#### 7.1.1 简单查询select

1. 查询所有列的记录

语法：

```sql
select * FROM 表名;

SELECT pid, paname, price, num FROM product;
```

2. 去重查询

```sql
去重查询
SELECT DISTINCT price FROM product;
```

3. 别名查询

```sql
select 列名 as 列名的别名，列名 from 表; // as可以不写

查询商品名称和商品价格,商品中price通过价格来显示
SELECT paname, price as 价格 from product;
```

4. 运算查询--加减乘除

```sql
SELECT paname，price+10 FROM product;
```

#### 7.1.2 条件查询

```sql
select... from 表 where 条件;
// 取出表中的每条数据，满足条件的记录就返回，不满足条件的记录就不返回
```

1. between ....and..区间查询

```sql
eg: where price between 1000 and 5000;
```

2. in(值，值)

```sql
SELECT * FROM product Where pid = 2;
SELECT * FROM product WHERE pid IN(2, 4);
```

3. 模糊查询 like

```sql
_：占一位
%：占0位n位
```

```
where name like '张%; 查询姓张的用户，名字的字数没有限制
where name like '张_';查询姓张的用户，名字是两个字的
```

4. and多条件查询

```sql
where 条件1 and 条件2 and 条件3;
```

5. or任意条件查询

```sql
where 条件1 or 条件2 or 条件3;
```

## 8、练习

```sql
create table tb_product(
	pid int primary key auto_increment,
	pname varchar(20) not null,
	price double not null,
	num int
);

1.查询商品价格>3000的商品
select pid, pname, price, num from tb_product where price > 3000;

2.查询pid=1的商品
select pid, pname, price, num from tb_product where pid = 1;

3.查询pid<>1的商品
select pid, pname, price, num from tb_product where pid > 1;
select * from tb_product where pid < 1; 

4.查询商品价格再3000到6000之间的商品
select pid, pname, price, num from tb_product where price between 3000 and 6000;

5.查询id是5，7，9，11的商品
select pid, pname, price, num from tb_product where pid in(5, 7, 9, 11);

6.查询商品以iph开头的商品
select pid, pname, price, num from tb_product where pname like 'iph%';

7.查询商品价格大于3000并且数量大于25的商品
select pid, pname, price, num from tb_product where price > 3000 and num > 25;

8.查询id=9或者价格小于3000的商品
select pid, pname, price, num from tb_product where pid = 9 or price < 3000;
```


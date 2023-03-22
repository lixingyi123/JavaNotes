<p align = "center" ><font size = 10， color = "#009999">mysql进阶2</font></p>

## 1、单表查询

先建立一个表

### 1.1 排序查询 order by

语法：

```sql
select 字段，from 表名 order by 列1 asc|desc [，列2 asc|desc];
asc:从小到大，升序排序，不使用时默认升序
desc:从大到小，降序排序

语法说明：
先按照列1进行升/降排序，如果列1相同，再按照列2进行升/降排序，以此内推
```

### 1.2 聚合排序 (聚合函数)

**注意：聚合函数会忽略null，不进行计算**

| 聚合函数      | 作用                                                         |
| ------------- | ------------------------------------------------------------ |
| max（列名）   | 求这一列的最大值                                             |
| min（列名）   | 求这一列的最小值                                             |
| avg（列名）   | 求这一列的平均值                                             |
| count（列名） | 求这一列有多少条记录，count不会计算为空的值，所以查找是使用非空列进行查找 |
| sum(列名)     | 求这一列的总和                                               |

练习：

1.求学生表中score的最大值，最小值，平均值，总和以及表中数据的数量

```sql
select max(score) from tb_student;

select min(score) from tb_student;

select avg(score) from tb_student;

select count(id) from tb_student;

select sum(score) from tb_student;
```

### 1.3 分组查询 group by

语法：

```sql
select 字段1，字段2，字段3... from 表名 [where 条件] GROUP BY 列 [having 条件];
```

```sql
select sex,count(id) from tb_student group by sex;
```

分组后筛选HAVING

```sql
根据性别分组，统计每组的总人数
select sex, count(id) from tb_student group by sex count(*) > 5;
```

==注意事项：==

1.单独分组，没有意义

2.分组的目的一般是做统计使用，经常与聚合函数一起使用

where与having的区别

| 子句   | 作用                                                         |
| ------ | ------------------------------------------------------------ |
| where  | 对查询结果进行分组时，将部分和where条件的行去掉，在分组前过滤数据，**就是先过滤后分组** |
| having | 先分组后过滤                                                 |

### 1.4 分页查询

limit是限制，所以limit的作用限制查询记录的条数，经常用来做分页查询

语法：

```sql
limit a, b
a:代表其实行数，不包含第a行
b:每一页查询的行数

例子：
分页查询学生，每一页查询4条
limit: 0(代表跳过0行), 4（代表4条）;
select name, sex, score from tb_student limit 0, 4;

b = 4;
a = (当前页数 - 1) * b
```

## 2、多表查询

### 2.1 为什么要有多表

多表：如果表中出现了很多重复数据（造成数据冗余），可以将一张表分成多个表进行处理

解决：员工与部门，将一张表分为员工表与部门表

```sql
# 创建员工表，里面有id，姓名，性别，年龄，入职时间
create table employee(
	id int primary key auto_increment,
    name varchar(20),
    sex char,
    age int,
    join_date date,
    dep_id int
);

# 创建部门表，有id，部门名称，base
create table department(
	id int primary key auto_increment,
    name varchar(20),
    base varchar(20)
);


# 为员工表添加信息
insert into employee values(null, '汪洋', '男', 34, '2019-08-09', 1);
insert into employee values(null, '汪涵新', '女', 32, '2017-06-07', 1);
insert into employee values(null, '汪涵', '女', 45, '2013-07-20', 1);
insert into employee values(null, '李毅洋', '男', 50, '2010-02-23', 1);
insert into employee values(null, '许涵曦', '女', 24, '2020-09-10', 2);
insert into employee values(null, '车帅', '男', 25, '2022-09-18', 1);
insert into employee values(null, '韩新月', '女', 56, '2007-05-08', 2);
insert into employee values(null, '张译', '男', 60, '2000-01-01', 2);

# 为部门表添加信息
insert into department values(null, '开发部', '北京');
insert into department values(null, '销售部', '深圳');
```

### 2.2 外键约束

**作用：**用来维护多表之间的关系

**外键：**一张从表中的某个字段引用主表中的主键

​	**主表：约束别人**

​	**从表：使用别人的数据，被别人约束**

### 2.3 外键语法

#### 2.3.1 添加外键

```sql
1.新建表时增加外键
[constraint] [外键约束名称] foreign key(外键字段名) references 主表名(主键名字段);

constraint :约束关键字
foreign key(外键字段名)：某个字段作为外键
references 主表名(主键字段名):表示参照主表中的某个字段

例如：将employee作为从表设置外键
create table employee(
	id int primary key auto_increment,
    name varchar(20),
    sex char,
    age int,
    join_date date,
    dep_id int,
    constraint emp_dep_fk foreign key(dep_id) references department(id)
)

2.已有表添加外键
alter table 从表 add [constraint] [外键约束名称] foreign key(外键字段名) references 主表名(主键名字段);

例如：为已经存在的表添加外键
create table employee(
	id int primary key auto_increment,
    name varchar(20),
    sex char,
    age int,
    join_date date,
    dep_id int
)
alter table employee add constraint emp_dep_fk foreign key(dep_id) references department(id);
```

#### 2.3.2 删除外键

```sql
删除外键
alter table 表名 drop foreign key 外键名称

例如：
删除员工表中的外键
alter table employee drop foreign key emp_dep_fk;
```

#### 2.3.3 外键的级联（了解）

```sql
外键的级联
on update cascade:级联更新，主键发生更新时，外键也会更新
on delete cascade:级联删除，主键发生删除时，外键也会删除

例如：
create table employee(
	id int primary key auto_increment,
    name varchar(20),
    sex char,
    age int,
    join_date date,
    dep_id int,
    constraint emp_dep_fk foreign key(dep_id) references department(id) on update cascade on delete cascade
)
```

## 3、多表间关系

### 3.1 一对多

班级和学生，部门与员工，客户与订单

一的一方：班级，部门，客户

多的一方：学生，员工，订单

**一对多建表原则：将多的一方设置为从表，少的一方设置为主表**，在从表中设置一个字段，字段作为外键指向主表的主键

### 3.2 多对多

老师和学生，学生与课程

一个老师可以有多名学生，一门课程可以被多名学生选择

一个学生可以有多名老师，一位学生可以选择多门课程

**多对多建表原则：**需要创建第三张表，中间表至少有两个字段，这两个字段分别作为外键指向各自一方的主键

### 3.3 一对一

一般不使用，因为可以直接只创建一个表就能解决问题

### 3.4 练习

需求：完成一个学校的选课系统，系统包括班级，学生，课程

```sql
# 创建班级表
create table class(
	class_id int primary key auto_increment,
	class_name varchar(20)
);

# 创建学生表
create table student(
	student_id int primary key auto_increment,
	student_name varchar(20),
	c_id int,
	constraint student_class_fk foreign key(c_id) references class(class_id)
);

# 创建课程表
create table course(
	course_id int primary key auto_increment,
    course_name varchar(20)
)

# 创建一个新表维护学生与课程
create table stu_co(
	sno int,
    cno int,
    constraint student_course_fk1 foreign key(sno) references student(student_id),
    constraint student_course_fk2 foreign key(cno) references course(course_id)
)
```

## 4、连接查询

### 4.1 交叉查询

把若干张表没有条件的连接在一起，进行展示

左表的每条数据和右表的每条数据组合，这种效果称为笛卡尔积

交叉查询产生的结果不是我们想要的

### 4.2 内连接查询

#### 4.2.1 隐式内连接

```sql
select * from 表名1，表名2 where 表名1.字段名 = 表名2.字段名;

例子：查询员工（员工表，employee）的id，姓名，性别，薪资，加入日期。所属部门是另一个表（department表）
select employee.id, employee.`name`, employee.sex, employee.salary, employee.join_date, department.`name` from employee, department where employee.dept_id = department.id;
```

#### 4.2.2 给表名取别名

```sql
select e.id, e.`name`, e.sex, e.salary, e.join_date, d.`name` from employee e, department d where e.d_id = d.id;
```

#### 4.2.3 显式内连接

```sql
select * from 表名1 [INNER] join 表名2 on 连接条件[where 其他条件];
INNER JOIN 关键字表示表中存在至少一个匹配时，inner join 关键字返回inner join与join是相同的
```

```sql
select * from employee INNER JOIN department on employee.dep_id = department.id
select * from employee INNER JOIN department on employee.dep_id = department.id where employee.id = 2
select * from employee JOIN department on employee.dept_id = department.id where employee.id = 2
```

```sql
查询所有部门下的员工信息，如果该部门下没有员工则不展示

隐示
select * from employee e,department d where e.dep_id = d.id;
显示
select * from  department d inner join employee e on e.dep_id = d.id;
```

1. 内连接的特点

   ​	查询的是公共部分，满足连接条件的部分

2. 使用内连接的关键点

​			使用主外键作为条件去除无用信息

​			显示内连接里面on只能主外键关系作为条件，如果还有其他条件，后面加where

### 4.3 外连接

#### 4.3.1 左外连接

语法：

```sql
select [字段]/[*] from 表名1 left join 表名2 on 条件;

# 以join左边的表作为主表，显示主表中的所有数据，根据条件查询连接右边的表的数据，满足条件则展示，不满足条件则显示null

例子：查询所有部门下的员工
select * from department d left join employee e on e.dep_id = d.id;
```

####  4.3.2 右外连接

语法：

```sql
select * [字段]/[*] from 表名1 right join 表名2 on 条件;

# 以join右边的表作为主表，显示主表中的所有数据，根据条件查询连接左边的表的数据，满足条件则展示，不满足条件则显示null

例子：查询所有员工对应的部门
select * from department right join employee on employee.dep_id = department.id; 
```

#### 4.3.3 内连接与外连接的应用

```
例子：用户与订单n
 1.查询所有用户的订单信息 有些用户可能没有下订单，没下的订单用null表示 用外连接
 2.查询下单的用户的信息   用户一定下过订单，不存在没有下单的情况，用内连接
 
 例子：用户与账户
 1.查询所有用户的账户信息  有些账户没有开，有可能微信是null，用外连接
 2.查询所有用户的开户信息  账号信息一定存在，所以用内连接
```

## 5、子查询

一个**查询语句里面至少包含两个select**，一个查询解决不了问题

**一个查询语句的结果作为另一个查询语句的条件**，有查询的嵌套

内部的查询称为子查询，子查询要使用括号，子查询的结果三种情况

1. 子查询的结果是一个值的时候

```sql
查询工资最高的员工是谁
1.查询最高工资是多少
select max(salary) from emp;
2.再查询最高工资对应的员工是谁
select * from emp where salary = (select max(salary) from emp);

```

2. 子查询的结果是单列多行

```sql
查询工资大于5000的员工所在的部门的名字
select dept_id from emp where salary > 5000;
再根据部门的id查询部门名称
select dept.`name` from demp where dept.id in(select dept_id from emp where salary > 5000);
```

3. 子查询的结果是多行多列

```sql
查询出2011年以后入职的员工信息，包括部门名称
1. 先查2011年以后入职的员工
select * from emp where join_date > '2011-01-01';
2. 查询所有的部门信息，与上面的虚表中的信息组合，找出所有部门的id等于dept_id的信息
select * from dept d, (select * from emp where join_date > '2011-01-01') e where e.dept_id = d.id;
```


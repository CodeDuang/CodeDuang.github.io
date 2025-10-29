# [SQL]mysql学习笔记（连载中）

学习视频：[【数据库】SQL 3小时快速入门 #数据库教程 #SQL教程 #MySQL教程 #database#Python连接数据库
](https://www.bilibili.com/video/BV1PT4y1e7UU/?spm_id_from=333.1007.top_right_bar_window_custom_collection.content.click&vd_source=e50f352f1c6366bbfab82c566af2e7c2)


# 0.MySQL命令速查
## 0.1.database、table、column、value不同层级增删改查
| --- | --- | --- | 
|  | 增 | 删 | 改 | 查 | 
| database | create | drop |  | show |    
| table | create | drop |  | select * |  
| column | alter+add  | alter+drop |  | describe |  
| value | insert | delete | update | where |  

# 1.SQL的基础知识
## 1.1.表(table)和键(key)
一个表的基本形式如下：

![image_30.png](image_30.png)

Employee是`表名`，第一行的每个元素称之为`属性`or`键`，每张表一定包含一个`主键`（primary key）,主键的作用是唯一标识每一行。

## 1.2.外键、联合主键

![image_31.png](image_31.png)

**外键**：上图的Employee表有两个绿色的属性：branch_id、sup_id，是用来连接的Branch表和自身表的`外键`（外键一定是其他表的主键），外键可以抽象理解为一个单箭头（这个箭头由Employee表出发可以指向任意表包括自己，但一定是被指表的主键），Employee表的branch_id可以用来检索Branch表的特定一行，但反过来Branch表无法通过其反检索。

**联合主键**：上图Works_With表的`联合主键`为emp_id和client_id，因为两个属性单独都没办法唯一表示每一行，但二者合起来可以唯一表示每一行。需要注意的是，联合主键并不是代表该表有很多主键，Works_With表依然还是只有一个主键，只不过这个主键是联合主键，由两个属性构成。

# 2.MySQL安装（略，请自行参考视频）

# 3.基本的MySQL语法
## 3.1.规则与约定

### 3.1.1.MySQL中的关键词不区分大小写
MySQL中的关键词不区分大小写，如
```sql
CREATE DATABASE `sql_tutorial`;
```
也可以写为
```sql
create database `sql_tutorial`;
```
### 3.1.2.非关键词部分，尽量使用\``括起来，防止被误认为关键词
非关键词部分，尽量使用\``括起来，防止被误认为关键词，如：
```sql
CREATE DATABASE database;
```
上面的写法会让MySQL误认为你的database是关键词，实际上你只是想要创建一个名为database的数据库，应该写为：
```sql
CREATE DATABASE `database`;
```

### 3.1.3.每一行命令以;作为结尾
### 3.1.4.创建语句不重复执行，区分其他编程语言
MySQL使用CREATE创建了一个数据库后，数据库就一直存在了（所有指令都会永久修改数据库状态，并不会因为指令执行结束而重置数据库），有新的指令加入，不需要全部指令再执行一次（与编程语言不同的地方），应当只执行新增部分（或仅执行基于上次sql语句执行后的状态，所需要执行的操作）

# 4.SQL数据库操作
##  4.1.数据库相关命令（创建、查询、删除）
### 4.1.1.创建数据库：
```sql
CREATE DATABASE `sql_tutorial`;#新建名为`sql_tutorial`的数据库
```
### 4.1.2.展示数据库：
```sql
SHOW DATABASES;#展示所有数据库
```
### 4.1.3.删除指定数据库：
```sql
DROP DATABASE `sql_tutorial`;#删除名为`sql_tutorial`的数据库
```
### 4.1.4.选择（进入）数据库指定数据库：
```sql
USE `sql_tutorial`;#进入该数据库（一般是要操作某个数据库的表格的时候使用）
```
##  4.2.表格相关命令（创建、查询、删除、修改）
### 4.2.1.创建表格（请先使用USE命令选择数据库，否则会报错）：
```sql
CREATE TABLE `student`( #新增`student`表格，注意最后一个属性末尾不需要逗号，且符号"）"后面需要跟符号";"
	`id` INT PRIMARY KEY,  #PRIMARY KEY标注主键
    `name` VARCHAR(10),
    `major` VARCHAR(10)
    #PRIMARY KEY(`id`) #假如没有在属性后面标注是主键，可以使用这种方式设定主键
);
```
创建表格的代码可以分解为：主体+属性
主体部分：

```Bash
CREATE TABLE `[表格名]`(
	...
	属性部分
	...
);
```
属性部分：
```Bash
`[属性a]` [类型名],
`[属性b]` [类型名],
...
`[属性n]` [类型名],
PRIMARY KEY(`[主键名]`)
```
MySQL中可选的类型名有：
`INT`：整数
`DECIMAL(x,y)`：小数，有x位其中小数点后有y位
`VARCHAR(n)`：字符串，长度为n个字节
`BLOB`：Binary Large Object二进制数据（图片、影片、档案...）
`DATE`：“YYYY-MM-DD”日期，eg：2021-08-08
`TIMESTEMP`：时间，比日期更精确到秒，“YYYY-MM-DD HH:MM:SS”

### 4.2.2.查看表格属性：
```sql
DESCRIBE `student`; #查看`student`表格的属性情况
```
### 4.2.3.删除表格：
```sql
DROP TABLE `student`;#删除`student`表格
```
### 4.2.4.新增表格属性：
```sql
ALTER TABLE `student` ADD `gpa` DECIMAL(3,2); #`student`表格新增属性gpa，类型为3位小数，其中2位小数位
```
### 4.2.5.删除表格属性（列）：
```sql
ALTER TABLE `student` DROP COLUMN `gpa`; #`student`表格删除gpa列
```
### 4.2.6.表格constraints(属性限制) ：
`NOT NULL`：
`DEFAULT`：
`AUTO_INCREMENT`：自增（总是以该属性最大的那一个为标准自增）
`UNIQUE`：


##  4.3.数据写入相关命令
### 4.3.1.查看表格全部内容：
```sql
SELECT * FROM `student`; #查看表格内容（以4.2.1创建的表格为目标，结果如下图）
```

![image_32.png](image_32.png)

### 4.3.2.插入一条数据（以4.2.1创建的表格为目标）：
```sql
INSERT INTO `student` VALUES(4,"小红","数学"); #插入数据（结果如下图）
```

![image_33.png](image_33.png)

```sql
INSERT INTO `student`(`major`,`name`,`id`) VALUES("英语","小红",5); #插入数据(指定属性的顺序)（结果如下图）
```

![image_34.png](image_34.png)

```sql
INSERT INTO `student`(`major`,`id`) VALUES("政治",6); #插入数据(指定属性的顺序，未出现的属性，自动赋值NULL)（结果如下图）
```

![image_35.png](image_35.png)

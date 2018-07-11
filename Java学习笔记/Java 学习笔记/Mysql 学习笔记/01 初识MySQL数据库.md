## 一、MySQL 的客户端:
```
1, Navicate
2, sqlyog
3, HeidiSQL
```

## 二、操作数据库
```
//1、登录数据库
mysql -uroot -p

//2、修改密码
set password for root@localhost=password('1234');

//3、刷新
flush privileges;
```

## 三、了解数据库
```
//1、查看所有的数据库
show database;

//2、查看数据库的字符集
show variables like 'character_set%';
    //修改字符集的方法

    //第一步：
    //停止MySQL服务
    //Net stop mysql
    
    //第二步：
    //修改  my.ini 文件里面的配置信息
    //（没有 my.ini 文件的可以把 my_default.ini 文件复制改名为 my.ini）
    
    //第三步：
    //启动mysql 
    //net start mysql
```

```
Information_schema
提供了访问数据库元数据的方式。
元数据是关于数据的数据，如数据库名称、表名、列名、列的数据类型

Mysql
存储了系统用户信息、用户权限信息

Performance_schema 
提供进程等待的详细信息，包括锁、互斥变量、文件信息。
```

## 三、数据库语言

- 数据定义语言DDL（Data Definition language）

- 对保存数据的格式进行定义, 用于操作对和对象属性，这种对象包括数据库本身，以及数据库对象。比如：表、视图等等。

- DDL对这些对象和属性的管理和定义主要表现在create 、 drop 、alter。一个数据库模型包含该数据库中所有实体的描述定义

```
//1、创建数据库
Create database dbname;

//2、使用数据库
Use dbname;

//3、删除数据库
Drop database dbname;

说明：
auto_increment  自增长,初始值为1,每插入一行，自动加一
comment         当前字段的定义说明,备注
default         指定默认值
primary key     指定主键
Engine = innodb 指定数据库引擎
default charset=utf8 指定编码
not null/nill   不能为空/可以为空

//4、创建表
create table person_info(
    person_id int not null auto_increment, 
    name varchar(50) not null comment '人名', 
    country varchar(30) default 'China' not null,
    account decimal(10,2) default 0.00 comment '账号',
    primary key(person_id)
)engine = innodb default charset=utf8;

//5、查看表结构
Desc table_name;

//6、创建结构相同的表
Create table table_name like table_name1;

//7、修改表的名称
Alter table old_table_name rename to new_table_name;

//8、查看当前库所有的表
Show tables;

//9、修改字段的类型
Alter table table_name modify column_name column_definition [first|after] conlumn_name;

//10、增加字段
Alter table table_name add column_name column_definition [first|after] column_name;

//11、删除字段
Alter table table_name drop column_name;

//12、修改字段的名称
Alter table table_name change old_cloumn_name new_column_name column_definition [first|after] column_name;

```

```
//1、数据库操作(管理)语言, DML(Data management language)

//2、插入 Insert
    insert into person_info (person_no,country,name,account) values(1,'China','隔壁老王',500);
    insert into person_info (person_no,country,name,account) values(2,'China','砖石王老五',1000);
    insert into person_info (person_no,country,name,account) values(3,'China','李刚',1500.5);

//3、查询 Select
    select * from person_info;

//4、修改 Update
    update set account = 10000.55 person_no = 2;

//5、删除 Delete
    delete from person_info where person_no = 4;
```
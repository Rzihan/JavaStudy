---
### 常用的数据类型

- 整数型的 tinyint 和 bigint
- 小数型的 decimal
- 日期时间类型的 datetime 和 timestamp
- 字符串类型是 char 和 varchar

---
### 数字型
```
create table tb1_int(
    a tinyint unsigned,
    b tinyint
);

insert into tb1_int values(255,127);    //插入成功
insert into tb1_int values(256,128);    //a列超出范围
insert into tb1_int values(0,128);      //b列超出范围

//zerofill  通过规定数据的显示宽度，达到统一显示的目的

alter table tb1_int add c tinyint(3) zerofill;

insert into tb1_int values(0,127,1);
insert into tb1_int values(0,127,5);
insert into tb1_int values(0,127,7);
```
---
### 小数型
```
//单精度 float[(M,D)] [unsigned] [zerofill]
//双精度 double[(M,D)] [unsigned] [zerofill]
//其中 M 表示总的位数,D表示小数位数

create table num_1(
    a float,
    b double
);

insert into num_1 values(1234567890.0123456789,123456789.0123456789);


//decimal 定点数型
定点数
decimal[(M[,D])] [unsigned] [zerofill]
其中M表示总的位数，D表示小数位数。

create table num_2(
    send_money decimal(6,2)
);

insert into num_2 values(9999.99);
```
---

### 日期时间类型
```
create table dt_1(
    a datetime,
    b timestamp
);

insert into dt_1 values('2018-4-19 16:58:59',now());
```

---
### 字符类型
* char 和 varchar 类型声明的长度表示你想要保存的最大字符数
* char(5) varchar(5)
```

//在枚举类型中我们只能插入写好的内容
create table s_8(
    gender enum('boy','girl')
);

insert into s_8 values('girl');
insert into s_8 values('boy');

insert into s_8 values('other');

//set是一个集合类型!(注意：在set类型中,我们可以多选)
create table s_6(
    hobby set('A','B','C','D')
);

insert into s_6 values('A');

insert into s_6 values('B,C');
```
---

### 设计数据类型要考量
- 1、使用最精确的类型，占用最少的空间
    - (现在考虑少了一位磁盘便宜了)
- 2、还应该考虑到相关语言处理方便性
    - (像我们用的是Java语言,要考虑在Java中有对应类的类型)
- 3、考虑移植的兼容性
    - 我们现在用Mysql来存储数据,万一要把数据移到oracle数据库呢
    

---
* Java中的boolean类型，在数据库中可以用bit，tinyint(1)，来存储，0对应false 1对应true
* tingint，int对应Java中的int
* bigint对应Java中的long
* blob 对应Java byte[]
* enum 对应Java Enum枚举类型
* set 对应Java set类型
* char varchar text 对应Java String
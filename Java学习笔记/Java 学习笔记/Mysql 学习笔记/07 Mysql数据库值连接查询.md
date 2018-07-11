### 一、连接查询

* 1、笛卡尔积 ：就是两个集合中的元素可能存在的所有组合方式而形成的新的集合！
* 代码演示
```
CREATE TABLE ONE(
    one_id INT,
    one_date CHAR(1),
    public_field INT
);

INSERT INTO ONE VALUES(1,'a',10),(2,'b',20),(3,'c',30);

CREATE TABLE two(
    two_id INT,
    two_date CHAR(1) NOT NULL DEFAULT 't',
    public_field INT
);

INSERT INTO two VALUES(2,'B',20),(3,'C',30),(4,'D',40);

//测试笛卡尔积
SELECT one.*,two.* FROM ONE,two;

```

* 2、内连接查询
* 只有在连接的表内数据都存在的情况下，才会做连接。内连接是把二个表连接成一个结果集，在这个结果集中仅包含哪些满足条件的记录行
* 代码演示
```
select * from tableA,tableB where tableA.column=tableB.column;
select * from tableA inner join tableB on tableA.column=tableB.column;
select * from tableA cross join tableB on tableA.conlumn=tableB.column;

//测试
SELECT one.*,two.* FROM ONE,two WHERE one.one_id = two.two_id;
SELECT one.*,two.* FROM ONE INNER JOIN two ON one.one_id = two.two_id;
SELECT one.*,two.* FROM ONE CROSS JOIN two ON one.one_id = two.two_id;
```

* 3、外链接查询
* 如果存在不能匹配的数据，也会进行连接，不过此时mysql会帮我们虚拟一条不存在的记录，字段值都是为null，帮助我们完成整个连接记录。
* 分为
  * 左外链接
    * left join on ,left outer join on;
    * 语法： select * from tableA left join tableB on tableA.column=tableB.column
  * 右外链接
    * right join on,right outer join on;
    * 语法： select * from tableA right join tableB on tableA.column=tableB.column
* 代码演示
```
SELECT one.*,two.* FROM ONE LEFT JOIN two ON one.one_id = two.two_id;
SELECT one.*,two.* FROM ONE LEFT JOIN two ON one.one_id = two.two_id WHERE two.`two_id` IS NULL;
SELECT one.*,two.* FROM ONE RIGHT JOIN two ON one.one_id = two.two_id;
SELECT one.*,two.* FROM ONE RIGHT JOIN two ON one.one_id = two.two_id WHERE one.`one_id` IS NULL;
```
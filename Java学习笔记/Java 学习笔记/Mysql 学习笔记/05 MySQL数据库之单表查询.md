
* 算术运算符 （+  -   *  /  %）
* 比较运算符  =  >   <  <>或!=   >=   <=  is null,  is not null

---

```
//字段别名，表的别名
column ad aliasname tablename as aliasname

select catagory_id as id,name,sort_order as sort,description as des from category as cat;
//注意：别名不能用关键字
```

---

### 关键字
```
//in 和 not in
select * from table_name where 条件  in(元素1, 元素2,....);
select * from table_name where 条件not  in(元素1, 元素2,....);

//between ... and ...
select * from  table_name where 条件 between 取值1 and 取值2;
select * from  table_name where 条件 not between 取值1 and 取值2;

//and   可以联合多个关键字查询
select * from table_name where 条件1 and 条件2

//or 关键字
select * from table_name where 条件1 or 条件2

//like 关键字模糊查询，有二种通配符 %  和  _
select * from category where name like '%机';
select * from category where category_id like '_000';

//having 关键字
//除了满足 where 后面的查询条件，还需要满足 having 后面的第二条件。
select * from category where category_id > 1005 having sort_order = 3;

//order by  可以对查询的结果进行升序(asc)和 降序(desc) 排列
select * from category order by sort_order asd;
select * from category order by sort_order desc;

//limit 关键字限定结果行数，控制输出的行数
//limit n;  n :代表输出的个数
//limit m, n; n 代表输出的个数， m 代表起始位,即是查询记录从m+1开始
```
---
## 例子
```
SELECT sid AS id ,sname AS our_name,gender FROM students AS s;

SELECT * FROM students WHERE gender IN ('男');
SELECT * FROM students WHERE gender NOT IN ('男');

SELECT * FROM students WHERE sid > 3117001001 AND sid < 3117001005 ;
SELECT * FROM students WHERE sid > 3117001002 AND gender = '男' ;
SELECT * FROM students WHERE sid > 3117001002 OR gender = '男' ;

SELECT * FROM students WHERE sname LIKE '_李';
SELECT * FROM students WHERE sname LIKE '老%';
SELECT * FROM students WHERE sname LIKE '老%' HAVING address = "广东广州";

SELECT * FROM students ORDER BY sid ASC;
SELECT * FROM students ORDER BY sid DESC;

SELECT * FROM students ORDER BY sid DESC LIMIT 4 ;
SELECT * FROM students ORDER BY sid ASC LIMIT 4;
SELECT * FROM students LIMIT 4,2;
SELECT * FROM students LIMIT 2,4;
```
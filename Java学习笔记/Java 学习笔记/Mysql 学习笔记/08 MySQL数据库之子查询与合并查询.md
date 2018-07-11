### 一、子查询
- 子查询的分类：

    - 类型一（根据子查询的返回值）：
        - 一个子查询会返回一个标量（单一值）,一个行， 一个列，一个表
        - 这些子查询被称为标量子查询，行子查询，列子查询，表子查询。
    
    - 类型二（根据子查询的出现条件语句）
        - where 子查询
        - from 子查询
    

```
SELECT id FROM t_booktype;
//带 in 关键字
SELECT * FROM t_book WHERE t_book.`bookTypeId` IN (SELECT id FROM t_booktype);

//带 比较运算符
SELECT * FROM t_book WHERE t_book.`price`>=(SELECT MAX(t_book_price.`price_label`) FROM t_book_price);
SELECT * FROM t_book WHERE t_book.`price`>=(SELECT MIN(t_book_price.`price_label`) FROM t_book_price);

//带Exists关键字
SELECT * FROM t_book WHERE EXISTS (SELECT MAX(t_book_price.`price_label`) FROM t_book_price);
SELECT * FROM t_book WHERE NOT EXISTS (SELECT MAX(t_book_price.`price_label`) FROM t_book_price);

//带All关键字的子查询
SELECT * FROM t_book WHERE t_book.`price`> ALL(SELECT t_book_price.`price_label` FROM t_book_price);

//带Any关键字的子查询
SELECT * FROM t_book WHERE t_book.`price`> ANY(SELECT t_book_price.`price_label` FROM t_book_price);
```


### 二、合并查询

- UNION
    - 使用UNION关键字，数据库系统会将所有的查询结果合并到一起，然后去除相同的记录
- UNION ALL
    - 使用UNION ALL，不会去除系统的记录
```
select id from t_book;
select id from t_booktype;

select id from t_book union select id from t_booktype;
SELECT id FROM t_book UNION all SELECT id FROM t_booktype;
```
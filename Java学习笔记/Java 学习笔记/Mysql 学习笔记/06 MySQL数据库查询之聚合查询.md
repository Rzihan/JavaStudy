```
//distinct
//去重，在结果中去除重复的行
select distinct column_names from 表名;

//作用于单列：
select distinct(order_id) from order_detail where id<30;

//作用于多列：
select distinct order_id, buy_number from order_detail where id<30;


//count 
//统计数量！
select count(id) from order_detail;


//concat(str1, str2, ...)
//连接函数，可以联合多列，构成一个总的字符串。

select contact(order_id, '-', product_id) from order_detail where id<30;


//group by 
//分组查询，对结果进行分组。通过 group by 子句可以将数据划分到不同的组里，实现对记录的分组查询。
//单独使用 group by 时，没什么实际意义！在与 avg() , sum(), count() 聚合函数一起使用时，作用最大。

max() 求表中某个字段最大值（数值类型）
min() 求表中某个字段最小值
sum() 求表中某个字段的总和
avg() 求表中某个字段平均值
```
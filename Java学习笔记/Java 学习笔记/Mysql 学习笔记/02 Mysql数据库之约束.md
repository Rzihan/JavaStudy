## 约束
* 约束是一种限制，它是通过对表的行或列的数据做出限制，来确保表和数据的完整性、唯一性和正确性。约束分为 5 种


```

//一、主键约束（primary key）
//主键要求这一行的数据不能重复且不能为空。
//创建表格

create table t_user(
    user_id int not null,
    user_name varchar(30) null comment '用户名称',
    password varchar(60) null,
    sex varchar(10) null comment '性别',
    mobile varchar(11) null comment '手机',
    birthday timestamp not null default CURRENT_TIMESTAMP,
    primary key(user_id)
);

//另一种添加主键的方式
alter table t_user add primary key(user_id);


//二、默认值约束（default）
//有default约束的列时，当插入数据为空时那么久插入该默认数据
//修改表 t_use 的默认值

alter table t_user modify sex varchar(10) default '男' not null;


//三、非空约束（not null）

    空格和 NULL 的区别：
    
    String s1 = ""; 空值
    创建出了对象（已经开辟了内存空间，对象已经实例化），这个对象内容为空，也就是空字符串。   
    s1.length = 0;       s1.isEmpty() = true;

    String s2 = "    "; 空格
    创建出了对象（已经开辟了内存空间，对象已经实例化），这个对象内容为不为空，而是空格。       
    s2.length = 1;        s2.isEmpty() = false;

    String s3 = null; 空对象
    还没创建出对象（未分配内存空间），值不存在。在调用所有对象方法时候都会抛出异常，如s3.length(), s3.isEmpty()等方法。
    
    
//四、唯一约束（unique） 可以为 NULL 不能重复！
//五、外键约束（foreign key）

    如果一个表的某个字段指向另一个表的主键，就称为外建。
    被指向的表，称之为主表，也叫父表
    指向的表，称之为从表，也叫子表
    
    //先来创建一张班级的表
    create table t_class(
        id int not null,
        class_name varchar(30) not null,
        primary key(id)
    );
    
    //再来创建一张学生表
    create table t_student(
        id int auto_increment not null,
        student_no char(4) not null,
        name varchar(16) not null,
        age smallint default 21 not null,
        class_id int not null,
        primary key(id),
        constraint stu_fk foreign key(class_id) references t_class(id)
    );
    
    //插入数据
    insert into t_class values(1,'网络工程1班');
    insert into t_class values(2,'网络工程2班');
    insert into t_class values(3,'网络工程3班');
    insert into t_class values(4,'网络工程4班');
    insert into t_class values(5,'网络工程5班');
    
    
    insert into t_student values(null,'1001','隔壁老大',21,1);
    insert into t_student values(null,'1002','隔壁老二',21,2);
    insert into t_student values(null,'1003','隔壁老三',21,3);
    insert into t_student values(null,'1004','隔壁老四',21,4);
    insert into t_student values(null,'1005','隔壁老五',21,5);
```
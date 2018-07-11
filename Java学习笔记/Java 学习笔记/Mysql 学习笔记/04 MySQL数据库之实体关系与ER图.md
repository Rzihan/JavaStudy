### 一、什么是数据库的设计

数据库设计(Database Design) 是指对于一个给定的应用环境，构造最优的数据库模式，建立数据库及其应用系统，使之能够有效地存储数据，满足各种用户的应用需求（信息要求和处理要求）。

---
### 二、数据库设计就可以理解为：
实体模型 ->概念模型->数据模型的过程。

---

### 三、实体关系模型
概念模型，即实体－关系模型。有三种成分：实体、关系、属性。在系统分析与设计的过程中，常用”E-R”图来表示。

#### 1、什么是实体（entity）?
- 标识数据库要管理的关键对象或实体
- 实体是名词：
- 学生、班级、年级、学校、用户、角色、菜单等等。
 ---

#### 2、 什么是属性（attribute） ?
- 标识每个实体的属性
- 用户实体下面的属性的：
- 登录名、用户名、密码、性别、头像、电话等。
- 角色实体下面的属性有：
- 角色名称、角色描述等。
 ---

#### 3、什么是关系（relationship ）?
- 标识对象之间的关系
- 用户和角色是主从关系：
- 需要表明用户对象属于哪个角色的。
- 学生和班级是主从关系：
- 需要表明学生对象属于哪个班级的。
---

### 三、三种关系模型
#### 1、一对一关系（1：1）
```
//如果对于实体集 A 中每一个实体，实体集 B
//中最多只有一个实体与之联系；
//反之对于实体集 B 中每一个实体，实体集 A //中也最多只有一个实体与之联系。
//我们称实体集 A 与实体集 B 之间具有一对一的联系。
//记为1:1，如下图
```

```
graph LR
A[班主任] --> |1| B{负责}
B{负责} --> |1| C[班级]
```
---
#### 2、一对多关系(1:n)
```
//如果对于实体集 A 中每一个实体，实体集 B 中有 n 个实体(n>=0)与之联系；
//反之对于实体集 B 中每一个实体，实体集 A 中最多只有一个实体与之联系。
//我们称实体集 A 与实体集 B之间具有一对多联系。记为1:n。
如下图所示：

```
```
graph LR
A[班级] --> |1| B{所属}
B{所属} --> |n| C[学生]
```
--- 
#### 3、多对多关系（M：n）
```
//如果对于实体集A中的每一个实体，实体集B中有n个实体（n>0）与之联系；反之对于实体集B中每一个实体，实体集A中也有m个实体（m>=0）与之联系。我们称实体集A与实体集B之间具有多对多联系。记为m：n，如下图所示
```
```
graph LR
A[学生] --> |m| B{学习}
B{学习} --> |n| C[课程]
```

### 四、E-R图遵循应以下原则
1. 首先针对特定用户的应用，确定实体、属性和实体间的联系，做出反映该用户视图的局部 E-R 图
2. 综合各个用户的局部 E-R 图，产生反映数据库整体概念的总体 E-R图。在综合时，删掉局部 E-R 图中同名实体，以便消除冗余，保持数据的移植性。
3. 在综合局部 E-R 图时，还要注意消除那些冗余的联系，冗余信息会影响数据的完整性，使维护工作复杂化。但有时也要折中考虑，有时必要的冗余会提高数据处理效率，综合时也可以在总体 E-R 图中增加新的联系。
---

### 五、E-R图转换为表
1. 将各实体转换为对应的表。
2. 将实体中的各属性转换为各表对应的列。
3. 标识每个表的主键列：需要注意是，没有主键的表添加ID编号列，它并没有实际意思，用于做主键或外键。
4. 在表之间建立朱外键，体现实体之间的映射关系（1:1,1：n,
和 m：n）

----
### 六、练习
```
create table student(
    student_no int not null,
    name varchar(32) not null,
    orign varchar(32),
    primary key(student_no)
);

```

```
create table t_class(
    id int not null,
    class_name varchar(32) not null,
    primary key(id)
);

create table t_student(
    id int auto_increment not null,
    student_no char(4) not null,
    name varchar(32) not null,
    age smallint default 21 not null,
    class_id int not null,
    primary key(id),
    constraint stu_fk foreign key(class_id) references t_class(id)
);
```

```
create table t_class(
    id int not null,
    class_name varchar(32) not null,
    number int not null,
    primary key(id),
);

create table t_teacher(
    teacher_no int not null,
    teacher_name varchar(32) not null,
    sex varchar(10) not null;
    class_id int not null;
    primary key(teacher_no);
    constrain t_c foreign key(class_id) references t_class(id)
);
```

## Connection 接口
* Connection 接口代表与特定的数据库的连接，在连接上下文中执行SQL语句并返回结果


方法                                 |   功能描述
---                                  |   ---
==*== createStatement()              |   创建Statement对象
createStatement(int resultSetType,int resultSetConcurrency)|创建一个Statement对象，该对象将生成具有给定类型、并发性和可保存性的ResultSet对象
==*== preparedStatement()            |   创建预处理对象prepardStatement
isReadOnly()                         |   查看当前Connection对象的读取模式是否为只读模式
setRendOnly()                        |   设置当前对象的读写模式
commit()                             |   使所有上一次提交/回滚后进行的更改成为持久更改，并释放此Connection对象当前持有的所有数据库锁
roolback()                           |   取消在当前事务中进行的所有更改，并释放此Connection对象当前持有的所有数据库锁
==*== close()                        |   立即释放此Connection对象的数据库和JDBC资源，而不是等待它们被自动释放


## Statement接口
* Statement接口用于在已经建立连接的基础上向数据库发送SQL语句
* Statement对象用于执行不带参数的简单SQL语句
* preparedStatement（继承Statement）对象用于执行动态的SQL语句
* callableStatement（继承preparedStatement）用于执行对数据库的存储过程的调用


**Statement接口中常用的方法**

方法                                |功能描述
----------                          |-----------
execute(String sql)                 |执行静态的selcet语句，该语句可能返回多个结果集
==*== executeQuery(String sql)            |执行给定的SQL语句，该语句返回单个ResultSet对象
clearBatch()                        |清空此Statement对象的当前SQL命令列表
executeBatch()                      |将一批命令提交给数据库来执行，如果全部命令执行成功，则返回更新计数组成的数组。数组元素的排序与SQL语句的添加顺序对应
addBatch()                          |将给定的SQL命令添加到此Statement对象的当前命令列表中。如果驱动程序不支持批量处理，将抛出异常
==*== close()                       |释放Statement实例占用的数据库和JDBC资源

**PreparedStatement 接口**
方法                                |功能描述
---                                 |---
==*== setInt(int index,int k)       |将指定位置的参数设置为int值
setFolat(int index,float f)         |将指定位置的参数设置为float值
setLong(int index,long l)           |将指定位置的参数设置为long值
setDouble(int index,double d)       |将指定位置的参数设置为double值
setBoolean(int index,boolean b)     |将指定位置的参数设置为boolean值
setDate(int index,date date)        |将指定位置的参数设置为date值
==*== executeQuery()                      |在此PreparedStatement对象中执行SQL查询，并返回该查询生成的ResultSet对象
==*== setString(int index,String s) |将指定位置的参数设置为String值
setNull(int index,intsqlType)       |将指定位置的参数设置为SQL NULL
==*== executeUpdate()                     |执行前面包含的参数的动态insert、update或delete语句
clearParameters()                   |清除当前所有参数的值

**DriverManager 类**
* DriverManager类用来管理数据库中的所有驱动程序。它是JDBC的管理层，作用于用户和驱动程序之间，跟踪可用的驱动程序，并在数据库的驱动程序之间建立连接。
* DriverManager类的常用方法

方法                                |功能描述
---                                 |---
==*== getConnection(String url,String user,String password)   |指定三个入口参数(url,用户名,密码)来获取与数据库的连接
setLoginTimeout()                   |获取驱动程序试图登录到某一数据库时可以等待的最长时间，以秒为单位
println(String message)             |将一条消息打印到当前JDBC日志流中

**ResultSet 接口**
* ResultSet接口类似于一个临时表，用来暂时存放数据库查询操作所获得的结果集
* ResultSet接口的常用方法  

方法                                |功能描述
---                                 |---
==*== getInt()                            |以int形式获取此ResultSet对象的当前行的指定列值。如果列值是NULL，则返回值是0
getFloat()                            |以Float形式获取此ResultSet对象的当前行的指定列值。如果列值是NULL，则返回值是0
getDate()                            |以Date形式获取此ResultSet对象的当前行的指定列值。如果列值是NULL，则返回值是null
getBoolean()                            |以boolean形式获取此ResultSet对象的当前行的指定列值。如果列值是NULL，则返回值是null
==*== getString()                            |以String形式获取此ResultSet对象的当前行的指定列值。如果列值是NULL，则返回值是null
getObject()                            |以Object形式获取此ResultSet对象的当前行的指定列值。如果列值是NULL，则返回值是null
first()                             |将指针移到当前记录的第一行
last()                              |将指针移到当前记录的最后一行
==*== next()                        |将指针向下移一行
beforeFirst()                       |将指针移到集合的开头(第一行位置)
afterLast()                         |将指针移到集合的尾部(最后一行位置)
absolute()                          |将指针移到ResultSet给定编号的行
isFirst()   |判断指针是否位于当前ResultSet集合的第一行
ifLast()    |判断指针是否位于当前ResultSet集合的最后一行
updateInt()     |用int值更新指定列
updateFloat()   |用Float值更新指定列
updateLong()    |用Long值更新指定列
updateString()  |用String值更新指定列
updateObject()  |用Object值更新指定列
updateNull()    |将指定的列值修改为null
updateDate()    |用指定的date值更新指定列
updateDouble()  |用指定的Double值更新指定列
getrow()        |查看当前行的索引号
insertRow()     |将插入行的内容插入到数据库中
updateRow()     |将当前行的内容同步到数据表中
deleteRow()     |删除当前行，但并不同不到数据库中，而是在执行close()方法后同步到数据中
### 1. JavaBean的概念

* JavaBean是一种可重复使用、且跨平台的软件组件。JavaBean可分为两种：

  一种是有用户界面(UI,User Interface)的JavaBean；

  还有一种是没有用户界面，主要负责处理事务(如数据运算，操纵数据库)的JavaBean。JSP通常访问的是后一种JavaBean

### 2. JSP与JavaBean搭配使用的优点

1. 使得HTML与Java程序分离，这样便于维护代码。如果把所有的程序代码都写到JSP网页中，会使得代码繁杂，难以维护

2. 可以降低开发JSP网页人员对Java编程能力的要求

3. JSP侧重于生成动态网页，事务处理由JavaBean来完成，这样可以充分利用JavaBean组件的可重用性特点，提高开发网站的效率

### 3. JavaBean的特征
* 一个标准的JavaBean有以下几个特性：  
>JavaBean是一个公共的（public）类  
>JavaBean有一个不带参数的构造方法  
>JavaBean通过setXXX方法设置属性，通过getXXX方法获取属性

### 4. JavaBean类
```java
public class CounterBean{

    private int count=0;
    
    public CounterBean(){}
    
    public int getCount(){
        return count;
    }
    
    public void setCount(int count){
        this.count=count;
    }
}
```

### 5. JSP访问JavaBean的语法
1. 导入JavaBean类 
```jsp
<%@ page import="com.pzh.www.javaBean.Person" %>
```
2. 声明JavaBean对象
```jsp
<jsp:useBean id="person" class="com.pzh.www.javaBean.Person">
```
3. 访问JavaBean属性
```jsp
<jsp:getProperty property="age" name="person"/>
<jsp:setProperty property="address" name="person" value="广东工业大学"/>
<jsp:setProperty property="age" name="person" param="helloworld">
```

### 6. javabean的存活范围
* scope属性决定了JavaBean对象的存在的范围。scope的可选值包括
1. page（默认值）
> ​	客户每次请求访问JSP页面时，都会创建一个JavaBean对象。JavaBean对象的有效范围是客户请求访问的当前JSP网页。JavaBean对象在以下两种情况下都会结束生命期：  
>
> &nbsp;&nbsp; - 客户请求访问的当前JSP网页通过<forward>标记将请求转发到另一个文件  
> &nbsp;&nbsp; - 客户请求访问的当前JSP页面执行完毕并向客户端发回响应。

2. request
> 客户每次请求访问JSP页面时，都会创建新的JavaBean对象。JavaBean对象的有效范围为：   
&nbsp;&nbsp; - 客户请求访问的当前JSP网页      
&nbsp;&nbsp; - 和当前JSP网页共享同一个客户请求的网页，即当前JSP网页中<%@ include>指令以及<forward>标记包含的其他JSP文件   
&nbsp;&nbsp; - 当所有共享同一个客户请求的JSP页面执行完毕并向客户端发回响应时，JavaBean对象结束生命周期。   
&nbsp;&nbsp; - JavaBean对象作为属性保存在HttpRequest对象中，属性名为JavaBean的id，属性值为JavaBean对象，因此也可以通过HttpRequest.getAttribute()方法取得JavaBean对象，例如：

```java
CountBean countBean = (CountBean)request.getAttribute("countBean");
```

3. session
> ​	JavaBean对象被创建后，它存在于整个Session的生存周期内，同一个Session中的JSP文件共享这个JavaBean对象   
> 	JavaBean对象作为属性保存在HttpSession对象中，属性名为JavaBean的id，属性值为JavaBean对象。除了可以通过JavaBean的id直接引用 JavaBean 对象外，也可以通过HttpSession.getAttribute() 方法取JavaBean对象，例如：

```java
CounterBean obj = (CounterBean)session.getAttribute("myBean");
```

4. application
> ​	JavaBean对象被创建后，它存在于整个Web应用的生命周期内，Web应用中的所有JSP文件都能共享同一个JavaBean对象   
> 	JavaBean对象作为属性保存在application对象中，属性名为JavaBean的 id，属性值为JavaBean对象，除了可以通过JavaBean的id直接引用 JavaBean对象外，也可以通过application.getAttribute() 方 法 取 得JavaBean对象，例如：

```java
CounterBean obj = (CounterBean)application.getAttribute("myBean");
```

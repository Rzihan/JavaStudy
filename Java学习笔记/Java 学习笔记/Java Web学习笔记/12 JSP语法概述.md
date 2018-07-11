### 1. JSP语法概述

1. JSP原始代码中包含了JSP元素和Template(模板)data两类
2. Templatedata指的是JSP引擎不处理的部分，即标记<%……%>以外的部分，例如代码中的
  HTML的内容等，这些数据会直接传送到客户端的浏览器
3. JSP元素则是指将由JSP引擎直接处理的部分，这一部分必须符合JAVA语法，否则会导致编译错误。

### 2. JSP例子
```html
<html>
    <head>
        <title>Hi-JSP实验</title>
    </head>
    <body>
        <%
            String msg = "This is JSP test.";
            out.print("Hello World!");
        %>
        <h2><%=msg%></h2>
    </body>
</html> 
```

1. JSP语法分为三种不同的类型
    * 编译器指令（DIRECTIVE）

    > <%@ page import=“java.io.*” %>

    * 脚本语法(SCRIPTING)

    * 动作语法(ACTION)

    > <jsp:forward>，<jsp:getProperty>，<jsp:include>

#### 2.1 脚本语法
1. “HTML注释”:<!— comments -->
2. “隐藏注释”:<%-- comments --%>
3. “声明”
4. “表达式”
5. “脚本段”

##### 2.1.1 HTML注释
* JSP 语法格式如下：
> <!-- comment [ <%= expression%> ] --> 或<!-- 注释 [<%= 表达式 %> ] -->
* 这种注释发送到客户端，但不直接显示，在源代码中可以查看到。

```html
<html>
    <head>
        <title> HTML注释 </title>
    </head>
    <body>
    <!-- This file displays the user login screen -->
        未显示上一行的注释。
    <!--This page was loaded on <%= (new java.util.Date()).toLocaleString() %> -->
    	在源文件中包括当前时间。
    </body>
</html>
```

##### 2.1.2 隐藏注释
* JSP语法格式如下：
> <%-- 注释 --%>
* 不发送到客户端

```html
<html>
    <head>
        <title>A Comment Test</title>
    </head>
    <body>
        <h2>A Test of Comments</h2>
        <%-- This comment will not be visible in the page source --%>
    </body>
</html>
```

##### 2.1.3 声明
* JSP 语法格式如下：
> <%! declaration; [ declaration; ] ...%>

##### 2.1.4 表示式
* JSP 语法格式如下：
> <%= 表达式 %>

##### 2.1.5 脚本段
* JSP 语法格式如下：
> <% 代码 %>



#### 2.2 编译器指令

1. 编译器指令包括“包含指令”，“页指令”
   和“taglib指令”

2. 它们包含在“<%@ %>”卷标里。

3. 两个主要的指令是page与include。

##### 2.2.1 包含指令

   - include指令：向当前页中插入一个静态文件的内容。
   - JSP 语法格式如下：

   > <%@ include file="relativeURL" %> 或<%@ include file="相对位置" %>

#### 2.3 动作语法

​	动作语法包括<jsp:forward>，<jsp:include>，<jsp:getProperty>，<jsp:setProperty>和<jsp:useBean>。

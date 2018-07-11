#### 1.Page指令

* "Page"指令用于定义JSP文件中的全局属性
```html
    <%@ page
    language="java"
    extends="package.class"
    import="package.class | package.*"
    session="true|false"
    isThreadSafe="true|false"
    errorPage="relativeURL"
    contentType="mimeType
    [;charset=characterSet]"|"text/html;charset=ISO-8859-1"]
    isErrorPage="true|false"
    %>
```

* 属性：
* 1．language="java"
声明脚本语言的种类，目前只能用"java" 。

* 2.import="{package.class | package.* },..."需要导入的Java包的列表，这些包作用于程序段，表达式，以及声明。下面的包在JSP编译时已经导入了，所以就不需要再指明了：

> java.lang.* 	javax.servlet.* 	 javax.servlet.jsp.* 	 javax.servlet.http.*   

* 3．errorPage="relativeURL"
设置处理异常事件的JSP文件。

* 4．isErrorPage="true | false"
设置此页是否为出错页，如果被设置为true,你就能使用exception对象

#### 2.Page指令详说

* “<%@ page%>”指令作用于整个JSP页面，同样包括静态的包含文件。但是“<%@ page %>”指令不能作用于动态的包含文件，比如 “<jsp:include>”。

* 可以在一个页面中用上多个“<%@ page%>”指令，但是其中的属性只能用一次，不过也有例外，那就是import属性。因为import属性和Java中的import语句类似(参照JavaLanguage，import语句引入是Java语言中的类)，所以此属性就能用多次。 

* 无论把“<%@ page%>”指令放在JSP的文件的哪个地方，它的作用范围都是整个JSP页面。不过，为了JSP程序
的可读性，以及好的编程习惯，最好还是把它放在JSP
文件的顶部。

#### 3.<jsp:forword>
* JSP语法格式如下：
>1．<jsp:forward page={"relativeURL" | "<%=expression %>"} />  
><jsp:param name="parameterName"
>value="{parameterValue | <%= expression %>}" />  

* 属性
* 1、page="{relativeURL | <%= expression %>}"

* 这里是一个表达式或是一个字符串用于说明你将要定向的文件或URL。这个文件可以是JSP,或程序段

* 2 、<jsp:param name="parameterName" value="{parameterValue | <%=expression %>}" />

* 向一个动态文件发送一个或多个参数，这个文件必须是动态文件。如果想传递多个参数，可以在一个JSP文件中使用多个“<jsp:param>”；“name”指定参数名，“value”指定参数值。

* “<jsp:forward>”标签从一个JSP文件向另一个文件传递一个包含用户请求的request对象。“<jsp:forward>”标签以后的代码，将不能执行。 

* forword.jsp
```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
	<jsp:forward page="forwordTo.jsp">
		<jsp:param value="R,gdut" name="userName"/>
	</jsp:forward>
</body>
</html>
```
* forwordTo.jsp
```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%
		String userName = request.getParameter("userName");
		String outStr = "谢谢光临！" + userName;
		out.println(outStr);
	%>
</body>
</html>
```

#### 四、<jsp:include>
* 包含一个静态或动态文件
* JSP 语法格式如下：
> 1．<jsp:include page="{relativeURL |<%=expression%>}" flush="true" />   
>
> 2. <jsp:param name="parameterName" value="{parameterValue |<%= expression %>}" />   

* <jsp:include>的属性
> 1．page="{relativeURL | <%=expression %>}"参数为一相对路径，或者是代表相对路径的表达式。   
> 2.<jsp:param name="parameterName" value="{parameterValue | <%=expression %> }" />   
> “<jsp:param>”用来传递一个或多个参数到指定的动态文件，能在一个页面中使用多个“<jsp:param>”来传递多个参数

* include.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%
		out.println("我爱学习!<br>");
	%>
	<jsp:include page="included.jsp">
		<jsp:param value="R,gdut" name="userName"/>
	</jsp:include>
</body>
</html>
```
* included.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	String userName = request.getParameter("userName");
	out.println("欢迎用户：  <h2>" + userName + "</h2><br>");
%>
```

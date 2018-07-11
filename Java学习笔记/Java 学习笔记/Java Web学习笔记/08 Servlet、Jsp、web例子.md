## 1. 知识点介绍

* 表单的action属性,表示表单提交到什么地方
> /WebDemo/LoginServlet
* 先到/WebDemo 的目录找到 web.xml 文件
> <servlet-mapping> --> <url-pattern> --> <servlet-name> --> <servlet-class>
> 创建相应的Servlet类
> getParameter(String args0) 可以获取对应表单的数据


## 2.login.jsp

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
        <!--action 表单提交到什么地方 -->
	<form action="/WebDemo/LoginServlet">
	
		username:<input type="text" name="username"><br>
		password:<input type="password" name="password"><br>
		<input type="submit" value="submit">&nbsp;&nbsp;&nbsp;
		<input type="reset" value="reset">	
	</form>
</body>
</html>
```

## 3. web.xml 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1">
  <display-name>WebDemo</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>
  
  <servlet>
  	<servlet-name>HelloWorld</servlet-name>
  	<servlet-class>com.pzh.servlet.HelloWorldServlet</servlet-class>
  </servlet>
  
  <servlet>
  	<servlet-name>LoginServlet</servlet-name>
  	<servlet-class>com.pzh.servlet.LoginServlet</servlet-class>
  </servlet>
  
  <servlet-mapping>
  	<servlet-name>HelloWorld</servlet-name>
  	<url-pattern>/HelloWorld</url-pattern>
  </servlet-mapping>
  
  <servlet-mapping>
  	<servlet-name>LoginServlet</servlet-name>
  	<url-pattern>/LoginServlet</url-pattern>
  </servlet-mapping>
</web-app>
```

## 4.Servlet类

```java
package com.pzh.servlet;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class LoginServlet extends HttpServlet {
	
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		resp.setContentType("text/html");
		
		String username = req.getParameter("username");
		String password = req.getParameter("password");
		
		PrintWriter out = resp.getWriter();
		
		out.println("<html><head><title>LoginRulset</title></head>");
		out.println("<body>username:" + username + "<br>");
		out.println("password:" + password + "</body></html>");
	}
}
```

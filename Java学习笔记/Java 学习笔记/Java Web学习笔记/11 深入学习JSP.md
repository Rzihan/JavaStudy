
### 1. JSP简介

1. 在传统的网页HTML文件（*.htm，*.html）中加入Java程序片段（Scriptlet）和JSP标签，就构成了JSP网页

2. Java程序片段可以操纵数据库、重新定向网页以及发送E-mail等，实现建立动态网站所需要的功能。

3. 所有程序操作都在服务器端执行，网络上传送给客户端的仅是得到的结果，这样大大降低了对客户浏览器的要求，即使客户浏览器端不支持Java，也可以访问JSP网页。

### 2. 复习JSP的概念

1. Java Server Pages
2. Servlet 简化设计，逻辑与界面设计分开，开发更方便；
3. HTML语法的Java扩张，加入新的标签（<%,%>）;
4. 强大的组件（Java Bean）支持功能；

### 3. JSP文件结构及主要标签

```jsp
<%@ page contentType="text/html;charset=gb2312" %>
<%@ page import="java.util.*“ %>
...
<HTML>
 <BODY>
    其他 HTML 语言
    <%
     符合JAVA 语法的 JAVA 语句
    %>
    其他 HTML 语言
 </BODY>
</HTML>
```

### 4. JSP执行过程


```
graph TD
A[..]-->|request|B[*.jsp]
B --> |jsp parser| C[*.java]
D[servlet] --> C
C-->|JSDK|E[*.class]
E-->|执行|F[response]
```

```
graph TD
A[客户端]-->|request|B[服务器]
B-->|response|A
B-->C[查找对应的JSP文件]
C-->D{是否存在}
D-->|N|H
D-->|Y|E{是否是修改或创建后第一次调用}
E-->|N|H
E-->F[调用Jsp Parser将其编译成Servlet程序]
F-->G[调用JSDK将对应的Servlet程序编译成Servlet字节码]
G-->H[执行已有的对应的Java字节码]
```


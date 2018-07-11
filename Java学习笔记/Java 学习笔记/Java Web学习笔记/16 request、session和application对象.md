### 1. request、session和application
1. request的setAttribute与getAttribute方法一般都是成对出现的，首先通过setAttribute方法设置属性与属性值，然后通过getAttribute方法根据属性获取到与该属性对应的对象值（获取到之后一般都需要进行向下类型转换，将属性值转换成为真正的对象），setAttribute与getAttribute方法都是在服务器端内部执行的，客户端不知道服务器端是否执行过这两个方法

2. request的getParameter方法的作用法是获取到客户端通过表单或url请求参数所发送过来的参数值，是客户端与服务器端端之间的交互，服务器端要想获取到客户端发送过来的数据，就需要使用getParameter方法来获取。没有与getParameter方法对应的setParameter方法

3. request对象内数据存活范围就是在request对象存活范围内，当客户端想服务器端发送一个请求，服务器想客户端返回一个响应后，该请求对象就被销毁了；之后再向服务器端发送新的请求时，服务器会创建新的request对象，该request对象与之前的request对象没有任何关系，因此也无法获得在之前的request对象中所存放的任何数据

4. session对象内数据的存活范围也就是session对象的存活范围（？只要浏览器不关闭，session对象就会一直存在？），因此在同一个浏览器窗口的，无论向服务器端发送多少个请求，session对象只有一个

5. application（应用对象）:存活范围最大的对象，只要服务器没有关闭，application对象中的数据就会一直存在。在整个服务器运行过程当中，application对象只有一个。

6. request、session以及application这3个对象的范围是逐个增加的：

   > request只在一个请求的范围内;
   >
   > ？ session 是在浏览器窗口的范围内？;
   >
   > application则是在整个服务器的运行过程中。 


#### 1.1 请求重定向和请求转发

1. HttpServletResponse对象的sendRedirect(String location)方法称作 重定向。如果 location 地址前面加上“/”，则表示相对于与Servlet容器的根来请求，即http://localhost:8080,如果location地址没加上“/”，则表示相对于当前请求的URL来寻找地址。

2. RequestDispatcher 的 forward(request,response)方法称作请求转发

```java
//请求重定向
response.sendRedirect("result.jsp");
//请求转发
RequestDispatcher rd = request.getRequestDispatcher("myResult.jsp");
rd.forward(request, response);
```

#### 1.2 Application 的 getRealPath()方法

```java
//getRealPath()方法会返回资源在服务器上的绝对路径
out.println(application.getRealPath("/application2.jsp"));
```

#### 1.3表单隐藏信息
```
<input type="hidden" name="username" value="<%=name %>">
```
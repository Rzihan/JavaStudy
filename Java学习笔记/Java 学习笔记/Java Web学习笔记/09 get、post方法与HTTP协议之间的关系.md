### 1. get与post方法之间的差别：

1. 浏览器地址栏呈现的结果不同(表象)
2. 真正的原因在于向服务器端发送请求时的形式是不同
3. get的请求格式：
> GET /test/LoginServlet?username=hello&password=world HTTP/1.1
4. post的请求格式：

> POST /test/LoginServlet HTTP/1.1  
> ......   
> Connection:Keep-Alive  
> 
> username=hello&password=world

5. 通过浏览器进行文件上传时，一定要使用post方式而绝不能使用get方式
6. 通过浏览器地址栏输入网址的方式来访问服务器端资源，全部使用的是get方法请求的

> post方式一般是通过表单(form)指定，在服务器端get和post没区别，只是方法名不一样
### 2.客户端、服务器与Servlet/jsp之间的关系



```markdown
graph LR
客户端-->服务器
服务器-->客户端
服务器-->Servlet
```



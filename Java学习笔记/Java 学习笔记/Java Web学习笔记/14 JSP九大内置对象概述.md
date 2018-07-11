### 1.JSP九大内置对象
1. request，请求对象
2. response，响应对象
3. pageContext，页面上下文对象
4. session，会话对象
5. application，应用程序对象
6. out，输出对象
7. config，配置对象
8. page，页面对象
9. exception，异常对象

### 2. 综述
* 有几种对象看起来和ASP的内置对象差不多，功能也类似，这是因为这些内置对象的构建基础是标准化的HTTP协议，如果使用过ASP，又对Java有一定了解的话，那么对这个几种JSP内置对象的使用应该能迅速掌握。需要注意的问题是对象名的写法，包括这些对象方法的调用时也要书写正确，因为Java语言本身对大小写敏感的

* 从本质上，jsp的这些内置对象其实都是由特定的Java类所产生的，在服务器运行时根据情况自动生成，所以如果你有较好的Java基础，可以参考相应的类说明，表给出了他们的对应关系。


### 3. JSP内置对象映射表
对象名| 类型 | 作用域
---|---|---
request | javax.servlet.ServletRequest 的子类 | Request
response | javax.servlet.ServletResponse 的子类 | Page
pageContext | javax.servlet.jsp.PageContext | Page
session | javax.servlet.http.HttpSession | Session
application | javax.servlet.ServletContext | Applicaton
Out |javax.servlet.jsp.JspWriter | Page
config | javax.servlet.ServletConfig | Page
Page | java.lang.Object | Page
exception | java.lang.Throwable | Page


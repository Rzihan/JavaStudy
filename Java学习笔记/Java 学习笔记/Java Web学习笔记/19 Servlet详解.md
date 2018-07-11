### 1. Servlet API
1. Servlet的框架的核心是javax.servlet.Servlet接口，所有的Servlet都必须实现这一接口。在Servlet接口中定义了五个放法，其中有三个方法代表了Servlet的生命周期:

>init方法：负责初始化Servlet对象；   
>service方法：负责响应客户的请求；   
>destroy方法：当Servlet对象退出生命周期时，负责释放占用的资源。   

2. 每一个Servlet都必须要实现Servlet接口，GenericServlet是个通用的、不特定于任何协议的Servlet，它实现了Servlet接口，而HttpServlet继承与GenericServlet，因此HttpServlet也实现了Servlet接口，所以我们定义的Servlet只需要继承HttpServlet父类即可。
3. Servelt接口中定义了一个service方法，HttpServlet对改方法进行了实现，实现方式就是将ServletRequest与ServletResponse转换为HttpServletRequest与HttpServletResponse

```java
public void service(ServletRequest req,ServletResponse res)
    throws ServletException,IOException{
        HttpServletRequest request;
        HttpServletResponse response;
        
        try{
            request = (HttpServletRequest)req;
            response = (HttpServletResponse)res;
        }catch(ClassCastException e){
            throw new ServletException("non-HTTP request or response");
        }
        service(request,response);
    }
```

4. 转换完毕后，会调用HttpServlet类中自己定义的service方法，如下所示
5. 在该 service 方法中，首先获得到请求的方法名，然后根据方法名调用对应的 doXXX 方法，比如说请求方法为GET，那么就去调用 doGet方法；请求方法为POST，那么就去调用 doPost 方法。

```java
protected void service(HttpServletRequest req,HttpServletResponse resp)
    throw ServletException,IOExpetion{
        String method = req.getMethod();
        if(method.equals(METHOD_GET)){
            long lastModified = getLastModified(req);
            if(lastModified == -1){
                doGet(req,resp);
            }else{
                long ifModifiedSince = req.getDateHeader(HEADER_IFMODSINCE);
                IF(ifModifiedSince < (lastModified / 1000 * 1000)){
                    maybeSetLastModified(resq,lastModified);
                    doGet(req,resp);
                }else{
                    resp.setStatus(HttpServletResponse.SC_NOT_MODIFIED);
                }
            }
        }
    }
```

6. 在 HttpServlet 类中所提供的 doGet、doPost 等方法都是直接返回错误信息，所以我们需要在自己定义的 Servlet 类中 override 这些方法

### 2. ServletRequest接口
​	ServletRequest接口中封装了客户请求信息，如客户请求方式、参数名和参数值、客户端正在使用的协议,以及发出客户请求的远程主机信息等 。ServletRequest接口还为Servlet提供了直接以二进制方式读取客户请求数据流的ServletInputStream。

​	ServletRequest的子类可以为Servlet提供更多的和特定协议相关的数据. 例如: HttpServletRequest 提供了读取HTTP Head信息的方法。

>getAttribute 根据参数给定的属性名返回属性值   
>getContentType 返回客户请求数据MIME类型    
>getInputStream 返回以二进制方式直接读取客户请求数据的输入流   
>getParameter 根据给定的参数名返回参数值  
>getRemoteAddr 返回远程客户主机的IP地址  
>getRemoteHost 返回远程客户主机名  
>getRemotePort 返回远程客户主机的端口   

### 3. ServletResponse接口
​	ServletResponse 接口为Servlet提供了返回响应结果的方法。它允许Servlet设返回数据的长度和MIME类型,并且提供输出流ServletOutputStream。

​	ServletResponse子类可以提供更多和特定协议相关的方法。例如: HttpServletResponse 提供设HTTPHEAD信息的方法。

>getOutputStream 返回可以向客户端发送二进制数据的输出流对象ServletOutputStream   
>getWriter 返回可以向客户端发送字符数据的PrintWriter对象
>getCharacterEncoding 返回Servlet发送的响应数据的字符编码   
>getContentType 返回Servlet发送的响应数据的MIME类型   
>setContentType 设置Servlet发送的响应数据的MIME类型   

### 4. Servlet 的启动
1. 在下列时刻Servlet容器装载Servlet：

>Servlet容器启动时自动装载某些Servlet    
>在Servlet容器启动后，客户首次向 Servlet 发出请求   
>Servlet的类文件被更新后，重新装载Servlet   

2. Servlet被装载后，Servlet容器创建一个Servlet实例并且调用Servlet的 init()方法进行初始化。在Servlet的整个生命周期中，init方法只会被调用一次

### 5. Servlet的响应客户端请求阶段
* 对于到达Servlet容器的客户请求，Servlet容器创建特定于这个请求的ServletRequest对象和ServletResponse对象，然后调用 Servlet 的service方法。service方法从ServletRequest对象获得客户请求信息、处理该请求，并通过ServletResponse对象向客户返回响应结果。

### 6. Servlet的终止阶段
* 当Web应用被终止，或Servlet容器终止运行，或Servlet容器重新装载Servlet的新实例时，Servlet容器会先调用 Servlet的destroy方法。在destroy方法中，可以释放Servlet所占用的资源。

### 7. Servlet对象何时被创建 
* 默认情况下，当Web客户第一次请求访问某个Servlet时，Web容器创建这个Servlet的实例
* 如果设置了<servlet>元素的<load-on-startup>子元素，Servlet容器在启动Web应用时，将按照指定的顺序创建并初始化这个Servlet。

### 8. web应用何时被加载
* 当Servlet容器启动时，会启动所有的Web应用
* 通过控制台启动Web应用

---
* 注意：某 些 Servlet 在 web.xml 文 件 中 只 有 <servlet> 元 素 而 没 有<servlet-mapping>元素，这样我们就无法通过 url 地址的方式访问这个 Servlet 了，这种 Servlet 通常会在<servlet>元素中配置一个<load-on-startup>子元素，让容器在启动的时候自动加载该 Servlet，并且调用其 init 方法完成一些全局性的初始化工作。
---

### 9. ServletContext和Web应用关系
​	当Servlet容器启动Web应用时，并为每个Web应用创建惟一的ServletContext对象。你可以ServletContext看成是一个Web应用的服务器端组件的共享内存。在ServletContext中可以存放共享数据，它提供了读取或设置共享数据的方法:   

– setAttribute（String name,Object object）把一个对象和一个属性名绑定，将这个对象存储在ServletContext中。

– getAttribute（String name）根据给定的属性名返回所绑定的对象


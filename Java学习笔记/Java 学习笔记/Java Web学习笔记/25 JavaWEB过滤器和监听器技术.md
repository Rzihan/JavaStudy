# JavaWEB过滤器和监听器技术

## 1、过滤器介绍

### 1.1、什么是过滤器

对请求和响应进行拦截或者增强的对象，就是过滤器。

Filter接口：功能——对请求和响应进行增强或者进行拦截。

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213521088-2113534094.png)

### 1.2、JavaWEB中的过滤器运行图解

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213521400-1362402675.png)

## 2、Filter的快速入门（重点：必须掌握）

### 2.1、FIlter定义以及创建步骤介绍

```java
package cn.itcast.filter;

import java.io.IOException;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;

/**
* @author panzihan
* 总结：过滤器书写步骤
* 第一：创建类实现接口——DemoFilter implements Filter
* 第二：过滤任务写在doFilter方法中
* 第三：web.xml中配置
*/

public class DemoFilter implements Filter{

    @Override
    //销毁的方法
    public void destroy() {}

    @Override
    //执行过滤的方法
    public void doFilter(ServletRequest arg0, ServletResponse arg1,
            FilterChain arg2) throws IOException, ServletException {
        System.out.println("DemoFilter.....doFilter....");
    }

    @Override
    //初始化的方法
    public void init(FilterConfig arg0) throws ServletException {}
}
```

Filter 是在 Web 应用程序的部署描述符中配置的——过滤器创建好之后，需要在web.xml中做配置 

### 2.2、在web.xml文件中配置过滤器

```xml
<filter>
    <filter-name>DemoFilter</filter-name>
    <filter-class>cn.itcast.filter.DemoFilter</filter-class>
</filter> 

<filter-mapping>
    <filter-name>DemoFilter</filter-name>
    <url-pattern>/1.txt</url-pattern>
</filter-mapping>
```

Filter拦截操作效果:

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213521650-685075054.png)

### 2.3、过滤器放行的对象：FilterChain功能介绍

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213521994-110364420.png)

### 2.4、**FilterChain的doFilter方法**： 

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213522353-1067652072.png)

代码实现：

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213522681-293248812.png)

过滤器放行执行过程：

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213523010-1482319124.png)

## 3、Filter的生命周期

回顾servlet的生命周期：

创建： 第一次被访问的时候

销毁： 服务器关闭的时候，或者当前项目从服务器中移除

 

回顾session的生命周期：

创建： 第一次调用getsession方法

销毁： 服务器非正常关闭，超过生存时间，调用销毁（自杀）的方法



Filter：

创建：在服务器启动的时候

服务器启动截图：

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213523369-1815783433.png)



销毁： 在服务器关闭的时候，过滤器销毁。

服务器关闭截图：

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213523650-332890033.png)

3.1、FilterConfig介绍

servletConfig对象：获取servlet相关的配置信息。

FilterConfig定义：获取filter相关的配置信息。

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213523869-1379418573.png)

API介绍： 

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213524353-2078246720.png)

API代码演示：

1）设置过滤器初始化参数

2）通过filterconfig对象来获取参数

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213524681-16135041.png)

参数配置：

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213525041-960753660.png)

效果演示：

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213525385-1889973980.png)

##  4、Filter配置详解（web.xml中的配置）

### 4.1、关于url-pattern配置

**过滤器如何匹配请求的路径?** 

回顾servlet的url-pattern：

全路径匹配——

​    地址栏：localhost:8080/项目根路径/资源路径 localhost:8080/itcast-filter2/1.txt

通配符的匹配——

​    地址栏：localhost:8080/项目根路径/abc/*



以上两种匹配方式，配置路径的时候必须以"/"开头

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213525728-333515520.png)

后缀名匹配——/路径/*.do: *.do *.txt *.action

​    地址栏：localhost:8080/项目根路径/*.txt

后缀名匹配方式，配置路径的时候不能以"/"开头

Filter的url-pattern配置与servlet一致

* 过滤器执行的顺序是按照，web.xml中filter-mapping标签的书写顺序执行（从上往下执行） 

---

## 5、监听器介绍

### 5.1、什么是监听器

监听事件员，根据事件员上发生事情，做成相应的处理。

### 5.2、监听机制相关概念

* 事件源：发生时间的源头，监听器需要监听的对象。
* 事件：事件员上发生的动作，监听器监听的内容。
* 监听器：负责监听事件源的对象。

### 5.3、JavaWeb监听器介绍

JavaWeb中监听器主要监听JavaWEB中的request、session、ServletContext对象的各种变化。

主要监听的任务：

 	1. 监听request，ServletContext，session对象的创建和销毁。
 	2. 监听request、session、servletContext对象存放数据变化情况。
 	3. 监听session中保存的JavaBean的状态。

## 6、JavaWeb监听器创建步骤

1. 需要定义一个类实现对应的监听器接口

   ServletRequestListener定义(API截图)：

   ![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213529713-1699000804.png)

   ![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213530041-1647297173.png)

   代码演示

   ```java
   package cn.itcast.listener;
   
   import javax.servlet.ServletRequestEvent;
   import javax.servlet.ServletRequestListener;
   
   public class MyServletRequestListener implements ServletRequestListener{
      @Override
      //监听request对象销毁的方法
      public void requestDestroyed(ServletRequestEvent sre) {        		 					System.out.println("MyServletRequestListener.....requestDestroyed....");		
      }
       
      @Override
      //监听request对象初始化的方法
      public void requestInitialized(ServletRequestEvent sre) {
           System.out.println("MyServletRequestListener.....requestInitialized....");
      }
   }
   ```

   

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213530463-1777375022.png)

### 6.1、配置监听器对象

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213530728-8641817.png)

* 注意：当服务器加载项目的时候，会读取web.xml文件中listener标签，那么服务器会自动创建监听器对象，并且自动调用其方法

### 6.2、监听器小结

1. 创建一个类，实现监听器接口
2. 在监听器对象的方法中，书写相关的代码。
3. 在web.xml配置当前监听器。

## 7、ServletContext创建销毁监听（ServletContextListener）

### 7.1、ServletContextListener定义（API截图）：

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213531025-109459812.png)

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213531338-12574087.png)

* 代码演示

```java
package cn.itcast.listener;

import javax.servlet.ServletContextEvent;
import javax.servlet.ServletContextListener;

public class MyServletContextListener implements ServletContextListener{
    @Override
    public void contextInitialized(ServletContextEvent sce) {
        System.out.println("MyServletContextListener.....contextInitialized....");
    }

    @Override
    public void contextDestroyed(ServletContextEvent sce) {
        System.out.println("MyServletContextListener.....contextDestroyed....");
    }
}
```

* 监听器配置

```xml
<listener>
    <listener-class>cn.itcast.listener.MyServletContextListener</listener-class>
</listener>
```

* 监听servletcontext对象初始化截图： 

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213531619-1597478352.png)

* 监听servletcontext对象销毁截图： 

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213531869-1527701864.png)

## 案例：定时任务演示

需求：项目启动时，获取服务器时间（new Date()），每一秒钟更新一次，打印在控制台

思路：

1）监控项目的启动（使用ServletContextListener来监听ServletContext对象的初始化）

1. 获取服务器时间：new Date（）；
2. 每一秒更新一次：定时器Timer

4）给定时器设置定时任务

Timer：定时器

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213532135-2138826952.png)

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213532478-1037155275.png)

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213532791-368821638.png) 

timeTask：定时器的任务（类）

firstTime：从什么时候开始执行，立即执行设置为：0

period ：间隔多少时间重复执行，毫秒值，1秒=1000毫秒

 

TimerTask：定时器的任务（类） 

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213533088-97766983.png)

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213533431-1362934229.png)

Run方法中应该写我们的定时任务：每一秒钟更新一次时间，打印在控制台上

 

代码实现：

```java
package cn.itcast.listener;

import java.util.Date;
import java.util.Timer;
import java.util.TimerTask;
import javax.servlet.ServletContextEvent;
import javax.servlet.ServletContextListener;

/**
* @author wjn
* 	1）创建一个类，实现监听器接口
    2）在监听器对象的方法中，书写相关的代码
    3）在web.xml中配置当前监听器。
*/

public class MyServletContextListener implements ServletContextListener{

    @Override
    public void contextInitialized(ServletContextEvent sce) {
        System.out.println("MyServletContextListener....contextInitialized...");
        //监控项目的启动（使用ServletContextListener来监听ServletContext对象的初始化）
        //2)获取服务器时间：new Date（）；
        //3)每一秒更新一次：定时器Timer
        //4)给定时器设置定时任务
        //获取定时器
        Timer timer = new Timer();
        //调用定时器的设置定时任务的方法
        //firstTime 0:立即执行
        //period：间隔多长时间执行一次，1000
        timer.schedule(new TimerTask() {
            @Override
            public void run() {
                //在run方法中，书写，要执行的任务
                //过时的方法一般不推荐使用，但是，过时的方法，jdk不会删除它的效果。
                //当前显示时间，可以使用服务器中的时间——java代码，new Date();
                //当前显示时间——javascript代码，new Date();
                //javascript代码，是在浏览器运行，客户端的时间，一般是不使用客户端的时间
                //业务：整点秒杀
                //获取的是服务器时间，用户，是没有办法控制
                //获取客户端时间，时间有客户控制，时间是不对的
                //一般尊循的原则，只要可以控制在服务器的，绝对不给客户端
                System.out.println(new Date().toLocaleString());
            }
        }, 0, 1000);
    }
    
    @Override
    public void contextDestroyed(ServletContextEvent sce) {
        System.out.println("MyServletContextListener....contextDestroyed...");
    }
}
```

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213534385-652562468.png) 

## 8、HttpSessionListener对象监听session的创建与销毁监听

HttpSessionListener定义（API截图）：

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213534728-1630722277.png)

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213535056-675190479.png)

代码演示：

```java
package cn.itcast.listener;

import javax.servlet.http.HttpSessionEvent;
import javax.servlet.http.HttpSessionListener;

public class MyHttpSessionListener implements HttpSessionListener{

    @Override
    public void sessionCreated(HttpSessionEvent se) {
        System.out.println("MyHttpSessionListener....sessionCreated....");
    }

    @Override
    public void sessionDestroyed(HttpSessionEvent se) {
        System.out.println("MyHttpSessionListener....sessionDestroyed....");
    }

}
```

* 配置文件：

```xml
<listener>
        <listener-class>cn.itcast.listener.MyHttpSessionListener</listener-class>
 </listener>
```

### 8.1、统计在线人数

用户积累：优惠，折扣，广告，扫码关注，想所有QQ用推送一条消息，给所有支付宝用户发送消息。

第三方登录，QQ账号，微博账号，微信账号，优酷账号，支付宝账号，银行账户，百度账号

1. 用户体验非常好

2. 创业公司，除了积累用户以外，还获取了用户的QQ或者支付宝，或者微信，可以使用现成推广渠道，再次推广自己应用

    

需求：统计当前访问网站的人数有多少人？

 什么时候我们可以知道用户访问了网站？

只要用户访问了我们的网站，session一定会创建。只要用户离开，点退出，session就销毁。

  

思路：

只要判断session创建，在线人数就加一

只要判断session销毁，在线人数就减一

 

在线人数的数据，要存在哪里？ 

ServletContext对象中，所有应用程序范围都可以获取，所有访问当前网站的用户，都应该可以看到在线人数



总思路：

1）先在servletContext中初始化在线人数参数；当前项目初始化的时候，将在线人数初始化：0人。

2）在监听器中只要判断session创建，在线人数就加一

3）在监听器中只要判断session销毁，在线人数就减一

 

代码实现：

![img](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213535853-912974342.png)

监听器代码：

```java
package cn.itcast.listener;

import javax.servlet.ServletContext;
import javax.servlet.http.HttpSessionEvent;
import javax.servlet.http.HttpSessionListener;

public class MyHttpSessionListener implements HttpSessionListener {
    @Override
    public void sessionCreated(HttpSessionEvent se) {
        System.out.println("MyHttpSessionListener....sessionCreated....");
        // 在监听器中只要判断session创建，在线人数就加一
        ServletContext context = se.getSession().getServletContext();
        // 获取里面的在线人数
        Integer onlineNum = (Integer) context.getAttribute("onlineNum");
        onlineNum = onlineNum + 1;
        context.setAttribute("onlineNum", onlineNum);
    }

    @Override
    public void sessionDestroyed(HttpSessionEvent se) {
        System.out.println("MyHttpSessionListener....sessionDestroyed....");
        // 在监听器中只要判断session销毁，在线人数就减去一
        ServletContext context = se.getSession().getServletContext();
        // 获取里面的在线人数
        Integer onlineNum = (Integer) context.getAttribute("onlineNum");
        onlineNum = onlineNum - 1;
        context.setAttribute("onlineNum", onlineNum);
    }
}
```

## 9、属性变化的监听

### 9.1、属性监听器介绍

主要是监听使用setAttribute、removeAttribute放在



ServletContextAttributeListener 专门用于监听ServletContext对象中的属性的变化情况；

HttpSessionAttributeListener 专门用于监听session对象中的属性的变化情况；

ServletRequestAttributeListener 专门用于监听request对象中的属性的变化情况；

她们中的监听 添加、删除、修改的方法名称全部一致：

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213536431-293806393.png)

代码演示： 

```jsp
<%
	//添加数据
	session.setAttribute("addr",111);
	//替换数据
	session.setAttribute("addr",222);
	//删除数据
	session.removeAttribute("addr")
%>
```

监听器： 

```java
package cn.itcast.listener;

import javax.servlet.http.HttpSessionAttributeListener;
import javax.servlet.http.HttpSessionBindingEvent;

public class MyHttpSessionAttributeListener implements HttpSessionAttributeListener {

    @Override
    public void attributeAdded(HttpSessionBindingEvent se) {
        System.out.println("MyHttpSessionAttributeListener....attributeAdded...");
    }

    @Override
    public void attributeRemoved(HttpSessionBindingEvent se) {
        System.out.println("MyHttpSessionAttributeListener....attributeRemoved...");
    }

    @Override
    public void attributeReplaced(HttpSessionBindingEvent se) {
        System.out.println("MyHttpSessionAttributeListener....attributeReplaced...");
    }

}
```

配置文件：

```xml
<listener>
        <listener-class>cn.itcast.listener.MyHttpSessionAttributeListener</listener-class>
</listener>
```

## 10、Bean监听演示

### 10.1、session中的bean监听

当我们给Session中保存一个Java对象的时候，或者把Java对象从Session中移除的时候会触发专门用来监听Session中对象变化的监听器中的方法。拥有这个方法的对象——HttpSessioBindingListener接口。

### 10.2、属性监听和bean监听的区别

属性监听：是对三个容器中的任何属性（包括对象和不是对象的数据，基本类型数据）的变化，进行监听。

Bean监听：它只监听JavaBean对象网session中保存和session中移除的过程。

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213536697-2140716158.png)

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213537494-363098760.png)

由于HttpSessionBindingListener是用来监听某个JavaBean对象的绑定和解绑的，所以这个监听器的实现类必须是被操作的，JavaBean（HttpSessionBindingListener不需要在web.xml中配置）

* javaBean：

```java
package cn.itcast.domain;

import javax.servlet.http.HttpSessionBindingEvent;
import javax.servlet.http.HttpSessionBindingListener;

public class User implements HttpSessionBindingListener{

    private int age;
    private String name;
    
    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User [age=" + age + ", name=" + name + "]";
    }

    @Override
    public void valueBound(HttpSessionBindingEvent event) {
        System.out.println("User....valueBound...");
    }

    @Override
    public void valueUnbound(HttpSessionBindingEvent event) {
        System.out.println("User....valueUnbound...");
    }
}
```

* JSP

```jsp
<%
     session.setAttribute("user", new User());
     session.removeAttribute("user");
%>
```

![](https://images2015.cnblogs.com/blog/725943/201701/725943-20170110213537900-745710388.png)


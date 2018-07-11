###  1. Session的概念

#### 	1.1 Web服务跟踪客户状态通常有四种方法

1. 建立含有跟踪数据的隐藏字段

2. 重写包含额外参数的URL

3. 使用持续的Cookie

4. 使用Servlet API 中的Session

* Session用于跟踪客户的状态。Session指的是在一段时间内，单个客户与Web服务器的一连串相关的交互过程。在一个Session中，客户可能会多次请求访问同一个网页，也有可能请求访问各种不同的服务器资源。

  例子：

  ​	在电子邮件应用中，从一个客户登录到电子邮件系统开始，经过收信、写信和发信等一系列操作，直至最后退出邮件系统，整个过程为一个Session。

  ​	在购物网站应用中，从一个客户开始购物，到最后结账，整个过程为一个Session。


#### 1.2 Session的运行机制

​	当一个Session开始时，Servlet容器将创建一个HttpSession对象，在HttpSession对象中可以存放客户状态的信息（例如购物车）

  	Servlet容器为HttpSession分配一个唯一标志符，称为Session ID。Servlet容器把Session ID作为Cookie保存在客户的浏览器中。

​	每次客户发出HTTP请求时，Servlet容器可以从HttpServletRequest对象中读取Session ID，然后根据Session ID 找到相应的HttpSession对象，从而获取客户的状态信息。

### 2. HttpSession API

| 方法                                     | 作用                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| getId（）                                | 返回Session的ID                                              |
| invalidate（）                           | 使当前的Session失效，Servlet容器会释放HttpSession对象占用的资源 |
| setAttribuate(String name, Object value) | 将一对name/value属性保存在HttpSession对象中                  |
| getAttribute(String name)                | 根据 name参数返回保存在HttpSession对象中的属性值             |
| isNew()                                  | 判断是否是新创建的Session。如果是新创建的Session ，返回true，否则返回false |
| setMaxInactiveInterval()                 | 设定一个Session可以处于不活动状态的最大时间间隔， 以秒为单位。如果超过这个时间，Session自动失效。如 果设置为负数，表示不限制Session处于不活动状态的时 间 |



### 3. Session的生命周期

​	当客户第一次访问Web应用中支持Session的某个网页时，就会开始一个新的Session

​	接下来当客户浏览这个Web应用的不同网页时，始终处于同一个Session中

​	默认情况下，JSP网页都是支持Session的，也可以通过以下语句显示声明支持Session：

​	`<%@ page session="true">`

​	在以下情况中，Session将结束生命周期，Servlet容器会将Session所占用的资源释放掉：

1. 客户端关闭浏览器（真的是这样吗）；
2. Session过期；
3. 服务器端调用了HttpSession的invalidate（）方法；



#### 3.1 如何做到在浏览器关闭时删除Session

​	严格的讲，做不到这一点。可以做一点努 力的办法是在所有的客户端页面里使用 javascript代码window.onclose来监视浏 览器的关闭动作，然后向服务器发送一个 请求来删除session。 

​	但是对于浏览器崩溃或者强行杀死进程这 些非常规手段仍然无能为力。

​	实际上在项目中我们也不会这么做,而是让 服务器在Session过期时将其删除  

#### 3.2 Session过期

​	Session过期是指当Session开始后，在一 段时间内客户没有和Web服务器交互，这 个Session会失效，HttpSession的 setMaxInactiveInterval()方法可以设置 允许Session保持不活动状态的时间（以秒 为单位），如果超过这一时间，Session就 会失效。 

### 4. 在JSP文件中控制Session

### 5. 在JSP文件中设置Session范围内的共享数据


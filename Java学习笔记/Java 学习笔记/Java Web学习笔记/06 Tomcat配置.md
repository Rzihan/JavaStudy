1. 首先需要配置Tomcat，使得能够正常启动
2. Tomcat安装完毕需要将jre换成jdk
3. 需要配置好如下三个环境变量：

>JAVA_HOME
>CATALINA_HOME
>PATH

4. 在Tomcat安装目录的conf目录下打开server.xml文件，找到倒数第四行</Host>,在</Host>上面加入如下XML片段

><Context path="/test" docBase="D:\shengsiyuan2\test\WebRoot" reloadable="true"/>

5. 启动Tomcat(startup.bat),打开浏览器，访问如下地址：

>http://localhost:8080/test/login.jsp

6. Servlet是JAVA服务器端编程，不同于我们之前写的一般的JAVA应用程序，Servlet程序是运行在服务器上的，服务器有很多种，本课程用到的服务器就是Tomcat
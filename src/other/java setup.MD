# Java环境设置
 
- 1.打开我的电脑--属性--高级--环境变量 

- 2.新建系统变量JAVA_HOME 和CLASSPATH 
  - 变量名：JAVA_HOME 变量值：C:\Program Files\Java\jdk1.7.0
  - 变量名：CLASSPATH 变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;

- 3.选择“系统变量”中变量名为“Path”的环境变量，双击该变量，把JDK安装路径中bin目录的绝对路径，添加到Path变量的值中，并使用半角的分号和已有的路径进行分隔。 
  - 变量名：Path 变量值：%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;

这是java的环境配置，配置完成后直接启动eclipse，它会自动完成java环境的配置


# Tomcat 7免安装版

- Tomcat7安装和配置
  - 下载zip文件之后直接解压到某个目录下，比如：C:\itdevelop\Tomcat7。
  - 然后在我的电脑->属性->高级->环境变量->系统变量中添加以下环境变量：
    - 新建变量名: TOMCAT_HOME, 值(value)为：C:\itdevelop\Tomcat7
    - 变量名: Path, 增加值：%TOMCAT_HOME%\common\lib;
    - 最后进入Tomcat7安装目录下的Bin目录，启动Tomcat.
  - 在浏览器中输入： http://localhost:8080/ ，若可以看到Tomcat7的欢迎界面，表示Tomcat7配置成功了。


# 新建webApp

这里介绍如何搭建一个JSP简单的应用。首先到Tomcat7目录下webapps目录，例如：C:\itdevelop\Tomcat7\webapps，该目录存放了ROOT，docs,examples等目录，ROOT存放的是欢迎界面的代码，docs主要是文档，examples中可以查看各种例子。接下来看看如何新建一个属于自己的jsp应用程序。

- 操作如下：
  - 1.在webapps下新建myapp目录。
  - 2.myapp下新建一个目录WEB-INF，注意，目录名称是区分大小写的。
  - 3.WEB-INF下新建一个文件web.xml，内容如下: 
```
<?xml version="1.0" encoding="ISO-8859-1"?>
<web-app version="3.0" xmlns="http://java.sun.com/xml/ns/javaee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://java.sun.com/xml/ns/javaeehttp://java.sun.com/xml/ns/javaee/web-app_3_0.xsd">
  <display-name>My Web Application</display-name>
  <description>A application for test.</description>
</web-app>
```
  - 4. 在myapp下新建一个测试的jsp页面，文件名为index.jsp，文件内容如下:
```
<html>
<body>
  <center>Now time is: <%=new java.util.Date()%></center>
</body>
</html>
```
  - 5. 启动Tomcat,在浏览器输入 http://localhost:8080/myapp/index.jsp 看到当前时间的话说明就成功了。

# 新建Servlet
- 在之前myapp目下的/WEB-INF/classes/test目录下新建HelloWorld.java(若没有class,test目录，请新建)。 HelloWorld内容如下：
```
package test; import java.io.*;
import javax.servlet.*; import javax.servlet.http.*;

public class HelloWorld extends HttpServlet{
  public void doGet(HttpServletRequest request,HttpServletResponse response)throws ServletException,IOException{response.setContentType("text/html");
    PrintWriter out = response.getWriter();
    out.println("<html><head><title>"); 
    out.println("This is my first Servlet"); 
    out.println("</title></head><body>");
    out.println("<h1>Hello,World!</h1>");
    out.println("</body></html>"); 
   }
}
```

- 之后用javac HelloWorld.java来编译该文件。倘若出现”package javax.servlet does not exist“，请把C:\itdevelop\Tomcat7\lib目录下的servlet-api.jar拷贝到C:\Program Files\Java\jre6\lib\ext，重启电脑，再次编译即可。 目前C:\itdevelop\Tomcat7\webapps\myapp的目录结构如下： ./index.jsp  ./WEB-INF/web.xml  ./WEB-INF/classes/test/HelloWorld.class (编译HelloWorld.java生成的) 然后在浏览器中输入 http://localhost:8080/myapp/HelloWorld ,于是Server众望所归的报错了:Error 404–Not Found 怎么回事呢？我们还需要配置Servlet的执行环境。打开WEB-INF目录下的web.xml，在<web-app></web-app>添加下面这段程序： 

```
<servlet>
  <servlet-name>HelloWorld</servlet-name>
  <servlet-class>test.HelloWorld</servlet-class>
</servlet>
<servlet-mapping>
  <servlet-name>HelloWorld</servlet-name>
  <url-pattern>/HelloWorld</url-pattern>
</servlet-mapping>
```

   这段xml内容，首先指定servlet的名字，类的名字。然后把servlet映射到一种URL模式，使得通过URL来访问这个servlet。修改之后，若需要重启Tomcat,然后浏览http://localhost:8080/myapp/HelloWorld一个Hello,World!等着你，如果你看到了，表示servlet也成功了。

# jboss-web.xml 加入一个域名
- `<virtual-host>www.lucky.com</virtual-host>`

  - request.forward	rewrite
  - response.redirect	redirect


# servlet

创建项目目录结构： 在您的工作目录中创建以下目录结构
```bash
PasswordManager/
├── WEB-INF/
│   ├── classes/
│   └── lib/
└── index.html
```
这里，PasswordManager是项目根目录，WEB-INF目录包含Web应用程序的配置文件和类文件，classes目录用于存放编译后的Java类文件，lib目录用于存放项目依赖的库文件。
创建Servlet类： 在WEB-INF/classes目录下创建一个名为PasswordManagerServlet.java的文件。在这个文件中，编写一个继承自javax.servlet.http.HttpServlet的Java类。例如：
```java
import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/PasswordManagerServlet")
public class PasswordManagerServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 处理GET请求
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 处理POST请求
    }
}
```
编译Servlet类： 使用Java编译器（如javac）编译PasswordManagerServlet.java文件。在命令行中，导航到WEB-INF/classes目录，然后运行以下命令：
javac -cp "path/to/tomcat/lib/servlet-api.jar" PasswordManagerServlet.java
将path/to/tomcat替换为您的Tomcat安装目录。这将生成一个名为PasswordManagerServlet.class的文件。
配置web.xml文件： 在WEB-INF目录下创建一个名为web.xml的文件。在这个文件中，配置Servlet映射和其他Web应用程序设置。例如：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                             http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1">
   <servlet>
       <servlet-name>PasswordManagerServlet</servlet-name>
       <servlet-class>PasswordManagerServlet</servlet-class>
    </servlet>
   <servlet-mapping>
       <servlet-name>PasswordManagerServlet</servlet-name>
        <url-pattern>/PasswordManagerServlet</url-pattern>
    </servlet-mapping>
</web-app>
```
部署Web应用程序： 将整个PasswordManager目录复制到Tomcat的webapps目录下。然后，启动Tomcat服务器。Tomcat将自动部署您的Web应用程序。
访问Servlet： 在浏览器中访问http://localhost:8080/PasswordManager/PasswordManagerServlet（或您配置的其他端口），您应该能够看到Servlet处理的请求。
请注意，这种方法可能不如使用IDE方便，但它可以让您更深入地了解Java Web应用程序的开发过程


# JSP
在不使用集成开发环境(IDE)的情况下创建一个JSP Web项目需要手动配置和编写一些基础文件。以下是一个基本步骤指南来帮助你从零开始创建这样一个项目：

### 1. 准备工作

- **安装Java**: 确保你的计算机上安装了Java Development Kit (JDK)。你可以从Oracle的官方网站下载适合你操作系统的JDK版本。
- **设置JAVA_HOME环境变量**: 配置JAVA_HOME指向JDK的安装目录。
- **安装Tomcat服务器**: Tomcat是运行JSP和Servlet的常用服务器。从Apache Tomcat官网下载并解压到你选择的目录。
- **设置CATALINA_HOME环境变量** (可选): 如果你需要，可以设置这个环境变量指向Tomcat的安装目录。

### 2. 创建项目结构

在你希望存放项目的目录下，手动创建以下目录结构：

```
/myWebApp
  /WEB-INF
    web.xml
  /jsp
    index.jsp
  /css
  /js
  /images
```

- `/myWebApp`: 你的项目根目录。
- `/WEB-INF`: 包含配置文件和类文件的私有目录。
- `web.xml`: 应用程序部署描述符，位于`WEB-INF`目录下，用于配置servlet、欢迎页面等。
- `/jsp`: 存放JSP文件的目录。
- 其他如`/css`, `/js`, `/images`用于存放前端资源。

### 3. 编写web.xml

在`WEB-INF`目录下创建`web.xml`文件，并添加基础配置。例如，设置欢迎页面：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
         http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <welcome-file-list>
        <welcome-file>jsp/index.jsp</welcome-file>
    </welcome-file-list>
</web-app>
```

### 4. 编写JSP文件

在`/jsp`目录下创建`index.jsp`文件，这是你的网页入口点：

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>My First JSP Page</title>
</head>
<body>
    <h1>Hello, World!</h1>
</body>
</html>
```

### 5. 部署并运行

- 将整个`myWebApp`目录复制到Tomcat的`webapps`目录下。
- 启动Tomcat服务器。通常可以通过在命令行进入Tomcat的`bin`目录，然后执行`startup.sh`(Linux/macOS)或`startup.bat`(Windows)来完成。
- 打开浏览器，访问`http://localhost:8080/myWebApp/`（假设Tomcat的默认端口是8080），你应该能看到你的JSP页面。

以上就是不使用开发工具创建JSP Web项目的基本步骤。虽然手动配置和管理项目比较繁琐，但它能帮助你更深入地理解Web应用的工作原理。随着项目复杂度的增加，使用像Eclipse、IntelliJ IDEA这样的IDE会更加高效。


要创建一个简单的JSP Web服务，用于显示数据、并实现对MySQL数据库的增删改查功能，你需要遵循以下步骤。这里我将提供一个基础示例来帮助你开始。请注意，在实际部署中，你应该考虑使用诸如Spring Boot或Struts这样的框架来更高效、安全地处理Web请求和数据库操作。

### 1. 准备工作

确保你已经安装了Java开发环境（JDK）和Tomcat服务器，并且你的系统中已安装MySQL数据库。还需要下载并配置MySQL的JDBC驱动（Connector/J）。

### 2. 创建数据库和表

首先，在MySQL中创建一个数据库和表作为例子：

```sql
CREATE DATABASE mydatabase;
USE mydatabase;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(50) UNIQUE NOT NULL
);
```

### 3. 添加MySQL JDBC驱动到项目

将MySQL的JDBC驱动（例如mysql-connector-java-x.x.xx.jar）添加到项目的`WEB-INF/lib`目录下。

### 4. 编写JSP页面

创建一个名为`index.jsp`的文件，用于显示用户列表，并提供增删改查的表单或链接。

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>User Management</title>
</head>
<body>
    <h2>User List</h2>
    <%
        // 这里仅为示意，实际应用中应使用DAO模式或Service层处理数据库操作
        Class.forName("com.mysql.cj.jdbc.Driver");
        java.sql.Connection conn = DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/mydatabase", "username", "password");
        Statement stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM users");
        while (rs.next()) {
            out.println("ID: " + rs.getInt("id") + ", Name: " + rs.getString("name") + ", Email: " + rs.getString("email") + "<br>");
        }
        rs.close();
        stmt.close();
        conn.close();
    %>
    <!-- 实现增删改查的链接或表单可以在这里添加 -->
</body>
</html>
```

### 5. 配置web.xml

在`WEB-INF`目录下，确保你有`web.xml`文件来配置应用程序的入口点。对于这个简单的例子，直接访问JSP页面即可，无需额外配置。

### 6. 部署到Tomcat

将整个项目打包成WAR文件，或者直接将项目目录放到Tomcat的`webapps`目录下，然后启动Tomcat服务器。

### 注意事项

- **安全性**：上述代码直接在JSP页面中进行数据库操作是不推荐的做法，因为这会暴露数据库登录信息，并且不符合MVC设计模式。在实际应用中，应该将数据库操作放在Servlet或独立的Java类（如DAO）中。
- **错误处理**：示例中没有包含任何错误处理逻辑，实际应用时需要添加异常捕获和处理。
- **参数化查询**：为了防止SQL注入攻击，应使用PreparedStatement进行参数化查询。

以上是一个非常基础的例子，仅用于演示目的。在实际开发中，建议采用更先进的技术栈和设计模式来提升应用的安全性、可维护性和性能。
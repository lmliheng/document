### JDBC（1）
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class MySQLExample {
    public static void main(String[] args) {
        try {
            // 加载JDBC驱动程序
            Class.forName("com.mysql.cj.jdbc.Driver");

            // 创建数据库连接
            String url = "jdbc:mysql://8.134.79.236:3306/twe?useSSL=false&serverTimezone=UTC";
            String username = "twe";
            String password = "13551458597a";
            Connection connection = DriverManager.getConnection(url, username, password);

            // 创建Statement对象，用于与数据库进行交互。可以使用此Statement对象执行SQL语句，如插入数据到数据库表中
            Statement statement = connection.createStatement();

            // 创建employees表
            String createTableQuery = "CREATE TABLE IF NOT EXISTS employees (" +
                    "id INT AUTO_INCREMENT PRIMARY KEY," +
                    "name VARCHAR(50)," +
                    "age INT," +
                    "salary DECIMAL(10, 2)" +
                    ")";
            statement.executeUpdate(createTableQuery);

            // 插入数据
            String insertQuery = "INSERT INTO employees (name, age, salary) VALUES ('John Doe', 30, 50000.00)";
            statement.executeUpdate(insertQuery);

            // 查询数据
            String selectQuery = "SELECT * FROM employees";
            ResultSet resultSet = statement.executeQuery(selectQuery);

            // 输出查询结果
            while (resultSet.next()) {
                int id = resultSet.getInt("id");
                String name = resultSet.getString("name");
                int age = resultSet.getInt("age");
                double salary = resultSet.getDouble("salary");
                System.out.println("ID: " + id + ", Name: " + name + ", Age: " + age + ", Salary: " + salary);
            }

            // 关闭资源
            resultSet.close();
            statement.close();
            connection.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
### JDBC资源终止
```java
package com.example;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.sql.SQLException;

public class LoginSelect {
    public static void main(String[] args) {
        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;

        try {
            // 加载JDBC驱动程序
            Class.forName("com.mysql.cj.jdbc.Driver");

            // 创建数据库连接
            String url = "jdbc:mysql://8.134.79.236:3306/twe?useSSL=false&serverTimezone=UTC";
            String username = "twe";
            String password = "13551458597a";
            connection = DriverManager.getConnection(url, username, password);

            // 创建Statement对象，用于与数据库进行交互
            statement = connection.createStatement();

            // 查询数据
            String selectQuery = "SELECT * FROM users";
            resultSet = statement.executeQuery(selectQuery);

            // 输出查询结果
            while (resultSet.next()) {
                int id = resultSet.getInt("id");
                String Username = resultSet.getString("username");
                String Password = resultSet.getString("password");
                System.out.println("ID: " + id + ", Username: " + Username + ", Password: " + Password);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // 关闭资源
            if (resultSet != null) {
                try {
                    resultSet.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (statement != null) {
                try {
                    statement.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (connection != null) {
                try {
                    connection.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```
### 登录查询模拟
```java
            // 模拟登录效果

            boolean IsLoginSuccess = false;

            String username = "admin";
            String password = "123456";

            ResultSet rs = statement.executeQuery("select * from users where username ='"+ username +"'and password='"+password +"'");

            while (rs.next())
            {
                IsLoginSuccess = true;
            }

            System.out.println("登录结果为"+IsLoginSuccess);
            // 关闭资源
            rs.close();
```            

### 本地mysql
目录:`C:\mysql\mysql-5.7.44-winx64\mysql-5.7.44-winx64`
root密码：`13551458597a`

### JDBC

拉取[mysql-connector-j](https://downloads.mysql.com/archives/c-j/)
连接数据库操作:
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
编译：`javac -cp .;C:\Users\李恒\Desktop\code\java\mysql-connector-j-8.3.0\mysql-connector-j-8.3.0\mysql-connector-j-8.3.0.jar -encoding UTF-8 MySQLExample.java`
运行:`java -cp .;C:\Users\李恒\Desktop\code\java\mysql-connector-j-8.3.0\mysql-connector-j-8.3.0\mysql-connector-j-8.3.0.jar MySQLExample`

```java
C:\Users\李恒\Desktop\code\java\JDBC>javac -cp .;C:\Users\李恒\Desktop\code\java\mysql-connector-j-8.3.0\mysql-connector-j-8.3.0\mysql-connector-j-8.3.0.jar -encoding UTF-8 MySQLExample.java

C:\Users\李恒\Desktop\code\java\JDBC>java -cp .;C:\Users\李恒\Desktop\code\java\mysql-connector-j-8.3.0\mysql-connector-j-8.3.0\mysql-connector-j-8.3.0.jar MySQLExample
ID: 1, Name: John Doe, Age: 30, Salary: 50000.0

C:\Users\李恒\Desktop\code\java\JDBC>
```
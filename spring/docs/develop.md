## 开发环境检查

1. [创建](https://start.spring.io/)springboot项目，并添加依赖spring web
2. maven安装依赖
3. 创建在 src/main/java 目录下，创建一个新的 Java 类文件，例如 MyController.java。
在新创建的 Java 类文件中，添加以下代码：
```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {

    @GetMapping("/my-endpoint")
    public String myEndpoint() {
        return "Hello, World!";
    }
}
```
在这个例子中，我们创建了一个名为 MyController 的控制器类，并使用 @RestController 注解标记它。我们还定义了一个名为 myEndpoint 的方法，并使用 @GetMapping 注解将其映射到 /my-endpoint URL。当用户访问 /my-endpoint URL 时，myEndpoint 方法将被调用，并返回 "Hello, World!" 字符串作为响应。

4. 保存并重新编译你的项目。

### 注意

1. 冗余声明

## thymeleaf
mvc与传统的三层架构不一样，使用view层来处理视图，model层来处理数据，controller层来处理业务逻辑。
采用前后端不分离就要使用模板引擎，Thymeleaf是Spring官方推荐使用的模板引擎，可以轻易与MVC等web架构集成

### 使用
1) 引入依赖
```java
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-thymeleaf</artifactId>
		</dependency>
```
2) 配置缓存机制
```properties
spring.thymeleaf.cache=false    
```
3) 编写控制器
```java
package com.example.demo;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HelloWorldMvcController {
 @RequestMapping("/helloworld")
 public String helloWorld(Model model) throws Exception {{
  model.addAttribute("message", "Hello World!");
  return "index";
  }
 }
}
```
4) 编写视图
```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <link rel="Shortcut Icon" href="http://web.yunduanjianzhan.cn/images/logos/favicon.ico" type="image/x-icon" />
    <title>恒加瓦</title>
</head>

<body>
<h1 th:text="${message}">表头</h1>
</body>

</html>
```
 
 
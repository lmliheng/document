## 注解（annotation）式编程

###  
```java
import org.springframework.boot.SpringApplication; // 导入 SpringApplication 类，用于启动 Spring Boot 应用程序
```
`import org.springframework.boot.autoconfigure.SpringBootApplication; `是一个 Java 导入语句，用于导入 `Spring Boot` 框架中的 `SpringBootApplication `注解

`SpringBootApplication` 注解是一个组合注解，它包含了以下三个注解：
`@Configuration`：表示这是一个配置类，用于定义应用程序的配置信息。
`@EnableAutoConfiguration`：表示启用`Spring Boot `的自动配置功能。Spring Boot 会根据项目的依赖和配置自动配置应用程序。
`@ComponentScan`：表示启用组件扫描功能。Spring Boot 会自动扫描指定包（默认为当前包及其子包）下的所有组件（如控制器、服务、仓库等），并将它们注册到 Spring 容器中。
初始化项目
```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);

	}

}
```

### RestController和GetMapping 
```java
package com.example.demo; // 定义包名为 com.example.demo

import org.springframework.web.bind.annotation.GetMapping; 
// 导入 GetMapping 注解，用于映射 HTTP GET 请求到方法
import org.springframework.web.bind.annotation.RestController;
 // 导入 RestController 注解，用于标记控制器类

// 使用 RestController 注解标记这个类，表示它是一个控制器类，负责处理 HTTP 请求
@RestController
public class MyController {

    // 使用 GetMapping 注解将 HTTP GET 请求映射到 index 方法
    @GetMapping("/index")
    // myEndpoint 方法返回字符串作为响应
    public String index() {
        retur
```        
### 系统注解
`@Override`覆写
`@Deprecated`
`@SuppressWarnings`

### 常见注解
`@Controller`标记在类上，定义控制器类，然后分发处理器会扫描该类中的方法是否使用 @RequestMapping 注解，并自动将方法映射到指定的 URL 上。

`@RestController`版本springboot4.0后出现，@Controller和@RestController功能一样，都是用来标记控制器类，但是@RestController返回的是json数据（等价于@Controller加@ResponseBody），@Controller返回的是视图。使用它来标志Rest风格的控制器类

`@RequestMapping`
处理请求地址映射的映射,
RequestMapping的属性有： 
value：请求地址
method：请求方式如GET，POST,PUT,PATCH,DELETE,OPTIONS,TRACE
params：请求参数
headers：请求头
consumes：请求类型如json,xml,text/html
produces：返回类型


`@GetMapping`

`@PathVariable`

`@Service`



        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        "Hello,我是恒";
    }

    // 使用 GetMapping 注解将 HTTP GET 请求映射到 inde 方法
    @GetMapping("/inde")
    // myEndpoint 方法返回 字符串作为响应
    public String inde() {
        return "Hello";
    }
}
```
名为 `MyController` 的控制器类，它使用 `@RestController` 注解标记。在控制器中，有一个名为 myEndpoint 的方法，它使用` @GetMapping `注解将` HTTP GET `请求映射到 `/index URL`。当用户访问` /index URL `时，myEndpoint 方法将被调用，并返回字符串作为响应。


### 
## springboot插件

注意：`spring-boot-maven-plugin`需要指定版本

打开Maven本地仓库。查看/org/springframework/boot路径下的spring-boot-maven-plugin文件夹底下，是否存在与springboot的版本相对应版本号
如果存在，添加<version>标签为自己的springboot版本
```bash
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>2.7.5</version>
            </plugin>
        </plugins>
    </build>
```    
Maven 项目中包含此插件，可以访问以下功能：
 1. **重新打包**：它可以将您的应用程序重新打包为可执行的 JAR/WAR，其中包括 JVM 的打包版本和运行应用程序所需的依赖项
 2. **Spring Boot Runner**：它允许您使用“mvn spring-boot：run”目标直接从命令行运行应用程序
 3. **启动器和依赖关系管理**：它允许包含自动添加常用库和配置的“启动器”，从而简化了依赖关系管理


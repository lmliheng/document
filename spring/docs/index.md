## 主页
hello,我是恒
## 文档版权
```java
/** 
*Copyright(C),2024 Centre Southn University
*FileName: SpringBoot
*Author:liheng
*License: MIT
*Description: 随缘维护
*Version: V1.0
*History: None
*/
```


### 环境配置
`IDE`:idea

`JDK`:21

`Maven配置`：

1. 版本:3.95
2. settings.xml文件路径:C:/users/Administrator/.m2/settings.xml
3. settings.xml文件内容:
4. maven路径：C:/users/Administrator/.m2/repository/

`依赖`:
1. Spring Web 
2. Lombok
### 项目目录结构:
```bash
├───demo/
│   ├───.gitignore
│   ├───HELP.md
│   ├───mvnw
│   ├───mvnw.cmd
│   ├───pom.xml
│   ├───.mvn/
│   │   ├───wrapper/
│   │   │   ├───maven-wrapper.jar
│   │   │   ├───maven-wrapper.properties
│   ├───src/
│   │   ├───main/
│   │   │   ├───java/
│   │   │   │   ├───com/
│   │   │   │   │   ├───example/
│   │   │   │   │   │   ├───demo/
│   │   │   │   │   │   │   ├───DemoApplication.java
│   │   │   ├───resources/
│   │   │   │   ├───application.properties
│   │   │   │   ├───static/
│   │   │   │   ├───templates/
│   │   ├───test/
│   │   │   ├───java/
│   │   │   │   ├───com/
│   │   │   │   │   ├───example/
│   │   │   │   │   │   ├───demo/
│   │   │   │   │   │   │   ├───DemoApplicationTests.java
```

### Maven项目结构
一个使用Maven管理的普通的Java项目,目录结构默认如下：
```
a-maven-project
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   └── resources
│   └── test
│       ├── java
│       └── resources
└── target
```
项目的根目录`maven-project`是项目名，它有一个项目描述文件`pom.xml`，存放Java源码的目录是`src/main/java`，存放资源文件的目录是`src/main/resources`，存放测试源码的目录是`src/test/java`，存放测试资源的目录是`src/test/resources`，最后，所有编译、打包生成的文件都放在`target`目录里

### banner.txt
```java
/***
 *                    _ooOoo_
 *                   o8888888o
 *                   88" . "88
 *                   (| -_- |)
 *                    O\ = /O
 *                ____/`---'\____
 *              .   ' \\| |// `.
 *               / \\||| : |||// \
 *             / _||||| -:- |||||- \
 *               | | \\\ - /// | |
 *             | \_| ''\---/'' | |
 *              \ .-\__ `-` ___/-. /
 *           ___`. .' /--.--\ `. . __
 *        ."" '< `.___\_<|>_/___.' >'"".
 *       | | : `- \`.;`\ _ /`;.`/ - ` : | |
 *         \ \ `-. \_ __\ /__ _/ .-` / /
 * ======`-.____`-.___\_____/___.-`____.-'======
 *                    `=---='
 *
 * .............................................
 *          佛祖保佑             永无BUG
 */

```
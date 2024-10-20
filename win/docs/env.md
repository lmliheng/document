### 环境变量
又称可执行文件路径，易知exe文件无需添加exe即可在命令行中运行
注意：
1.尽量使用系统变量，
2.注意路径Path 会被覆盖（PATH这些会覆盖），找回：echo %Path%
3.Path备份

### java环境变量规范

名称|路径|
| | |
JAVA_HOME|\jdk1.8.0_181的路径|
ClassPath|.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar; |
Path|%JAVA_HOME%\jre\bin|
Path|%JAVA_HOME%\bin|

### Tomcat


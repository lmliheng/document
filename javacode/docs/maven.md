## Maven构建
### 注意
使用阿里源,解决构建项目异常停止（通过运行一个简单的 Maven 命令来检查代理或镜像是否生效，例如 mvn help:effective-pom）

### 项目构建
更新Maven仓库
```bash
mvn install
或者
mvn clean install -U
```
运行`mvn archetype:generate`命令： 在新创建的目录下运行mvn archetype:generate命令，以创建一个Maven项目
```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=my-java-client -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```
这将在当前目录下创建一个名为my-java-client的Maven项目，其中groupId为com.example。根据需要修改这些值。
编写Java代码： 在`src/main/java/com/example`目录下创建一个新的Java类，例如MyJavaClient.java。
编译和运行项目： 在命令行或终端中，进入项目根目录，然后运行以下命令以编译和运行项目：
```bash
mvn compile
mvn exec:java -Dexec.mainClass="com.example.MyJavaClient"
```
这将编译Java代码并运行MyJavaClient类。



## 手动构建

```bash
javac -d bin src\com\hutubill\*.java src\com\hutubill\dao\*.java src\com\hutubill\entity\*.java src\com\hutubill\gui\*.java src\com\hutubill\service\*.java src\com\hutubill\startup\*.java src\com\hutubill\test\*.java src\com\hutubill\util\*.java
```

### maven配置
配置文件settings.xml
```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
   
   <!-- 本地仓库的位置 -->
   <localRepository>C:\Users\李恒\.m2\repository</localRepository>

    <!-- 镜像设置，用于指定中央仓库的镜像，以提高依赖项下载的速度 -->
    <mirrors>
        <!-- 阿里私服 -->
        <mirror>
            <id>alimaven</id>
            <mirrorOf>central</mirrorOf>
            <name>aliyun maven</name>
            <url>http://maven.aliyun.com/nexus/content/repositories/central/</url>
        </mirror>

        <!-- 中央仓库1 -->
        <mirror>
            <id>repo1</id>
            <mirrorOf>central</mirrorOf>
            <name>Human Readable Name for this Mirror.</name>
            <url>http://repo1.maven.org/maven2/</url>
        </mirror>

        <!-- 中央仓库2 -->
        <mirror>
            <id>repo2</id>
            <mirrorOf>central</mirrorOf>
            <name>Human Readable Name for this Mirror.</name>
            <url>http://repo2.maven.org/maven2/</url>
        </mirror>
    </mirrors>

</settings>

```

### 手动写入本地仓库

```bash
C:\Users\李恒\Desktop\Easybbs源码_全部源码\easybbsall\easybbs-front-admin\easybbs-front-admin>mvn install:install-file -Dfile=C:/Users/李恒/Desktop/Easybbs源码_全部源码/easybbsall/easybbs-java/easybbs-java/easybbs-java/easybbs-common/target
/easybbs-common-1.0.jar -DgroupId=com.easybbs -DartifactId=easybbs-common -Dversion=1.0 -Dpackaging=jar
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------< org.apache.maven:standalone-pom >-------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] --------------------------------[ pom ]---------------------------------
[INFO]
[INFO] --- install:3.1.1:install-file (default-cli) @ standalone-pom ---
[INFO] Installing C:\Users\鏉庢亽\Desktop\Easybbs婧愮爜_鍏ㄩ儴婧愮爜\easybbsall\easybbs-java\easybbs-java\easybbs-java\easybbs-common\target\easybbs-common-1.0.jar to C:\Users\鏉庢亽\.m2\repository\com\easybbs\easybbs-common\1.0\easybbs-common-1.0.jar
[INFO] Installing C:\Users\鏉庢亽\AppData\Local\Temp\easybbs-common-1.0826069367780022559.pom to C:\Users\鏉庢亽\.m2\repository\com\easybbs\easybbs-common\1.0\easybbs-common-1.0.pom
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.271 s
[INFO] Finished at: 2024-06-08T00:33:12+08:00
[INFO] ------------------------------------------------------------------------

C:\Users\李恒\Desktop\Easybbs源码_全部源码\easybbsall\easybbs-front-admin\easybbs-front-admin>
```
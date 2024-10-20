### (1)
```bash
C:\Users\李恒\Desktop\code\java\GUI\SimpleCodeEditor.java:44:2
java: 进行语法分析时已到达文件结尾
```

### (2)
```bash
C:\Users\李恒\Desktop\code\java\aliyun_java_sdk_3.10.2>java -cp ".;C:\Users\李恒\Desktop\code\java\aliyun_java_sdk_3.10.2\aliyun-sdk-oss-3.10.2.jar" OSSFileManager
Exception in thread "AWT-EventQueue-0" java.lang.NoClassDefFoundError: org/apache/http/client/CredentialsProvider
        at com.aliyun.oss.OSSClient.<init>(OSSClient.java:223)
        at com.aliyun.oss.OSSClientBuilder.build(OSSClientBuilder.java:33)
        at OSSFileManager.createAndShowGUI(OSSFileManager.java:31)
        at OSSFileManager.lambda$main$0(OSSFileManager.java:26)
        at java.awt.event.InvocationEvent.dispatch(Unknown Source)
        at java.awt.EventQueue.dispatchEventImpl(Unknown Source)
        at java.awt.EventQueue.access$500(Unknown Source)
        at java.awt.EventQueue$3.run(Unknown Source)
        at java.awt.EventQueue$3.run(Unknown Source)
        at java.security.AccessController.doPrivileged(Native Method)
        at java.security.ProtectionDomain$JavaSecurityAccessImpl.doIntersectionPrivilege(Unknown Source)
        at java.awt.EventQueue.dispatchEvent(Unknown Source)
        at java.awt.EventDispatchThread.pumpOneEventForFilters(Unknown Source)
        at java.awt.EventDispatchThread.pumpEventsForFilter(Unknown Source)
        at java.awt.EventDispatchThread.pumpEventsForHierarchy(Unknown Source)
        at java.awt.EventDispatchThread.pumpEvents(Unknown Source)
        at java.awt.EventDispatchThread.pumpEvents(Unknown Source)
        at java.awt.EventDispatchThread.run(Unknown Source)
Caused by: java.lang.ClassNotFoundException: org.apache.http.client.CredentialsProvider
        at java.net.URLClassLoader.findClass(Unknown Source)
        at java.lang.ClassLoader.loadClass(Unknown Source)
        at sun.misc.Launcher$AppClassLoader.loadClass(Unknown Source)
        at java.lang.ClassLoader.loadClass(Unknown Source)
        ... 18 more
```        


### (3)
maven构建错误，阿里云源已检查（通过运行一个简单的 Maven 命令来检查代理或镜像是否生效，例如 mvn help:effective-pom）
```bash
[WARNING] The requested profile "proxy" could not be activated because it does not exist.
[ERROR] Failed to execute goal on project aliyun-ecs-demo: Could not resolve dependencies for project com.example:aliyun-ecs-demo:jar:1.0-SNAPSHOT: The following artifacts could not be resolved: com.aliyun:aliyun-java-sdk-core:jar:3.10.2 (absent), com.aliyun:aliyun-java-sdk-ecs:jar:3.10.2 (absent): com.aliyun:aliyun-java-sdk-core:jar:3.10.2 was not found in https://maven.aliyun.com/repository/public during a previous attempt. This failure was cached in the local repository and resolution is not reattempted until the update interval of aliyunmaven has elapsed or updates are forced -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/DependencyResolutionException
```

### (4)
```bash
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  1.538 s
[INFO] Finished at: 2024-05-24T01:15:55+08:00
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal on project aliyun-ecs-demo: Could not resolve dependencies for project com.example:aliyun-ecs-demo:jar:1.0-SNAPSHOT: The following artifacts could not be resolved: com.aliyun:aliyun-java-sdk-core:jar:3.10.2 (absent), com.aliyun:aliyun-java-sdk-ecs:jar:3.10.2 (absent): Could not find artifact com.aliyun:aliyun-java-sdk-core:jar:3.10.2 in alimaven (http://maven.aliyun.com/nexus/content/repositories/central/) -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/DependencyResolutionException
```

### （5）

```bash
java.lang.ClassNotFoundException: com.birosoft.liquid.LiquidLookAndFeel
        at java.net.URLClassLoader.findClass(URLClassLoader.java:387)
        at java.lang.ClassLoader.loadClass(ClassLoader.java:418)
        at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:355)
        at java.lang.ClassLoader.loadClass(ClassLoader.java:351)
        at java.lang.Class.forName0(Native Method)
        at java.lang.Class.forName(Class.java:348)
        at javax.swing.SwingUtilities.loadSystemClass(SwingUtilities.java:1879)
        at javax.swing.UIManager.setLookAndFeel(UIManager.java:582)
        at util.GUIUtil.useLNF(GUIUtil.java:99)
        at startup.Bootstrap.main(Bootstrap.java:12)
```

### (6)JDBC资源泄露
在运行过程中遇到了一个警告，这是由于MySQL连接在程序结束时没有被正确关闭。这可能会导致资源泄漏和其他问题
```bash
[WARNING] thread Thread[mysql-cj-abandoned-connection-cleanup,5,com.example.LoginSelect] will linger despite being asked to die via interruption
[WARNING] NOTE: 1 thread(s) did not finish despite being asked to via interruption. This is not a problem with exec:java, it is a problem with the running code. Although not serious, it should be remedied.
[WARNING] Couldn't destroy threadgroup org.codehaus.mojo.exec.ExecJavaMojo$IsolatedThreadGroup[name=com.example.LoginSelect,maxpri=10]
java.lang.IllegalThreadStateException
```

### (7)ClassNotFoundException
maven构建时未声明包名`package com.example;`
```bash
[WARNING]
java.lang.ClassNotFoundException: com.example.LoginSelect
```

### （8）springboot的spring-boot-maven-plugin异常
```bash
[ERROR] Failed to execute goal org.codehaus.mojo:exec-maven-plugin:3.3.0:java (default-cli) on project demo: An exception occurred while executing the Java class. DemoApplication 
```

### (9)
```bash
java.lang.ClassNotFoundException: com.birosoft.liquid.LiquidLookAndFeel
```
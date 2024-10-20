### 包路径
注意java代码里面的包名
```bash
C:\Users\李恒\Desktop\code\java\本地网络检查>javac InternetDemo
错误: 仅当显式请求注释处理时才接受类名称 'InternetDemo'
1 个错误
```

### 资源文件路径异常
问题出在ImageIcon的初始化上。NullPointerException表明在尝试创建ImageIcon时，传递给它的URL为null。这通常是因为资源文件没有正确加载。
解决：`java -cp .;C:\Users\李恒\Desktop\code\java\GUI\resources SimpleCodeEditorTwo`
```bash
C:\Users\李恒\Desktop\code\java\GUI>java SimpleCodeEditorTwo
Exception in thread "AWT-EventQueue-0" java.lang.NullPointerException
        at javax.swing.ImageIcon.<init>(Unknown Source)
        at ImageIconExample.<init>(SimpleCodeEditorTwo.java:36)
        at SimpleCodeEditorTwo.createAndShowGUI(SimpleCodeEditorTwo.java:14)
        at SimpleCodeEditorTwo.lambda$main$0(SimpleCodeEditorTwo.java:9)
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

C:\Users\李恒\Desktop\code\java\GUI>
```

### 颜色提示
```bash
C:\Users\李恒\Desktop\code\java\GUI>java CodeEditorWithSnippets
libpng warning: iCCP: known incorrect sRGB profile
libpng warning: iCCP: known incorrect sRGB profile
```


### eclipse中显示“编辑器中没有main类型
问题：在eclipse中编写程序时总会出现“编辑器中没有main类型”，但自己的程序明明就有main方法。这里其实不是程序的问题，而是导入外包的问题。

解决的方法：eclipse中的“包资源管理器”窗口，选中你所导入的包eclipse中显示“编辑器中没有main类型”（假如是“lib”文件是有我们想要运行的程序）所在的源文件包，点击右键，eclipse中显示“编辑器中没有main类型”，就会出现“构建路径”，选中后再选中“用作源文件夹”。选中之后文件夹会有变化，请仔细看右边这个eclipse中显示“编辑器中没有main类型”src包，这就是更改后的状态，之后运行就没问题了


### IDEA打jar包缺少主类
```bash
C:\Users\李恒\Desktop>java -jar my-java-client-1.0-SNAPSHOT.jar
my-java-client-1.0-SNAPSHOT.jar中没有主清单属性
```
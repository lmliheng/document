。
安装Vue CLI：Vue CLI是一个用于快速生成Vue.js项目的命令行工具。在命令行中运行以下命令以全局安装Vue CLI：
```bash
npm install -g @vue/cli
```
创建Vue.js项目：使用Vue CLI创建一个新的Vue.js项目：
```bash
vue create quiz-app
```
按照提示选择适合您需求的配置。

进入项目目录并启动开发服务器：
```bash
cd quiz-app
npm run serve
```

### package.json
注意：
dependencies：依赖会打包dist文件中。
devDependencies：依赖不会打包到dist文件中。

总结：
项目一直需要它，放dependencies；而webpack是为了方便打包上线，打包上线后就用不到了，放devdependencies。
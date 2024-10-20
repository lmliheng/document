### 全局安装create-react-app工具
```bash
npm install -g create-react-app
```

### 创建项目
```bash
create-react-app todolist
或者直接使用
npx create-react-app student-info-management
```

### 启动
```bash
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
```
运行`npm start`
```bash
Compiled successfully!

You can now view todolist in the browser.

  Local:            http://localhost:3000
  On Your Network:  http://192.168.163.1:3000

Note that the development build is not optimized.
To create a production build, use npm run build.
```
报错（1）
```bash
webpack compiled successfully
One of your dependencies, babel-preset-react-app, is importing the
"@babel/plugin-proposal-private-property-in-object" package without
declaring it in its dependencies. This is currently working because
"@babel/plugin-proposal-private-property-in-object" is already in your
node_modules folder for unrelated reasons, but it may break at any time.

babel-preset-react-app is part of the create-react-app project, which
is not maintianed anymore. It is thus unlikely that this bug will
ever be fixed. Add "@babel/plugin-proposal-private-property-in-object" to
your devDependencies to work around this error. This will make this message
go away.
```
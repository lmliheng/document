## express

使用`express 4.x`，[官方文档](https://nodejs.cn/express/4x/api/express/)

### 快速上手


安装`npm install --save express`
```javascript
const express = require('express');
const app = express();
const port = ;

app.use(express.json());

// 待办事项数组
let todos = [];

// 获取待办事项列表
app.get('/todos', (req, res) => {
  res.json(todos);
});

// 添加待办事项
app.post('/todos', (req, res) => {
  const todo = req.body;
  todos.push(todo);
  res.status(201).json(todo);
});

// 删除待办事项
app.delete('/todos/:id', (req, res) => {
  const index = todos.findIndex(t => t.id === parseInt(req.params.id));
  todos.splice(index, 1);
  res.json({ message: 'Todo deleted successfully' });
});

app.listen(port, () => {
  console.log(`Server is running at http://localhost:${port}`);
});
```
运行`npm start`
检查接口端点
post请求测试`curl -X POST -H "Content-Type: application/json" -d "{\"id\":\"1\", \"title\": \"Learn Express\", \"description\": \"Learn how to use Express.js to build web applications\"}" http://localhost:5000/todos`

再次测试GET请求：
```json
[
    {
        "id": 1,
        "title": "Learn Express",
        "description": "Learn how to use Express.js to build web applications"
    },
]    
```
测试`delate`
```bash
C:\Users\李恒>curl -X DELETE http://localhost:5000/todos/2
{"message":"Todo deleted successfully"}
```

待办事项数据存储在内存中的todos数组中。这意味着数据不会被永久保存到磁盘或数据库。
每次应用程序重启时，todos数组都会被重置为空数组，所有之前添加的待办事项都会丢失

#### 重构代码
将待办事项数据存储在内存中的todos.json文件里
```javascript
const express = require('express');
const fs = require('fs');
const app = express();
const port = 5000;

app.use(express.json());

// 从todos.json文件中读取待办事项数据
let todos = [];
fs.readFile('todos.json', 'utf-8', (err, data) => {
  if (err) {
    console.error('Error reading todos.json:', err);
  } else {
    todos = JSON.parse(data);
  }
});

// 获取待办事项列表
app.get('/todos', (req, res) => {
  res.json(todos);
});

// 添加待办事项
app.post('/todos', (req, res) => {
  const todo = req.body;
  todos.push(todo);
  // 将更新后的待办事项数据写入todos.json文件
  fs.writeFile('todos.json', JSON.stringify(todos), 'utf-8', (err) => {
    if (err) {
      console.error('Error writing todos.json:', err);
    }
  });
  res.status(201).json(todo);
});

// 删除待办事项
app.delete('/todos/:id', (req, res) => {
  const index = todos.findIndex(t => t.id === parseInt(req.params.id));
  todos.splice(index, 1);
  // 将更新后的待办事项数据写入todos.json文件
  fs.writeFile('todos.json', JSON.stringify(todos), 'utf-8', (err) => {
    if (err) {
      console.error('Error writing todos.json:', err);
    }
  });
  res.json({ message: 'Todo deleted successfully' });
});

app.listen(port, () => {
  console.log(`Server is running at http://localhost:${port}`);
});
```
提前写入json数据,运行检测
```json
[{"id":1,"title":"Learn Express","description":"Learn how to use Express.js to build web applications"},{"id":2,"title":"Build a Todo App","description":"Build a simple todo app using Express and a frontend framework"},{"id":"3","title":"Learn Express","description":"Learn how to use Express.js to build web applications"}]
```

#### 书写接口文档
待办事项API
1. 获取待办事项列表
请求方法：`GET`
请求路径：`/todos`
请求参数：`无`
响应：
状态码：`200 OK`
响应体：JSON数组，包含所有待办事项的详细信息。
示例响应：
```json
[
  {
    "id": 1,
    "title": "Learn Express",
    "description": "Learn how to use Express.js to build web applications"
  },
  {
    "id": 2,
    "title": "Build a Todo App",
    "description": "Build a simple todo app using Express and a frontend framework"
  },
  {
    "id": 3,
    "title": "Learn Express",
    "description": "Learn how to use Express.js to build web applications"
  }
]
```
2. 添加待办事项
请求方法：`POST`
请求路径：`/todos`
请求头：`Content-Type: application/json`
请求体：`JSON对象`，包含待办事项的详细信息。
示例请求体：
```json
{
  "title": "New Todo",
  "description": "This is a new todo item"
}
```
响应：
状态码：`201 Created`
响应体：JSON对象，包含新创建的待办事项的详细信息。
示例响应：
```json
{
  "id": 4,
  "title": "New Todo",
  "description": "This is a new todo item"
}
```
3. 删除待办事项
请求方法：`DELETE`
请求路径：`/todos/:id`
请求参数：
id：要删除的待办事项的ID。
响应：
状态码：`200 OK`
响应体：JSON对象，包含删除操作的消息。
示例响应：
```json
{
  "message": "Todo deleted successfully"
}
```

#### 扩展使用内存数据库或者数据库


## 规范
在构建优秀的Express项目时，采用良好的代码结构和组织方式至关重要
```bash
my-express-app/
|-- app.js
|-- package.json
|-- config/
|   |-- database.js
|   |-- middleware.js
|   |-- routes.js
|-- controllers/
|   |-- userController.js
|   |-- todoController.js
|-- models/
|   |-- userModel.js
|   |-- todoModel.js
|-- routes/
|   |-- userRoutes.js
|   |-- todoRoutes.js
|-- services/
|   |-- userService.js
|   |-- todoService.js
|-- utils/
|   |-- auth.js
|   |-- logger.js
|-- middleware/
|   |-- authMiddleware.js
|   |-- errorHandler.js
|-- public/
|   |-- css/
|   |-- js/
|   |-- images/
|-- views/
    |-- index.ejs
    |-- user.ejs
    |-- todo.ejs
```    
以下是对这个结构的简要说明：

app.js：项目的入口文件，用于设置Express应用程序、数据库连接、中间件和路由。

package.json：项目的依赖和元数据文件。

config/：存放项目配置文件的目录，例如数据库连接、中间件和路由配置。

controllers/：存放控制器文件的目录，用于处理HTTP请求并与模型和服务交互。

models/：存放数据模型文件的目录，用于定义数据结构和与数据库交互的方法。

routes/：存放路由文件的目录，用于定义应用程序的路由和端点。

services/：存放服务文件的目录，用于封装与模型交互的业务逻辑。

utils/：存放实用工具文件的目录，例如身份验证、日志记录等。

middleware/：存放自定义中间件文件的目录，用于处理请求和响应。

public/：存放静态资源文件的目录，例如CSS、JavaScript和图像文件。

views/：存放视图模板文件的目录，用于渲染HTML页面。

## 部署

处理跨域请求
1. 安装中间件:`npm install --save cors`
2. 配置
```javascript
var cors= require('cors');
var app= expresss();
app.use(cors({
  origin : [''],
  method : ['GET','POST','PATCH'] ,
  allowHeaders:['Content-Type']
}));

```

## 中间件

1. 应用级中间件

使用 `app.use()` 和 `app.METHOD()` 函数将应用级中间件绑定到 app 对象 的实例
```js
app.use((req, res, next) => {
    console.log('Time:', Date.now())
    next()
  })
```
2. 路由级中间件

3. 错误处理中间件

4. 内置中间件

5. 第三方中间件


## 开发需求

### 跨域中间件设置
```js
const cors = require('cors');
app.use(cors());
```

### 编写引入中间件

```js
const registerUser = require('./register');
```
### json解析

```js
const bodyParser = require('body-parser');
app.use(bodyParser.json());
```


### 模块系统

Node.js默认使用`CommonJS`模块系统
require函数返回由SqlSelect模块导出的对象或值，并将其赋值给名为SqlSelect的常量。
确保`./src/SqlSelect`路径下的文件正确地导出了你想要使用的功能。例如SqlSelect是一个类
```javascript
// src/SqlSelect.js
class SqlSelect {
  // class implementation...
}
module.exports = SqlSelect;
```


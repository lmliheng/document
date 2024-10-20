1. 环境准备
确保你已经安装了Node.js和npm。然后，使用Create React App创建一个新的React项目：
```bash
npx create-react-app student-info-management
cd student-info-management
```
2. 后端服务 - 使用Express
在项目根目录外创建一个新的文件夹，例如server，并初始化一个Node.js项目：
```bash
npm init -y
npm install express cors body-parser
```
在server文件夹中创建index.js，编写基本的Express服务器代码：
```bash
// server/index.js
const express = require('express');
const cors = require('cors');
const bodyParser = require('body-parser');

const app = express();
app.use(cors());
app.use(bodyParser.json());

// 在这里定义你的API路由

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```
3. 数据库设置
在这个例子中，我们将使用一个内存数据库来存储学生信息。在实际项目中，你可能会使用MySQL或其他数据库。

安装lowdb作为内存数据库：
```bash
npm install lowdb
```
创建一个db.js文件来初始化数据库：
```bash
// server/db.js
const low = require('lowdb');
const Memory = require('lowdb/adapters/Memory');

const adapter = new Memory();
const db = low(adapter);

db.defaults({ students: [] }).write();

module.exports = db;
```
4. 前后端交互
在server/index.js中定义API路由来处理登录、信息录入和后台管理操作。这里我们只提供一个简单的示例，实际项目中你需要添加更多的逻辑和安全性措施。
```bash
// server/index.js
const db = require('./db');

// 登录API
app.post('/api/login', (req, res) => {
  // 在实际项目中，你需要验证用户名和密码
  res.json({ token: 'your-jwt-token' });
});

// 学生信息录入API
app.post('/api/students', (req, res) => {
  const student = req.body;
  db.get('students').push(student).write();
  res.json(student);
});

// 获取学生列表API
app.get('/api/students', (req, res) => {
  const students = db.get('students').value();
  res.json(students);
});

// 更新学生信息API
app.put('/api/students/:id', (req, res) => {
  const studentId = req.params.id;
  const updatedStudent = req.body;
  db.get('students').find({ id: studentId }).assign(updatedStudent).write();
  res.json(updatedStudent);
});

// 删除学生信息API
app.delete('/api/students/:id', (req, res) => {
  const studentId = req.params.id;
  db.get('students').remove({ id: studentId }).write();
  res.json({ message: 'Student deleted successfully' });
});
```
5. 功能实现
在React项目中，你需要创建组件来实现登录、信息录入和后台管理功能。这里我们只提供一个简化的示例，实际项目中你需要添加更多的逻辑和样式。

例如，创建一个简单的登录表单组件：
```bash
// src/LoginForm.js
import React, { useState } from 'react';

const LoginForm = () => {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');

  const handleSubmit = async (e) => {
    e.preventDefault();
    // 在这里发送请求到后端API进行登录
  };

  return (
    <form onSubmit={handleSubmit}>
     <input
        type="text"
        value={username}
        onChange={(e) => setUsername(e.target.value)}
        placeholder="Username"
      />
     <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        placeholder="Password"
      />
     <button type="submit">Login</button>
    </form>
  );
};

export default LoginForm;
```
在实际项目中，你需要创建更多的组件来实现信息录入和后台管理功能，并使用fetch或axios与后端API进行交互。

6. 路由和状态管理
使用React Router管理客户端路由，管理不同页面之间的导航。对于复杂的状态管理，可以考虑使用Redux或Context API。

7. 安全性
确保敏感操作使用HTTPS，对用户输入进行验证和清理，防止XSS和SQL注入攻击。使用JWT或其他机制处理用户身份验证和授权。

8. 测试与部署
对关键功能进行单元测试和集成测试，使用Jest和Enzyme或其他测试框架。选择云服务部署前后端应用，确保环境变量正确配置。
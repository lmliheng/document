### 重写express API后
修改全局 res 对象的情况。，这样的操作会改变全局的响应对象行为，可能会影响到应用程序中的其他部分，特别是如果其他部分依赖于默认的行为

```bash
Error [ERR_HTTP_HEADERS_SENT]: Cannot set headers after they are sent to the client
    at new NodeError (node:internal/errors:387:5)
    at ServerResponse.setHeader (node:_http_outgoing:644:11)
    at ServerResponse.header (C:\Users\李恒\Desktop\code\node\node_login\node_modules\express\lib\response.js:795:10)
    at ServerResponse.contentType (C:\Users\李恒\Desktop\code\node\node_login\node_modules\express\lib\response.js:625:15)
    at ServerResponse.app.response.sendStatus (C:\Users\李恒\Desktop\code\node\node_login\todolist.js:31:17)
    at C:\Users\李恒\Desktop\code\node\node_login\todolist.js:42:7
    at Layer.handle [as handle_request] (C:\Users\李恒\Desktop\code\node\node_login\node_modules\express\lib\router\layer.js:95:5)
    at next (C:\Users\李恒\Desktop\code\node\node_login\node_modules\express\lib\router\route.js:149:13)
    at Route.dispatch (C:\Users\李恒\Desktop\code\node\node_login\node_modules\express\lib\router\route.js:119:3)
    at Layer.handle [as handle_request] (C:\Users\李恒\Desktop\code\node\node_login\node_modules\express\lib\router\layer.js:95:5)
```

**解决:可以考虑创建一个中间件或自定义函数，这样可以保持代码的模块化和可维护性。**

例如，您可以创建一个名为 customSendStatus 的中间件或函数，如下所示：
```js
Javascript
function customSendStatus(statusCode, type = 'text/plain', message) {
  return function(req, res, next) {
    res.contentType(type)
      .status(statusCode)
      .send(message);
  }
}

// 使用中间件
app.use(customSendStatus(404, 'application/json', '{"error":"resource not found"}'));
```
在路由处理程序中使用这个功能
```js
Javascript
app.get('/myroute', function(req, res) {
  customSendStatus(404, 'application/json', '{"error":"resource not found"}')(req, res);
});
```


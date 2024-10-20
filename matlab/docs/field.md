## 回调函数中的数据类型

注意`username=app.TextArea.Value`中传递给username的数据类型是cell，而不是char。
所以需要先将cell转为char，username = char(app.TextArea.Value);
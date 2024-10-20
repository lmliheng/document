## 注意匹配
请求类型
请求头
数据

## 测试
测试GET
测试POST请求，您可以使用curl命令或者使用Postman
使用curl命令：

首先，确保您已经安装了curl。如果没有，请参考前面的回答以安装curl。
使用以下命令发送POST请求
```
curl -X POST -H "Content-Type: application/json" -d '{"name": "test_item", "price": 19.99, "is_offer": true}' http://localhost:8000/items/1
```
使用-X POST指定请求类型为POST，-H "Content-Type: application/json"设置请求头的Content-Type为application/json，-d选项用于指定请求体中的JSON数据。

Curl
```
curl -X 'PUT' \
'http://127.0.0.1:8000/items/1' \
-H 'accept: application/json' \
-H 'Content-Type: application/json' \
-d '{
"name": "string",
"price": 0,
"is_offer": true
}'
```
Request URL
```
http://127.0.0.1:8000/items/1
```
Server response
```
Response body
Download
{
"item_name": "string",
"item_id": 1
}
```
Response headers
```
content-length: 34
content-type: application/json
date: Fri,10 May 2024 03:16:30 GMT
server: uvicorn 
```


## http请求

在JavaScript中，进行前端请求主要可以使用`XMLHttpRequest`对象或者更现代的`fetch`API。下面我将分别展示如何使用这两种方法来发起GET和POST请求。

### 使用 XMLHttpRequest

**GET请求示例：**

```javascript
function sendGetRequest() {
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function () {
        if (xhr.readyState == 4 && xhr.status == 200) {
            console.log(xhr.responseText);
        }
    };
    xhr.open("GET", "https://api.example.com/data", true);
    xhr.send();
}
```
**POST请求示例：**
```javascript
function sendPostRequest() {
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function () {
        if (xhr.readyState == 4 && xhr.status == 200) {
            console.log(xhr.responseText);
        }
    };
    xhr.open("POST", "https://api.example.com/submit", true);
    xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8");
    var data = JSON.stringify({ key: "value" });
    xhr.send(data);
}
```
### 使用 Fetch API
**GET请求示例：**
```javascript
fetch("https://api.example.com/data")
    .then(response => {
        if (!response.ok) {
            throw new Error("Network response was not ok");
        }
        return response.text();
    })
    .then(data => console.log(data))
    .catch(error => console.error("There was a problem with the fetch operation:", error));
```
**POST请求示例：**

```javascript
fetch("https://api.example.com/submit", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({ key: "value" })
})
    .then(response => {
        if (!response.ok) {
            throw new Error("Network response was not ok");
        }
        return response.json(); // 或者 response.text() 根据响应类型调整
    })
    .then(data => console.log(data))
    .catch(error => console.error("There was a problem with the fetch operation:", error));
```

Fetch API相比XMLHttpRequest更简洁且支持Promise，使得异步操作更加易于理解和维护。
不过，需要注意的是，fetch是一个全局函数，而在一些较旧的浏览器中可能不被支持，因此在生产环境中可能需要引入polyfill来兼容。


## fetch
fetch()的功能与 XMLHttpRequest 基本相同，但有三个主要的差异。
（1）fetch()使用 Promise，不使用回调函数，因此大大简化了写法，写起来更简洁。
（2）fetch()采用模块化设计，API 分散在多个对象上（Response 对象、Request 对象、Headers 对象），更合理一些；相比之下，XMLHttpRequest 的 API 设计并不是很好，输入、输出、状态都在同一个接口管理，容易写出非常混乱的代码。
（3）fetch()通过数据流（Stream 对象）处理数据，可以分块读取，有利于提高网站性能表现，减少内存占用，对于请求大文件或者网速慢的场景相当有用。XMLHTTPRequest 对象不支持数据流，所有的数据必须放在缓存里，不支持分块读取，必须等待全部拿到后，再一次性吐出来。
在用法上，fetch()接受一个 URL 字符串作为参数时，默认向该网址发出 GET 请求，返回一个 Promise 对象。它的基本用法如下
fetch()的第一个参数是 URL，还可以接受第二个参数，作为配置对象，定制发出的 HTTP 请求。
fetch(url, optionObj)
上面命令的optionObj就是第二个参数,HTTP 请求的方法、标头、数据体都在这个对象里面
```
fetch(url)
.then(...)
.catch(...)
```
采用await的写法，也可使用.then()的写法
由于Fetch API是基于Promise的，因此需要使用async/await或.then()来处理异步操作
```javascript
fetch('https://api.github.com/users/lmliheng')
    //fetch()函数返回一个Promise，当请求成功时，这个Promise会解析为一个Response对象
    .then(response => response.json())
    //.then()方法接收一个回调函数，该函数将Response对象转换为JSON对象
    .then(json => console.log(json))
    .catch(err => console.log('Request Failed', err));
```

```javascript
// 使用Fetch API获取GitHub用户信息
async function fetchGitHubUserInfo(username) {
  try {
    const response = await fetch(`https://api.github.com/users/${username}`);

    // 检查响应状态
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    // 解析响应数据为JSON对象
    const userInfo = await response.json();
    return userInfo;
  } catch (error) {
    console.error('Error fetching GitHub user info:', error);
    return null;
  }
}

// 示例：获取用户 "lmliheng" 的信息
fetchGitHubUserInfo('lmliheng')
  .then((userInfo) => {
    if (userInfo) {
      console.log('User info:', userInfo);
      console.log('用户名:',userInfo.name)
    } else {
      console.log('Failed to fetch user info.');
    }
  });    

```


### node快速创建接口
json-server 是一个基于 Node.js 的轻量级服务器，它允许您快速地搭建一个基于 JSON 文件的 RESTful API

以下是如何使用 json-server 的简要步骤：

安装 json-server：
使用 npm 安装 json-server：
npm install -g json-server
这将在全局范围内安装 json-server。
创建 JSON 文件：
创建一个名为 db.json 的文件，其中包含您的数据。例如：
{
"users": [
{
"id": 1,
"name": "John Doe",
"email": "john.doe@example.com"
},
{
"id": 2,
"name": "Jane Doe",
"email": "jane.doe@example.com"
}
],
"posts": [
{
"id": 1,
"title": "Hello, World!",
"content": "This is my first post.",
"userId": 1
}
]
}
在这个示例中，我们定义了两个资源：users 和 posts。
启动 json-server：
在命令行中，导航到包含 db.json 文件的目录，然后运行以下命令：
json-server --watch db.json
--watch 选项表示当 db.json 文件发生更改时，服务器将自动重新加载数据。 默认情况下，json-server 将在端口 3000 上启动。您可以通过访问 http://localhost:3000 来查看 API 的基本信息。
使用 API：
现在，您可以使用 HTTP 请求与 json-server 进行交互。例如，要获取所有用户，您可以发送 GET 请求到 http://localhost:3000/users。要获取具有特定 ID 的用户，您可以发送 GET 请求到 http://localhost:3000/users/1（将 1 替换为所需的 ID）。 json-server 还支持其他 HTTP 方法，如 POST、PUT、PATCH 和 DELETE。您可以使用这些方法来创建、更新和删除资源。
通过以上步骤，您可以使用 json-server 快速搭建一个简单的 RESTful API，以便在前端开发过程中进行测试和学习
增(POST)
curl "http://127.0.0.1:3000/data" -H "Content-Type: application/json" -d "{\"name\":\"zhangsan\"}" -X POST
-H表示增加请求头
-d后面是数据
-X POST表示用POST请求
返回值如下

{
"name": "zhangsan",
"id": 2
}
再看一下我们刚才创建的db.json文件，里面多了我们刚才POST的数据。实际上就是存在了这个文件里面。

改(PATCH)
注意改的时候url后面跟上id

curl "http://127.0.0.1:3000/data/2"  -H "Content-Type: application/json" -d "{\"name\":\"lisi\"}"  -X PATCH
返回如下

{
"name": "lisi",
"id": 2
}
说明修改成功

查(GET)
curl "http://127.0.0.1:3000/data"  -X GET
直接查全部

[
{
"name": "lisi",
"id": 2
}
]
删(DELETE)
删除id为2的数据

curl "http://127.0.0.1:3000/data/2" -X DELETE
返回如下

{}
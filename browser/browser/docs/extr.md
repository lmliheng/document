## 快捷键
1. ctrl+s（双击s）本地获取页面html代码
2. f12开发者模式
3. f11全屏
4. ctrl+p打印当前html也可转换为PDF下载到本地
5. tab+alt切换至其他页面（略）


## 同源策略

浏览器采用了 SOP（同源策略），它规定了浏览器中所有的服务请求必须要满足三个条件： 同域名，同协议，同端口


#### 跨域
跨域CORS（跨源资源共享） 的问题，想要解决它非常简单：
在前端：可以写入 devServer 的 proxy 代理（或者通过 nginx 代理）
在后端：可以通过 cors 添加响应头
```shell
from origin 'http://localhost:3000'has been blocked by CORSpolicy:
No 'Access-Control-Allow-Origin' header is present on the requestedresource. 
If an opaque response serves, your needs, ,set the requestss modeto 'no-cors' to fetch the resource with CORS disabted
```
当 sunday.com 的 Web 应用尝试从 admin.com 请求资源时，浏览器会自动在请求中包含 Origin 标头，指示请求源自何处 (sunday.com)。 此时：admin.com 的服务器不会根据 SOP 彻底阻止此类跨源请求，而是可以检查此 Origin 标头，并根据自己的 CORS 策略决定是否允许或拒绝该请求。
如果 admin.com 认为 sunday.com 值得信赖，或者所请求的资源可以公开访问，则它可以使用特定的CORS标头进行响应，
例如Access-Control-Allow-Origin，指示允许哪些源访问该资源。
此标头可能设置为 http://example.com，明确允许此源，或 * 表示任何源都可以访问的公共资源。
这也是常见的后端处理跨域的方式。
但是此时，我们需要注意：如果请求没有 Origin 标头怎么办？
如果请求没有 Origin 标头，通常是因为请求是通过非浏览器发起的，或者是因为浏览器的同源策略禁止了对跨源请求的 Origin 标头的发送（例如发送给 file:// 或 data:// URI）。在这种情况下，浏览器不会发送 Origin 标头，并且 CORS 的处理会变得更加复杂，因为它不再是一个“简单的请求”。
这时可能需要使用 CORS 中的预检请求来进行处理，以确定是否允许实际的请求。
#### 预检请求
当浏览器在发送某些类型的可能修改服务器上数据的请求（如 PUT、DELETE 方法），或者发送包含不会自动包含在每个请求中的标头的请求时，会先发送一个预检请求，即 OPTIONS 请求。
预检请求的目的是向服务器检查实际请求是否可以安全发送。预检请求会包括描述 HTTP 方法的标头和实际请求的标头。
服务器在收到预检请求后，如果支持 CORS 策略并且允许实际请求，会使用特定的 CORS 标头（如 Access-Control-Allow-Methods 和 Access-Control-Allow-Headers）来响应预检请求，指示允许哪些方法和标头。
浏览器根据服务器对预检请求的响应来决定是否继续处理实际请求。如果服务器的响应表明该请求被允许，则浏览器会发送实际请求；否则，浏览器将阻止该请求，并显示与 CORS 相关的错误。


### chrome浏览器设置允许跨域

[参考文章](https://haorooms.com/post/chrome_cros_yx)

设置跨域，在chrome快捷方式右键‘属性’，‘快捷方式’，‘目标’ 路径最后边`按一下空格`，再添加以下代码：
```bash
--args --disable-web-security --user-data-dir=D:\HaoroomsChromeUserData
```
设置成功以后再打开浏览器，会有提示：`“您使用的是不受支持的命令行标记： --disable-web-security，稳定性和安全性会有所下降”`

等于是用户在自己电脑创建了一套chrome的私有化浏览器，里边的设置配置等均为私有化设置

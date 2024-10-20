## 获取公网IP
个人物理服务器获取公网IP地址通常有以下几个方法：

1. **通过操作系统命令查询**：
   - **对于Linux服务器**，可以在终端中运行以下命令：
     ```
     curl ifconfig.me
     ```
     或者
     ```
     wget -qO- ifconfig.co
     ```
     还可以使用 `hostname -I` 或 `ip addr show` 查看所有网络接口的IP地址，其中可能包含公网IP。

 
2. **访问特定网站查询**：
   直接在服务器的浏览器中访问如 `http://ifconfig.me/`、`https://whatismyipaddress.com/` 或 `https://checkip.amazonaws.com/` 等网站，它们会显示服务器的公网IP地址。

3. **路由器管理界面查询**：
   如果服务器直接连接到互联网且背后没有复杂的网络结构，可以通过登录路由器管理界面查看WAN口的IP地址，这个通常是公网IP地址。

4. **联系ISP（互联网服务提供商）**：
   如果上述方法无法获取公网IP，或者你确定需要一个固定的公网IP，可能需要联系你的ISP。对于个人用户，有的ISP可能提供动态公网IP服务，也可能需要额外付费申请静态公网IP地址，具体政策依据ISP而定。

5. **使用DDNS服务**：
   如果你的服务器位于NAT后面或使用的是动态公网IP，可以考虑使用DDNS（Dynamic DNS）服务。DDNS服务能将你的动态公网IP地址映射到一个固定的域名上，便于远程访问。

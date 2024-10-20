### Github
[仓库](https://github.com/lmliheng/he-web)


### 结构
```bash
├───web服务器_updata/
│   ├───makefile
│   ├───conf/
│   │   ├───main.conf
│   ├───includes/
│   │   ├───config.h
│   │   ├───request.h
│   │   ├───response.h
│   │   ├───server.h
│   ├───src/
│   │   ├───config.c
│   │   ├───main.c
│   │   ├───request.c
│   │   ├───response.c
│   │   ├───server.c
│   ├───static/
│   │   ├───index.html
```

### conf
#### main.conf
```conf
port = 8080
root_dir = root/static/index
```
### src
#### congig.c
```c
#include "config.h"

Config* parse_config(const char *config_file) {
    Config *config = (Config *)malloc(sizeof(Config));
    if (config == NULL) {
        printf("无法分配内存。\n");
        return NULL;
    }

    FILE *file = fopen(config_file, "r");
    if (file == NULL) {
        printf("无法打开配置文件。\n");
        free(config);
        return NULL;
    }

    char line[256];
    while (fgets(line, sizeof(line), file)) {
        char *key = strtok(line, "=");
        char *value = strtok(NULL, "\n");

        if (strcmp(key, "port") == 0) {
            config->port = atoi(value);
        } else if (strcmp(key, "root_dir") == 0) {
            strcpy(config->root_dir, value);
        }
    }

    fclose(file);
    return config;
}
```

#### main.c
```c
#include<stdio.h>
#include<string.h>
#include <stdlib.h>
#include <unistd.h>
#include <arpa/inet.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <fcntl.h>
#include "config.h"
#include "server.h"
#include "response.h"

// 定义main函数
int main() {
    // 定义配置文件路径
    const char *config_file = "conf/main.conf";

    // 解析配置文件
    Config *config = parse_config(config_file);
    if (config == NULL) {
        printf("无法解析配置文件。\n");
        return 1;
    }

    start_server(config->port,config->root_dir);
    return 0;


}
/*
    // 创建服务器套接字
    int server_socket = create_server_socket(config->port);
    if (server_socket == -1) {
        printf("无法创建服务器套接字。\n");
        free(config);
        return 1;
    }

    // 输出服务器正在监听的端口
    printf("Web服务器正在监听端口 %d...\n", config->port);

    // 使用while循环来接受客户端连接
    while (1) {
        int client_socket = accept_client_connection(server_socket);
        if (client_socket == -1) {
            printf("无法接受客户端连接。\n");
            continue;
        }

        // 处理客户端请求
        handle_request(client_socket, config->root_dir);

        // 关闭客户端套接字
        close(client_socket);
    }

    // 关闭服务器套接字并释放配置内存
    close(server_socket);
    free(config);
    return 0;
}
*/

/*
#include "server.h"

int main() {
    
    int port = 7890; // 监听端口
    start_server(port);
    return 0;
}
*/


/*
web_server/
|-- src/
|   |-- main.c       // 主函数入口
|   |-- server.c     // 服务器核心逻辑
|   |-- request.c    // 请求处理逻辑
|   |-- response.c   // 响应生成逻辑
|-- includes/
|   |-- server.h     // 服务器相关函数声明
|   |-- request.h    // 请求处理函数声明
|   |-- response.h   // 响应生成函数声明
|-- static/
|   |-- index.html   // 默认返回的HTML页面
|-- Makefile         // 编译规则

*/

//编译：gcc -Wall -g -o web_server src/main.c src/server.c src/request.c src/response.c -Iincludes
```

#### request.c
```c

/*#include "request.h"
#include "response.h"
#include "server.h"

void handle_request(int client_socket, const char *root_dir) {
    send_response(client_socket, root_dir);
}
*/

#include<stdio.h>
#include<string.h>
#include <unistd.h>
#include <sys/socket.h>
#include "response.h"
#include "config.h"

void handle_request(int client_socket) {

        // 定义配置文件路径
    const char *config_file = "conf/main.conf";

    // 解析配置文件
    Config *config = parse_config(config_file);


    char buffer[1024] = {0};
    ssize_t bytes_read = recv(client_socket, buffer, sizeof(buffer) - 1, 0);
    
    if (bytes_read > 0) {
        // 这里可以添加解析HTTP请求的逻辑，但为了简洁，我们直接发送响应
        
        send_response(client_socket,config->root_dir);
    }
}

```
#### response.c
```c
#include "response.h"
#include<stdio.h>
#include<string.h>
#include <stdlib.h>

void send_response(int client_socket, const char *root_dir) {
    char index_html_path[256];
    sprintf(index_html_path, "%s/index.html", root_dir);

    FILE *file = fopen(index_html_path, "r");
    if (file == NULL) {
        printf("无法打开文件以读取内容。\n");
        return;
    }

    char html_content[4096] = {0};
    size_t bytes_read = fread(html_content, sizeof(char), sizeof(html_content) - 1, file);
    if (bytes_read == 0) {
        printf("无法读取文件内容。\n");
        fclose(file);
        return;
    }

    html_content[bytes_read] = '\0';
    fclose(file);

    char header[512] = {0};
    sprintf(header, "HTTP/1.1 200 OK\r\nContent-Type: text/html\r\nContent-Length: %zu\r\n\r\n", strlen(html_content));

    send(client_socket, header, strlen(header), 0);
    send(client_socket, html_content, strlen(html_content), 0);
}

/*
#include<stdio.h>
#include<string.h>
#include <unistd.h>
#include <sys/socket.h>

void send_response(int client_socket) {
    const char* html_content = "<!DOCTYPE html><html><head<title>Hello from C Web Server</title></head><body><h1>Hello, World!</h1></body></html>";
    char header[512] = {0};

    // 构建HTTP响应头
    sprintf(header, "HTTP/1.1 200 OK\r\nContent-Type: text/html\r\nContent-Length: %zu\r\n\r\n", strlen(html_content));
    

    // 发送响应头和内容
    send(client_socket, header, strlen(header), 0);
    send(client_socket, html_content, strlen(html_content), 0);
}

// 在response.h中声明send_response函数
void send_response(int client_socket);
*/

```
#### server.c
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h> 
#include <sys/socket.h>
#include "request.h"
#include "response.h"

void start_server(int port,const char *root_dir ) {
    int server_fd, new_socket;
    struct sockaddr_in address;
    int opt = 1;
    int addrlen = sizeof(address);

    
    // 创建socket文件描述符
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        perror("socket failed");
        exit(EXIT_FAILURE);
    }

    
    // 设置socket选项，允许端口复用
    if (setsockopt(server_fd, SOL_SOCKET, SO_REUSEADDR | SO_REUSEPORT, &opt, sizeof(opt))) {
        perror("setsockopt");
        exit(EXIT_FAILURE);
    }
    
    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(port);
    

      // 绑定地址到socket
    if (bind(server_fd, (struct sockaddr *)&address, sizeof(address))<0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }
    
    // 开始监听，最大连接数为5
    if (listen(server_fd, 5) < 0) {
        perror("listen");
        exit(EXIT_FAILURE);
    }
    
    while(1) {
        // 接受新的连接请求
        if ((new_socket = accept(server_fd, (struct sockaddr *)&address, (socklen_t*)&addrlen))<0) {
            perror("accept");
            exit(EXIT_FAILURE);
        }

           // 处理客户端请求
        handle_request(new_socket);
        
        close(new_socket); // 关闭连接
    }
    
    shutdown(server_fd, SHUT_RDWR);
}
```

### includes
#### config.h
```h
#ifndef CONFIG_H
#define CONFIG_H

#include<stdio.h>
#include<stdlib.h>
#include<string.h>

typedef struct {
    int port;
    char root_dir[256];
} Config;

Config* parse_config(const char *config_file);

#endif // CONFIG_H
```
#### request.h
```h
#ifndef REQUEST_H
#define REQUEST_H

#include <unistd.h>
#include <sys/socket.h>

void handle_request(int client_socket);

#endif // REQUEST_H
```
#### response.h
```h
#ifndef RESPONSE_H
#define RESPONSE_H

#include <unistd.h>
#include <sys/socket.h>

void send_response(int client_socket, const char *root_dir);

#endif // RESPONSE_H
```
#### server.h
```h
#ifndef SERVER_H
#define SERVER_H

#include <unistd.h>
#include <sys/socket.h>

int create_server_socket(int port);
void start_server(int server_socket, const char *root_dir);

#endif // SERVER_H
```
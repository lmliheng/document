## 底层头文件
```c
#include<stdio.h>
#include<string.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<fcntl.h>
```

## 文件操作

类型检查


## 命令行参数
### 


## 函数链接
### 头文件写法
```c
//cmd_utils.h
#ifndef CMD_UTILS_H
#define CMD_UTILS_H
void show_command_usage(const char *command);

#endif // CMD_UTILS_H
```c
//cmd_utils.c
#include "../../includes/cmd_utils.h"
```
```c
//入口文件
#include "../includes/cmd_utils.h"
```

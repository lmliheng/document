### omnTools
在本项目中，我们使用C++和Windows API实现了一个命令行工具，用于在本地和远程执行一系列操作
### 功能
本地调用：通过命令行调用本项目的入口exe文件，执行特定命令。
远程文件安装：使用本项目特定命令从远程服务器下载并安装文件。
其他操作：根据需要，可以扩展本项目以支持更多操作。
### 构建和运行
环境要求：
操作系统：`Windows`
编译器：支持C++17的编译器，如`Visual Studio 2017`或更高版本
构建： 使用C++编译器编译项目源代码，生成可执行文件（exe）。
运行： 在命令行中，导航到可执行文件所在的目录，并使用以下命令运行程序：
```
your_executable.exe command [arguments]
```
其中your_executable.exe是你的项目可执行文件的名称，command是要执行的命令，arguments是命令的参数（如果有）。
示例
以下是一些使用本项目的示例：
本地调用：
```
your_executable.exe local_command
```
这将在本地执行名为local_command的命令。
远程文件安装：
```
your_executable.exe install https://example.com/remote_file.zip
```
这将从https://example.com/remote_file.zip下载文件并安装。
### 许可证
本项目采用`MIT`许可证。这意味着你可以自由地使用、修改和分发本项目的源代码，只要遵循许可证的条款和条件。
### 联系我们
如果你有任何问题或建议，请随时与我们联系。你可以通过以下方式与我们取得联系：
GitHub：https://github.com/limitless-0day
我们期待与你合作，共同推进本项目的发展。使用我们特定的命令。
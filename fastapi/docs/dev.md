## 开发
本地环境`windows11`，`python3.11`

生产环境`linux centos7`，`python3.6`
### 调试
#### 虚拟环境
本地创建
```
PS C:\Users\李恒\Desktop\code\Fast API> python -m venv myenv
PS C:\Users\李恒\Desktop\code\Fast API> myenv\Scripts\activate
```

FastAPI 依赖 Python 3.8 及更高版本。
安装 FastAPI 很简单，这里我们使用 pip 命令来安装。
```
pip install fastapi
pip install "uvicorn[standard]"
```
另外我们还需要一个 ASGI 服务器，生产环境可以使用 Uvicorn 或者 Hypercorn：
```
pip install "uvicorn[standard]"
```
启动
```
uvicorn main:app --reload
```
API 文档访问
```
http://127.0.0.1:8000/redoc
http://127.0.0.1:8000/docs
```




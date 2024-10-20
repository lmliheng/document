```python
from typing import Union

from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()


class Item(BaseModel):
    name: str
    price: float
    is_offer: Union[bool, None] = None


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, q: Union[str, None] = None):
    return {"item_id": item_id, "q": q}


@app.put("/items/{item_id}")
def update_item(item_id: int, item: Item):
    return {"item_name": item.name, "item_id": item_id}
```

Query查询校验

```python
from typing import Optional


from fastapi import FastAPI, Query

app = FastAPI()


@app.get("/items/")
async def read_items(q: Optional[str] = Query(None, max_length=50)):
    results = {"items": [{"item_id": "Foo"}, {"item_id": "Bar"}]}
    if q:
        results.update({"q": q})
    return results
```



FastAPI官方文档提供了一个很好的示例来展示如何连接到MySQL数据库并执行基本的CRUD（创建、读取、更新、删除）操作。
下面是一个基于FastAPI和SQLAlchemy连接MySQL数据库的基本示例，遵循官方文档的指导原则。
这个例子将展示如何设置数据库模型、创建依赖项来获取数据库会话，以及定义几个基本的路由来操作用户数据。
首先，确保你已安装所需的库，可以通过以下命令安装：
```bash
pip install fastapi uvicorn sqlalchemy pymysql
```
然后，你可以按照以下步骤设置你的FastAPI应用：

1. **定义数据库模型**：
   使用SQLAlchemy定义你的数据库模型。例如，创建一个`User`模型表示用户表。

```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
Base = declarative_base()
class User(Base):
    __tablename__ = "users"
    
    id = Column(Integer, primary_key=True, index=True)
    email = Column(String, unique=True, index=True)
    password = Column(String)
```

2. **数据库连接与配置**：
   设置数据库连接URL，并创建一个依赖项来管理数据库会话。

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import Session
from fastapi import Depends

DATABASE_URL = "mysql+pymysql://username:password@localhost/dbname"

engine = create_engine(DATABASE_URL)
Base.metadata.create_all(bind=engine)

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
```

这里，`DATABASE_URL`应替换为你实际的数据库连接信息。

3. **FastAPI应用实例与路由定义**：
   创建FastAPI应用实例，并定义路由来处理用户相关的HTTP请求。

```python
from fastapi import FastAPI, HTTPException
from . import models  # 导入上面定义的User模型

app = FastAPI()

@app.post("/users/", response_model=models.User)
def create_user(user: models.User, db: Session = Depends(get_db)):
    db_user = models.User(**user.dict())
    db.add(db_user)
    db.commit()
    db.refresh(db_user)
    return db_user

@app.get("/users/{user_id}", response_model=models.User)
def read_user(user_id: int, db: Session = Depends(get_db)):
    db_user = db.query(models.User).filter(models.User.id == user_id).first()
    if not db_user:
        raise HTTPException(status_code=404, detail="User not found")
    return db_user

# 类似的，你可以添加update_user和delete_user等路由
```

4. **运行应用**：
   使用Uvicorn运行你的FastAPI应用。

```bash
uvicorn main:app --reload
```

请根据你的具体需求调整上述代码，比如数据库连接信息、模型字段等。这个例子展示了如何使用FastAPI官方推荐的方式与MySQL数据库进行交互。记得在实际部署前，处理好敏感信息如数据库凭据，并确保遵循最佳安全实践。


- 导入包
```python
import uvicorn
from fastapi import FastAPI
from langchain_ollama import ChatOllama
from langserve import add_routes
```

- 1.初始化FastAPI应用
```python
app=FastAPI(title="Langserve 服务")
```

- 2.初始化本地ollama模型
```python
model=ChatOllama(model="qwen3:0.6b",base_url="http://localhost:11434")
```

- 3.使用LangServe将模型注册为路由路径 "/ollama"       【也就是把模型挂载到接口路径 /ollama】
```python
add_routes(app,model,path="/ollama")
```

- 4.启动服务
```python
uvicorn.run(app,host="localhost",port=8000)
```
- 5.启动之后的服务如下
<img width="735" height="293" alt="image" src="https://github.com/user-attachments/assets/eff481e9-c177-4aed-9c39-24c0e3a59a81" />

- 6.说明  
&nbsp;&nbsp;&nbsp;&nbsp;现在就是可以在别人的电脑上访问到自己的本地大模型了，在浏览器上输入：http://localhost:8000/ollama/playground/    就会显示一个可视化Web界面直接与之对话即可，此时可能需要把localhost 更换成 自己电脑的ip地址才可访问。

- 7.访问的样子
<img width="855" height="648" alt="image" src="https://github.com/user-attachments/assets/1c209f74-b2f3-4924-ae8a-512ec9946292" />

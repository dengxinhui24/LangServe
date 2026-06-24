'''python
#导入库
import uvicorn
from fastapi import FastAPI
from langchain_ollama import ChatOllama
from langserve import add_routes

# 1.初始化FastAPI应用
app=FastAPI(title="Langserve 服务")

# 2.初始化本地ollama模型
model=ChatOllama(model="qwen3:0.6b",base_url="http://localhost:11434")

# 3.使用LangServe将模型注册为路由路径 "/ollama"       【也就是把模型挂载到接口路径 /ollama】
add_routes(app,model,path="/ollama")

# 4.启动服务
uvicorn.run(app,host="localhost",port=8000)
'''

#效果

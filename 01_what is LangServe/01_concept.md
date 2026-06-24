# LangServe的基本概念
## 1.什么是LangServe
LangServe是LangChain官方推出的 应用发布工具 可以快速将本地运行的Chain、Agent、RAG链路封装为标准REST API服务，支持跨语言、跨平台调用，是 智能应用前后端分离、对外提供服务的核心组件。

## 2.LangServe能做什么
（1）自动暴露API端点：只需要几行代码，就可以把Langchain的链 或 Agent转化为HTTP接口。支持 invoke / batch / stream 多种调用方式。   
（2）内置测试界面：部署后自动生成交互式Playground页面和Swagger文档，直接在浏览器里就能调试API，不用额外写测试代码。  
（3）语言调用支持：提供 Python 和 JS客户端SDK ，前端或后端项目都能方便地调用已部署的服务。  
（4）流式输出能力：支持实时流式返回AI模型输出，适合聊天机器人等需要逐字显示的场景。  

## 3.需要做什么
在部署前需要安装LangServe核心依赖包，包含服务运行所需的网络、接口解析组件，打开cmd 执行 pip install "langserve[all]" langchain fastapi uvicorn

## 4.运行原理
LangServe 基于 FastAPI 搭建 Web 服务，Uvicorn 作为 ASGI 高性能服务网关，将 LangChain 业务逻辑与 Web 服务解耦，同时内置交互式调试页面，方便开发者在线测试接口。

## 补充知识点
（1）调用方式   
&nbsp;&nbsp;&nbsp;&nbsp;invoke() 同步一次性输出 ： 简单说 就是等模型完整全部回答，全部结束后一次性返回完整字符串。   
&nbsp;&nbsp;&nbsp;&nbsp;stream()流式分段输出    ： 简单说 就是模型生成几个字就会返回一块，循环接受每一段增量文本，实现实时打印回答的效果。  
&nbsp;&nbsp;&nbsp;&nbsp;batch() 批量调用        ： 简单说 就是一次性一组多个输入，让LLM/Chain一次性批量处理，不用循环多次 invoke()。

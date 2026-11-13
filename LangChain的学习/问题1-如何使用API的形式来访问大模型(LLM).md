1.使用openai原生的api来访问大模型
1.1 使用【硬编码】的方式
特点: base_url | api_key都写死在代码中
```java
"""
    硬编码的方式  写相关的配置
    http://models.ascend.localhost.com/v1
    sk-xkhTeVq1B86LmsYCISNUXgCu76yeGZsCvh6NS2pKuxKd6bsm
"""
import os
from openai import OpenAI

# 配置代理忽略（如未在系统环境变量设置）
os.environ["NO_PROXY"] = "localhost"

client = OpenAI(
    base_url="http://models.ascend.localhost.com/v1",
    api_key="sk-xkhTeVq1B86LmsYCISNUXgCu76yeGZsCvh6NS2pKuxKd6bsm"
)

response = client.chat.completions.create(
    model="glm-5.3-flash",
    messages=[{"role": "user", "content": "你好"}]
)

print(response.choices[0].message.content)
```
1.2 使用environment环境变量的方式
特点:从【环境变量】中去拿取 base_url | api_key
```java
"""
    使用环境变量的方式 来拿到配置
    使用环境变量调用大模型
"""
import os
from openai import OpenAI

# 配置代理忽略（如未在系统环境变量设置）
os.environ["NO_PROXY"] = "localhost"

client = OpenAI(
    base_url=os.environ["OPENAI_BASE_URL"],
    api_key=os.environ["OPENAI_API_KEY"]
)

response = client.chat.completions.create(
    model="glm-5.3-flash",
    messages=[{"role": "user", "content": "你好"}]
)

print(response.choices[0].message.content)
```

1.3 通过【配置文件】的方式
.env配置文件
```java
# 模型配置参数
MODEL_NAME=qwen3.8-27b
OPENAI_BASE_URL=http://models.ascend.localhost.com/v1
OPENAI_API_KEY=sk-xkhTeVq1B86LmsYCISNUXgCu76yeGZsCvh6NS2pKuxKd6bsm
```
```java
"""
    使用环境变量的方式 来拿到配置
    使用环境变量调用大模型
"""
import os
import dotenv
from openai import OpenAI



# 加载Env配置文件
dotenv.load_dotenv()

# 调试：打印当前获取到的变量值
print(f"DEBUG: OPENAI_BASE_URL = {os.getenv('OPENAI_BASE_URL')}")
print(f"DEBUG: OPENAI_API_KEY = {os.getenv('OPENAI_API_KEY')}")


# 配置代理忽略（如未在系统环境变量设置）
os.environ["NO_PROXY"] = "localhost"

client = OpenAI(
    base_url=os.getenv("OPENAI_BASE_URL"),
    api_key=os.getenv("OPENAI_API_KEY")
)

response = client.chat.completions.create(
    model="glm-5.3-flash",
    messages=[{"role": "user", "content": "你好"}],
    temperature=1 # 示例值，可根据需求调整
)

print(response.choices[0].message.content)
```



2.使用langChain的api访问大模型
2.1 通过【硬编码】的方式
```java

```
2.2 通过【配置文件】的方式
真实生产api_key | base_url使用原则:代码中不应出现具体的 URL 或 Key 字符串，而应通过标准库（如 os.getenv）或配置中心 SDK 动态获取
下面的 严禁将 .env 文件提交至代码仓库，建议在 .gitignore 中添加 .env。
```java
import os
from dotenv import load_dotenv
from langchain_openai import ChatOpenAI

# 加载 .env 文件中的环境变量
load_dotenv()

# 配置代理忽略（如未在系统环境变量设置）
os.environ["NO_PROXY"] = "localhost"

# 调用对话模型
chat_model = ChatOpenAI(
    model_name=os.getenv("MODEL_NAME"), # 从 .env 获取模型名称
    base_url=os.getenv("BASE_URL"),      # 从 .env 获取基础 URL
    api_key=os.getenv("API_KEY"),         # 从 .env 获取 API 密钥
    request_timeout=60.0                  # 增加超时时间至 60 秒
)

# 调用模型
response = chat_model.invoke("你是谁?")

# 查看响应的结果
print(response)

```






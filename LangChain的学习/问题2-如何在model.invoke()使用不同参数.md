探究response = chat_model.invoke("你是谁?")支持哪些入参
本质
```java
LanguageModelInput = PromptValue | str | Sequence[MessageLikeRepresentation]
```
入参是字符串
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

入参是:Sequence[MessageLikeRepresentation]
```java
import os
import json
from dotenv import load_dotenv
from langchain_core.messages import HumanMessage, SystemMessage
from langchain_openai import ChatOpenAI

# 加载 .env 文件中的环境变量
load_dotenv()

# 配置代理忽略（如未在系统环境变量设置）
os.environ["NO_PROXY"] = ".huawei.com,.localhost"

# 调用对话模型
chat_model = ChatOpenAI(
    model_name=os.getenv("MODEL_NAME"),  # 从 .env 获取模型名称
    base_url=os.getenv("BASE_URL"),  # 从 .env 获取基础 URL
    api_key=os.getenv("API_KEY"),  # 从 .env 获取 API 密钥
    request_timeout=60.0  # 增加超时时间至 60 秒
)

# 准备对话历史记录
messages = [
    SystemMessage(content="你是一个专业的AI助手。"),
    HumanMessage(content="你好，我想了解一下人工智能的最新发展。"),
]

# 调用模型
response = chat_model.invoke(messages)

# 查看响应的结果
response_json = response.json()

# 输出JSON格式的响应
print(json.dumps(response_json, ensure_ascii=False, indent=2))

```
最终输出的结构化结果
```java
{
  "content": "你好！很高兴为你介绍人工智能领域的发展。以下是一些主要的进展方向：\n\n## 1. 大语言模型持续突破\n- **推理能力增强**：新一代模型（如 OpenAI 的 o1/o3 系列、DeepSeek-R1 等）通过“思维链”推理，在数学、编程和科学问题上表现大幅提升\n- **开源生态繁荣**：Llama、Qwen（通义千问）、DeepSeek、Mistral 等开源模型性能不断逼近闭源模型，降低了应用门槛\n\n## 2. 多模态能力\n- 模型不再局限于文本，可以理解图像、音频、视频\n- 视频生成技术快速发展（如 Sora、可灵 Kling 等），能生成高质量的视频内容\n- 实时语音对话体验更加自然流畅\n\n## 3. AI 智能体（AI Agents）\n- AI 从“回答问题”向“完成任务”演进，能自主使用工具、浏览网页、编写代码\n- Computer Use（操作电脑界面）等能力让 AI 可以代替人类执行复杂操作流程\n\n## 4. AI 在科学领域的应用\n- **AlphaFold** 因蛋白质结构预测获得诺贝尔化学奖\n- AI 辅助药物研发、新材料发现、气象预测等\n- 数学定理证明和科研论文辅助写作\n\n## 5. 硬件与算力\n- GPU 需求激增，NVIDIA 成为核心受益者\n- 各大公司投入自研芯片，推理成本快速下降\n\n## 6. 监管与伦理\n- 欧盟《人工智能法案》正式生效\n- 深度伪造、版权、就业影响等议题受到广泛关注\n\n---\n\n需要说明的是，我的知识有截止日期，可能无法涵盖最近几个月的最新动态。\n\n你对哪个方向比较感兴趣？我可以深入展开讲讲，比如大模型原理、AI 应用场景、或者行业趋势等。",
  "type": "ai",
  "id": "lc_run--01a1ce7e-b7f7-745c-a8fb-06528e9079e8-0",
  "response_metadata": {
    "model_provider": "openai",
    "model_name": "glm5.3-flash",
    "id": "chatcmpl-80f47cee97620946",
    "finish_reason": "stop",
    "token_usage": {
      "prompt_tokens": 27,
      "completion_tokens": 737,
      "total_tokens": 764
    }
  },
  "usage_metadata": {
    "input_tokens": 27,
    "output_tokens": 737,
    "total_tokens": 764
  },
  "tool_calls": [],
  "invalid_tool_calls": []
}

```
入参是PromptValue(提示词模板)
```java
import os
import json
from dotenv import load_dotenv
from langchain_core.messages import HumanMessage, SystemMessage
from langchain_core.prompt_values import PromptValue
from langchain_core.prompts import ChatPromptTemplate
from langchain_openai import ChatOpenAI

# 加载 .env 文件中的环境变量
load_dotenv()

# 配置代理忽略（如未在系统环境变量设置）
os.environ["NO_PROXY"] = ".huawei.com,.localhost"

# 调用对话模型
chat_model = ChatOpenAI(
    model_name=os.getenv("MODEL_NAME"),  # 从 .env 获取模型名称
    base_url=os.getenv("BASE_URL"),  # 从 .env 获取基础 URL
    api_key=os.getenv("API_KEY"),  # 从 .env 获取 API 密钥
    request_timeout=60.0  # 增加超时时间至 60 秒
)

# 准备对话历史记录
# 2. 定义提示词模板
prompt_template = ChatPromptTemplate.from_template(
    "请介绍一下 {topic} 的最新发展。"
)

# 3. 生成 PromptValue 对象
# format方法会返回一个 PromptValue 实例
prompt_value: PromptValue = prompt_template.format(topic="人工智能")

# 调用模型
response = chat_model.invoke(prompt_value)

# 查看响应的结果
response_json = response.model_dump_json()
# 输出JSON格式的响应
print(json.dumps(response_json, ensure_ascii=False, indent=2))

```






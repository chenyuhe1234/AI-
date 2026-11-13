什么是提示词模板

几种场景的提示词模板
PromptTemplate：LLM提示模板，用于生成字符串提示。它使用Python的字符串来模板提示。

ChatPromptTemplate：聊天提示模板，用于组合各种角色的消息模板，传入聊天模型。

XxxMessagePromptTemplate：消息模板词模板，包括：SystemMessagePromptTemplate、HumanMessagePromptTemplate、AIMessagePromptTemplate、ChatMessagePromptTemplate等

FewShotPromptTemplate：样本提示词模板，通过示例来教模型如何回答

PipelinePrompt：管道提示词模板，用于把几个提示词组合在一起使用。

自定义模板：允许基于其它模板类来定制自己的提示词模板。

目标
1、PromptTemplate如何获取实例
2、两种特殊结构的使用（部分提示词模板的使用、组合提示词的使用）
3、给变量赋值的两种方式：format() / invoke()
4、结合大模型的使用


1.使用构造方法 获取prompt Template实例

2.使用form_template(推荐)
```java
# 定义多变量模板
template = PromptTemplate.from_template(template="请详述{product}的优缺点，包括{aspect1}和{aspect2}。")

# 使用模板生成提示词
prompt_1 = template.format(product="智能手机", aspect1="电池续航", aspect2="拍照质量")

print(prompt_1)
```

什么是部分提示词模板
```java
from langchain.prompts import PromptTemplate

# 1. 定义包含多个变量的完整模板
# 假设模板包含：system_role, topic, style
full_template = PromptTemplate.from_template(
    "你是一个{system_role}。请写一篇关于{topic}的文章，风格要求是{style}。"
)

# 2. 使用 partial() 固定部分变量
# 这里固定了 system_role 为 "资深技术专家"
# 生成的 partial_template 只需要传入 topic 和 style
partial_template = full_template.partial(system_role="资深技术专家")

# 3. 使用部分模板生成最终提示词
# 只需传入剩余的变量：topic 和 style
final_prompt = partial_template.format(topic="人工智能", style="通俗易懂")

print(final_prompt)

```


invoke(): 传入的是字典，返回ChatPromptValue
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
os.environ["NO_PROXY"] = "localhost"

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


问题点:大模型(LLM)是没有记忆功能的
在多轮对话中 大模型不具备记忆功能
代码
```java
"""
   没有记忆功能
"""
import os
import json
from dotenv import load_dotenv
from langchain_core.messages import HumanMessage, SystemMessage
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

sys_message = SystemMessage(content="你是一个专业的AI助手 你的名字叫 小白");

human_message = HumanMessage(content="你好，我想了解一下人工智能的最新发展。")

# 准备对话历史记录
messages = [
    sys_message,
    human_message
]

# 调用模型
print("-------------------- 第一轮对话 ---------------------- ")
response = chat_model.invoke(messages)


response1=chat_model.invoke("你叫什么名字")

# 查看响应的结果
response_json = response.model_dump_json()

# 输出JSON格式的响应
print(json.dumps(response_json, ensure_ascii=False, indent=2))

print("-------------------- 第二轮对话 问题:你叫什么名字 ---------------------- ")
# content='我是GLM，由Z.ai开发的大语言模型。我被设计用来理解和生成人类语言，帮助回答问题、提供信息和进行对话交流。\n\n我的训练包含广泛的文本数据，让我能够处理多种话题和任务。有什么我能帮你解答或探讨的问题吗？' additional_kwargs={'refusal': None} response_metadata={'token_usage': {'completion_tokens': 236, 'prompt_tokens': 16, 'total_tokens': 252, 'completion_tokens_details': {'accepted_prediction_tokens': None, 'audio_tokens': 0, 'reasoning_tokens': 0, 'rejected_prediction_tokens': None, 'text_tokens': 0, 'image_tokens': 0}, 'prompt_tokens_details': {'audio_tokens': 0, 'cache_write_tokens': None, 'cached_tokens': 0, 'image_tokens': 0, 'text_tokens': 0}, 'usage_semantic': 'openai', 'usage_source': 'anthropic', 'billing_usage': {'source': 'claude_messages', 'semantic': 'anthropic', 'claude_usage': {'input_tokens': 16, 'cache_creation_input_tokens': 0, 'cache_read_input_tokens': 0, 'output_tokens': 236, 'claude_cache_creation_5_m_tokens': 0, 'claude_cache_creation_1_h_tokens': 0}}, 'input_tokens': 16, 'output_tokens': 0, 'input_tokens_details': None, 'claude_cache_creation_5_m_tokens': 0, 'claude_cache_creation_1_h_tokens': 0}, 'model_provider': 'openai', 'model_name': 'glm5.3-flash', 'system_fingerprint': None, 'id': 'chatcmpl-b77d2b09b2741f1f', 'finish_reason': 'stop', 'logprobs': None} id='lc_run--01a1ce9e-1067-75c4-a227-8e5bb7dbe8dd-0' tool_calls=[] invalid_tool_calls=[] usage_metadata={'input_tokens': 16, 'output_tokens': 236, 'total_tokens': 252, 'input_token_details': {'audio': 0, 'cache_read': 0}, 'output_token_details': {'audio': 0, 'reasoning': 0}}
print(response1)

```
输出结果
从第二轮的对话输出结果 可以看出 没有记忆功能
```java

-------------------- 第一轮对话 ---------------------- 
"{\"content\":\"\\n\\n你好！我是小白。可以，我帮你梳理一下人工智能最近比较重要的几个发展方向。整体来看，AI 正在从“会聊天、会生成内容”走向“会推理、会操作、会协作、会进入真实世界”。\\n\\n下面按几个关键方向讲：\\n\\n---\\n\\n## 1. 大语言模型：从“生成”走向“深度推理”\\n\\n以前的大模型主要擅长：\\n\\n- 回答问题\\n- 写文章\\n- 写代码\\n- 翻译总结\\n- 多轮对话\\n\\n现在更明显的发展趋势是：**模型开始具备更强的推理能力**。\\n\\n也就是说，不只是“背知识”或“语言接龙”，而是能完成类似这样的任务：\\n\\n- 多步骤数学推理\\n- 逻辑分析\\n- 代码调试\\n- 科研假设推演\\n- 复杂任务规划\\n- 长时间上下文理解\\n\\n典型表现是：\\n\\n- **推理型模型**更受关注，比如能进行“思考—反思—再回答”的模型。\\n- 模型处理长文档、长代码库、长视频、长对话的能力在增强。\\n- 多模态理解越来越强，不只是看文字，还能结合图像、表格、代码、语音等。\\n\\n简单说：  \\n**AI 正在从“能说会道”变成“能想清楚”。**\\n\\n---\\n\\n## 2. 多模态 AI：文字、图像、语音、视频全面融合\\n\\n现在 AI 不再只是处理文字，而是可以同时处理多种信息形式。\\n\\n比如一个模型可以：\\n\\n- 看图片并解释内容\\n- 读图表并给出分析\\n- 听语音并转写、总结\\n- 生成图像或视频\\n- 理解视频内容\\n- 根据截图完成操作\\n- 结合文档、网页、代码一起分析\\n\\n典型应用包括：\\n\\n- 图片问答\\n- 文档理解\\n- 视频摘要\\n- 智能客服\\n- 教育辅导\\n- 医疗影像辅助\\n- 代码与界面理解\\n- 自动生成 PPT、报告、视频脚本\\n\\n未来趋势是：  \\n**AI 会越来越多地像人一样“看、听、说、读、写、做”。**\\n\\n---\\n\\n## 3. AI Agent：从“工具”变成“能干活的助手”\\n\\n这是最近非常热门的方向。\\n\\n传统 AI 是：\\n\\n> 你问，它答。\\n\\nAI Agent 是：\\n\\n> 你给目标，它自己规划、执行、调用工具、检查结果，最后完成任务。\\n\\n例如你可以说：\\n\\n> “帮我调研一下某行业最近三个月的新闻，整理成一份报告，并生成 PPT。”\\n\\n一个 Agent 可能会自动完成：\\n\\n1. 理解任务目标  \\n2. 制定步骤  \\n3. 搜索网页  \\n4. 阅读资料  \\n5. 提取关键信息  \\n6. 总结成文档  \\n7. 制作表格或 PPT  \\n8. 检查错误并修正  \\n9. 返回结果\\n\\nAgent 的关键能力包括：\\n\\n- 任务规划\\n- 工具调用\\n- 浏览器操作\\n- 代码执行\\n- 文件读写\\n- API 调用\\n- 多轮自我修正\\n- 多 Agent 协作\\n\\n未来很多软件界面可能会从“点按钮”变成“直接说需求”。\\n\\n---\\n\\n## 4. 具身智能和机器人：AI 进入物理世界\\n\\n除了数字世界，AI 也开始进入真实物理世界，这通常叫 **具身智能** 或 **Embodied AI**。\\n\\n简单说，就是给机器人、机械臂、自动驾驶汽车、无人机等配上 AI 大脑。\\n\\n方向包括：\\n\\n- 人形机器人\\n- 工业机器人\\n- 自动驾驶\\n- 物流分拣机器人\\n- 家庭服务机器人\\n- 农业机器人\\n- 医疗手术辅助\\n\\n难点在于：\\n\\n- 感知环境\\n- 理解物理世界\\n- 稳定操作物体\\n- 安全控制\\n- 泛化能力\\n- 实时决策\\n\\n现在的趋势是：  \\n**大模型正在和机器人结合，让机器人不只是按固定程序走，而是能更灵活地理解任务和场景。**\\n\\n---\\n\\n## 5. AI 编程：从“辅助写代码”到“自动开发”\\n\\nAI 对软件开发的影响非常直接。\\n\\n过去 AI 编程工具主要帮人：\\n\\n- 补全代码\\n- 解释代码\\n- 写函数\\n- 找 bug\\n- 写测试\\n\\n现在正在往更高级的方向发展：\\n\\n- 根据需求生成完整项目\\n- 自动修改多文件代码\\n- 阅读整个代码库\\n- 自动调试和运行\\n- 生成前端界面\\n- 自动部署\\n- 生成测试用例\\n- 做代码审查\\n\\n这对开发者影响很大。未来工程师可能更像：\\n\\n> “定义问题 + 审核 AI 输出 + 做系统架构决策”\\n\\n而不是单纯手写每一行代码。\\n\\n---\\n\\n## 6. AI 科学发现：开始参与科研\\n\\nAI 不只是做内容生成，也开始参与科学研究。\\n\\n比较典型的应用有：\\n\\n- 蛋白质结构预测\\n- 新药研发\\n- 材料科学\\n- 气象预测\\n- 物理模拟\\n- 基因组分析\\n- 数学证明辅助\\n- 化学合成路径预测\\n- 天文数据分析\\n\\n比如 AI 可以在海量数据中发现规律，提出假设，辅助实验设计。\\n\\n未来 AI 可能会成为很多科学家、工程师、研究员的“数字助手”，甚至参与提出新理论或新实验方案。\\n\\n---\\n\\n## 7. 算力、芯片和基础设施竞争\\n\\nAI 发展离不开算力和芯片。\\n\\n核心包括：\\n\\n- GPU / NPU / 加速器\\n- 数据中心\\n- 高带宽内存\\n- 网络通信\\n- 液冷散热\\n- 电力供应\\n- 模型训练平台\\n- 推理优化\\n- 分布式计算\\n\\n现在竞争不只是“谁模型强”，还包括：\\n\\n- 谁的训练成本更低\\n- 谁的推理速度更快\\n- 谁的芯片更适合 AI\\n- 谁能大规模部署\\n- 谁的数据和工程体系更强\\n\\n简单说：  \\n**AI 竞争已经从单点技术变成系统性竞争。**\\n\\n---\\n\\n## 8. 开源模型和生态：越来越重要\\n\\n开源模型是最近几年的重要趋势。\\n\\n开源带来的好处：\\n\\n- 研究者更容易复现和修改\\n- 企业可以私有部署\\n- 开发成本降低\\n- 生态更繁荣\\n- 小公司也能参与创新\\n- 模型安全更容易被社区检查\\n\\n目前很多开源模型在能力上已经接近部分闭源模型，而且在垂直领域、私有化部署、本地运行等方面有明显优势。\\n\\n未来可能会形成：\\n\\n- 顶级闭源模型负责复杂任务\\n- 开源模型负责本地、私有、低成本场景\\n- 小模型负责端侧设备\\n- 多模型协作完成复杂任务\\n\\n---\\n\\n## 9. AI 安全、对齐和治理越来越重要\\n\\n随着 AI 能力增强，安全和治理问题也越来越突出。\\n\\n主要关注点包括：\\n\\n### 1. 对齐问题\\n如何确保 AI 的目标与人类价值观一致？\\n\\n### 2. 幻觉问题\\nAI 有时会生成看似合理但错误的内容。\\n\\n### 3. 隐私问题\\n训练数据、用户数据、企业数据如何保护？\\n\\n### 4. 安全攻击\\n比如提示注入、数据泄露、恶意利用等。\\n\\n### 5. 版权和责任\\nAI 生成内容归谁？出错后谁负责？\\n\\n### 6. 社会影响\\n就业、教育、媒体、金融等领域都会被改变。\\n\\n所以未来 AI 不只是技术问题，也是法律、伦理、社会治理问题。\\n\\n---\\n\\n## 10. 端侧 AI：AI 从云端走向手机、电脑和设备\\n\\n现在不只是大服务器里跑 AI，越来越多 AI 能力会部署到本地设备上。\\n\\n比如：\\n\\n- 手机实时翻译\\n- 本地语音助手\\n- 电脑端 AI 写作\\n- 摄像头智能分析\\n- 汽车本地推理\\n- 智能家居\\n- 可穿戴设备\\n- 工业设备边缘计算\\n\\n端侧 AI 的优势是：\\n\\n- 速度更快\\n- 延迟更低\\n- 隐私更好\\n- 不依赖网络\\n- 成本可能更低\\n\\n未来会出现：  \\n**云端大模型 + 本地小模型 + 设备端推理** 的混合架构。\\n\\n---\\n\\n# 如果你想快速了解，可以关注这些关键词\\n\\n你可以用这些关键词去搜索最新新闻：\\n\\n1. **Reasoning LLM**  \\n   推理型大模型\\n\\n2. **Multimodal AI**  \\n   多模态 AI\\n\\n3. **AI Agent**  \\n   智能体\\n\\n4. **Embodied AI / Humanoid Robot**  \\n   具身智能 / 人形机器人\\n\\n5. **Open-source LLM**  \\n   开源大模型\\n\\n6. **AI Coding**  \\n   AI 编程\\n\\n7. **Edge AI / On-device AI**  \\n   端侧 AI\\n\\n8. **AI Safety / AI Alignment**  \\n   AI 安全 / 对齐\\n\\n9. **AI for Science**  \\n   AI for Science / AI 科研\\n\\n10. **AI Chip / AI Infrastructure**  \\n   AI 芯片 / AI 基础设施\\n\\n---\\n\\n# 如果你刚开始入门，我建议这样了解\\n\\n## 入门路线\\n\\n### 第一步：理解基本概念\\n先搞清楚：\\n\\n- 机器学习\\n- 深度学习\\n- 神经网络\\n- 大语言模型\\n- 多模态\\n- Token\\n- 上下文窗口\\n- 推理成本\\n\\n### 第二步：体验实际产品\\n可以用：\\n\\n- 聊天助手\\n- AI 编程工具\\n- AI 搜索\\n- 图像生成\\n- 视频理解\\n- 文档分析工具\\n\\n先感受它能做什么，不能做什么。\\n\\n### 第三步：选择一个方向深入\\n比如：\\n\\n- 想创业：关注 Agent、AI 应用、垂直行业\\n- 想做研究：关注模型架构、推理、多模态、AI 安全\\n- 想做工程：关注模型部署、RAG、Agent、MLOps\\n- 想做内容：关注多模态生成、视频、图像\\n- 想做机器人：关注具身智能、SLAM、强化学习、控制\\n\\n### 第四步：动手实践\\n不要只看概念，最好做一点小项目：\\n\\n- 用 API 做一个问答机器人\\n- 做一个文档总结工具\\n- 做一个 AI 邮件助手\\n- 做一个代码解释器\\n- 做一个网页爬虫 + 报告生成工具\\n- 做一个简单 Agent\\n\\n---\\n\\n# 简单总结\\n\\n现在人工智能的发展主要有几个关键词：\\n\\n> **更强推理、多模态、智能体、机器人、AI 编程、科研应用、端侧部署、开源生态、安全治理。**\\n\\n如果用一句话概括：\\n\\n> **AI 正在从“内容生成工具”演化为能理解、规划、调用工具、操作现实世界的通用智能系统。**\\n\\n如果你愿意，我也可以继续帮你做一个更具体的方向，比如：\\n\\n1. **最新 AI 技术趋势详解**  \\n2. **AI 能带来哪些行业机会**  \\n3. **普通人如何学习 AI**  \\n4. **AI Agent 是什么，怎么入门**  \\n5. **AI 会如何影响程序员、设计师、产品经理**  \\n6. **用通俗方式解释大模型原理**\",\"additional_kwargs\":{\"refusal\":null},\"response_metadata\":{\"token_usage\":{\"completion_tokens\":2516,\"prompt_tokens\":70,\"total_tokens\":2586,\"completion_tokens_details\":null,\"prompt_tokens_details\":null},\"model_provider\":\"openai\",\"model_name\":\"Qwen3.8-27B\",\"system_fingerprint\":\"vllm-0.26.0-tp2-e225f1fb\",\"id\":\"chatcmpl-a7b68824d1ae0da1\",\"finish_reason\":\"stop\",\"logprobs\":null},\"type\":\"ai\",\"name\":null,\"id\":\"lc_run--01a1d321-130d-7420-8481-b2e26ed2725c-0\",\"tool_calls\":[],\"invalid_tool_calls\":[],\"usage_metadata\":{\"input_tokens\":70,\"output_tokens\":2516,\"total_tokens\":2586,\"input_token_details\":{},\"output_token_details\":{}}}"
-------------------- 第二轮对话 问题:你叫什么名字 ---------------------- 
content='\n\n我叫通义千问，也可以叫我 Qwen。' additional_kwargs={'refusal': None} response_metadata={'token_usage': {'completion_tokens': 70, 'prompt_tokens': 55, 'total_tokens': 125, 'completion_tokens_details': None, 'prompt_tokens_details': None}, 'model_provider': 'openai', 'model_name': 'Qwen3.8-27B', 'system_fingerprint': 'vllm-0.26.0-tp2-e225f1fb', 'id': 'chatcmpl-a0f559784f004640', 'finish_reason': 'stop', 'logprobs': None} id='lc_run--01a1d321-a879-762e-97cb-9404e2347803-0' tool_calls=[] invalid_tool_calls=[] usage_metadata={'input_tokens': 55, 'output_tokens': 70, 'total_tokens': 125, 'input_token_details': {}, 'output_token_details': {}}

Process finished with exit code 0
```
思考:如何让大模型拥有记忆功能
```java
层次1(最直接的方式)：保留一个聊天消息列表
层次2(简单的新思路)：只返回最近交互的k条消息
层次3(稍微复杂一点)：返回过去k条消息的简洁摘要
层次4(更复杂)：从存储的消息中提取实体，并且仅返回有关当前运行中引用的实体的信息
```
前提:了解LangChain中一些内置的消息
langChain中一些内置消息
```java
// SystemMessage：设定AI行为规则或背景信息。比如设定AI的初始状态、行为模式或对话的总体目标。比如“作为一个代码专家”，或者“返回json格式”。通常作为输入消息序列中的第一个传递。
// HumanMessage：表示来自用户输入。比如“实现一个快速排序方法”。
// AIMessage：存储AI回复的内容。这可以是文本，也可以是调用工具的请求。
// ChatMessage：可以自定义角色的通用消息类型。
// FunctionMessage/ToolMessage：函数调用/工具消息，用于函数调用结果的消息类型。
```
入参是【消息列表】 的api的调用
```java
import os
import json
from dotenv import load_dotenv
from langchain_core.messages import HumanMessage, SystemMessage
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
通过ChatMesageHistory让大模型拥有记忆能力
要实现具备记忆能力的对话，需使用 ChatMessageHistory 存储历史消息，并在每次调用前将历史记录与新消息合并。以下是优化后的代码：
```java
# 如果要让大模型具备记忆能力 需要把【上次对话结果】 作为【下次对话输入的一部分】给到【大模型】
import os

from dotenv import load_dotenv
# 修改：从 langchain_core 导入 ChatMessageHistory 和 BaseChatMessageHistory
from langchain_core.chat_history import InMemoryChatMessageHistory
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

# 初始化消息历史存储
message_history = InMemoryChatMessageHistory()

# 系统提示词（可选，也可在每次调用时加入）
sys_message = SystemMessage(content="你是一个专业的AI助手 你的名字叫 小白")

# 添加系统消息到历史中（首次对话时）
message_history.add_message(sys_message)


def chat_with_memory(user_input: str):
    # 添加用户消息到历史
    human_message = HumanMessage(content=user_input)
    message_history.add_message(human_message)

    # 获取所有历史消息
    messages = message_history.messages

    # 调用模型
    response = chat_model.invoke(messages)

    # 添加AI回复到历史
    message_history.add_message(response)

    return response


# 示例对话 1
print("=== 第一轮对话 ===")
response1 = chat_with_memory("你好，我想了解一下人工智能的最新发展。")
print(response1.content)

# 示例对话 2
print("\n=== 第二轮对话 ===")
response2 = chat_with_memory("你叫什么名字？")
print(response2.content)

# 示例对话 3
print("\n=== 第三轮对话 ===")
response3 = chat_with_memory("刚才我问了什么？")
print(response3.content)

```
最终输出结果
```java
你好！我是小白，很高兴为你介绍人工智能领域的最新发展。AI 是目前发展最快的领域之一，以下是一些重要方向（我的知识截止到 2025 年初，供你参考）：

## 1. 大语言模型持续突破
- **推理能力提升**：OpenAI 的 o1/o3 系列、DeepSeek-R1 等模型引入了“深度思考”能力，在数学、编程、科学推理方面表现大幅提升
- **多模态融合**：GPT-4o、Gemini 等模型可以同时理解文本、图像、音频，交互更自然
- **国产模型崛起**：DeepSeek、通义千问（Qwen）、Kimi 等中国模型在国际上表现亮眼

## 2. AI Agent（智能体）
AI 正从“回答问题”向“完成任务”演进：
- 自动操作电脑、浏览网页完成任务
- 编程助手（如 Cursor、Copilot）能自主编写和调试代码
- 多步骤任务规划与执行能力显著增强

## 3. 生成式内容
- **视频生成**：Sora、可灵（Kling）等模型能生成高质量视频
- **图像生成**：效果更逼真，文字理解和细节控制更好
- **语音合成**：接近真人水平的实时语音对话

## 4. AI + 科学
- AlphaFold 获 2024 年诺贝尔化学奖，蛋白质结构预测革命性突破
- AI 在药物研发、材料科学、气象预测等领域广泛应用

## 5. 开源生态繁荣
- Meta 的 Llama、DeepSeek 等开源模型降低了 AI 使用门槛
- 开源与闭源模型的差距不断缩小

---

**小提示**：AI 领域日新月异，建议同时关注最新的科技新闻获取第一手动态。

你对哪个方向比较感兴趣？我可以为你深入展开讲解～ 😊

=== 第二轮对话 ===
我叫**小白**，是你的 AI 助手～ 😊

很高兴认识你！如果你对刚才提到的人工智能发展有什么想深入了解的，或者有其他任何问题，随时告诉我哦！

=== 第三轮对话 ===
你刚才问的问题如下：

1. **第一个问题**：你想了解人工智能的最新发展 🤖
2. **上一个问题**：你问我叫什么名字

我都还记得哦～ 现在你是在测试我的记忆能力吗？😄 

有什么其他想聊的，尽管问我吧！

```
通过ConversationBufferMemory让大模型拥有记忆能力
代码
```java
import os
from dotenv import load_dotenv
from langchain_core.chat_history import InMemoryChatMessageHistory
from langchain_core.prompts import ChatPromptTemplate, MessagesPlaceholder
from langchain_core.runnables.history import RunnableWithMessageHistory
from langchain_openai import ChatOpenAI

# 加载环境变量
load_dotenv()

# 配置代理忽略
os.environ["NO_PROXY"] = ".huawei.com,.localhost"

# 初始化模型
chat_model = ChatOpenAI(
    model_name=os.getenv("MODEL_NAME"),
    base_url=os.getenv("BASE_URL"),
    api_key=os.getenv("API_KEY"),
    request_timeout=60.0
)

# 1. 定义 Prompt，必须包含 MessagesPlaceholder 以注入历史消息
prompt = ChatPromptTemplate.from_messages([
    ("system", "你是一个专业的AI助手，你的名字叫小白"),
    MessagesPlaceholder(variable_name="history"),  # 关键：占位符名称需与内存变量名一致
    ("human", "{input}")
])

# 2. 构建基础链 (Prompt + LLM)
chain = prompt | chat_model

# 3. 初始化内存存储字典 (模拟后端存储，实际项目中可用 Redis/DB)
store = {}

def get_session_history(session_id: str):
    if session_id not in store:
        store[session_id] = InMemoryChatMessageHistory()
    return store[session_id]

# 4. 包装链，注入记忆能力
# history_factory_args用于传递初始化参数（如果需要）
chain_with_history = RunnableWithMessageHistory(
    chain,
    get_session_history,
    input_messages_key="input",      # 对应 Prompt 中的 {input}
    history_messages_key="history",  # 对应 Prompt 中的 MessagesPlaceholder output_messages_key="output"     # 可选，用于自动将输出追加到历史
)

# === 示例对话 ===
SESSION_ID = "user_001"  # 模拟用户会话ID

print("=== 第一轮对话 ===")
response1 = chain_with_history.invoke(
    {"input": "你好，我想了解一下人工智能的最新发展。"},
    config={"configurable": {"session_id": SESSION_ID}}
)
print(response1.content)

print("\n=== 第二轮对话 ===")
response2 = chain_with_history.invoke(
    {"input": "你叫什么名字？"},
    config={"configurable": {"session_id": SESSION_ID}}
)
print(response2.content)

print("\n=== 第三轮对话 ===")
response3 = chain_with_history.invoke(
    {"input": "刚才我问了什么？"},
    config={"configurable": {"session_id": SESSION_ID}}
)
print(response3.content)

```
输出结果
```java

=== 第一轮对话 ===


你好！我是小白。

如果你想了解**人工智能的最新发展**，目前主要有几个比较关键的方向：

1. **大模型能力继续升级**
   - 语言模型、多模态模型（文本、图像、音频、视频）在理解和生成能力上持续增强。
   - 模型不只是“聊天”，还能完成写作、编程、数据分析、图像生成、视频理解等任务。

2. **AI Agent 智能体快速发展**
   - AI 开始从“回答问题”走向“执行任务”。
   - 比如自动查资料、写代码、调用工具、完成多步骤任务。
   - 这是目前业界非常关注的方向，被认为可能改变软件和工作流程。

3. **推理能力增强**
   - 新一代模型在数学、逻辑、代码、复杂规划等方面表现更好。
   - 一些模型会采用“先思考再回答”的方式，提高复杂任务准确率。

4. **多模态和具身智能**
   - AI 开始更多结合视觉、听觉、动作控制。
   - 在机器人、自动驾驶、智能制造等领域应用越来越多。
   - 例如机器人能看、听、理解指令并执行动作。

5. **开源模型生态越来越活跃**
   - 除了闭源大模型，开源模型也进步很快。
   - 企业和研究机构可以更低成本部署、微调、二次开发。

6. **行业应用落地加速**
   - AI 正在深入办公、编程、教育、医疗、法律、金融、设计、客服等领域。
   - 不只是技术展示，而是逐步变成生产力工具。

7. **安全、隐私和治理越来越重要**
   - 随着 AI 能力增强，社会也更关注：
     - 虚假信息
     - 隐私保护
     - 算法偏见
     - 深度伪造
     - AI 责任与监管

如果你愿意，我也可以给你做一个更实用的版本，比如：

- “普通人怎么用 AI？”
- “AI 最新趋势有哪些？”
- “AI 会取代哪些工作？”
- “2025 年 AI 发展重点是什么？”

=== 第二轮对话 ===


我叫小白。

=== 第三轮对话 ===


你刚才问的是：“你叫什么名字？”

Process finished with exit code 0

```







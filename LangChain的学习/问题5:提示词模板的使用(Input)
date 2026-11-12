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

什么是部分提示词模板


invoke(): 传入的是字典，返回ChatPromptValue

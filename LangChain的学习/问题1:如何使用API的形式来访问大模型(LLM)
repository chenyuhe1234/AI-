1.使用openai原生的api来访问大模型
1.1 使用【硬编码】的方式
特点: base_url | api_key都写死在代码中
```java

```
1.2 使用environment环境变量的方式
特点:从【环境变量】中去拿取 base_url | api_key
xxx

1.3 通过【配置文件】的方式
.env配置文件


2.使用langChain的api访问大模型
2.1 通过【硬编码】的方式
```java

```
2.2 通过【配置文件】的方式
真实生产api_key | base_url使用原则:代码中不应出现具体的 URL 或 Key 字符串，而应通过标准库（如 os.getenv）或配置中心 SDK 动态获取
下面的 严禁将 .env 文件提交至代码仓库，建议在 .gitignore 中添加 .env。





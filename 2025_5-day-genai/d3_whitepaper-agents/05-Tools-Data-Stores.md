# Data stores

数据存储

Imagine a language model as a vast library of books, containing its training data. But unlike a library that continuously acquires new volumes, this one remains static, holding only the knowledge it was initially trained on. This presents a challenge, as real-world knowledge is constantly evolving. Data Stores address this limitation by providing access to more dynamic and up-to-date information, and ensuring a model’s responses remain grounded in factuality and relevance.

把语言模型 (Language Model) 想象成一座巨大的图书馆，里面装的是它的训练数据。但和不断购入新书的图书馆不同，这座图书馆是静止的，只保有它最初训练时的知识。这带来一个难题，因为现实世界的知识在不断变化。数据存储 (Data Store) 针对的就是这个限制：提供更动态、更新的信息，并让模型的响应保持在事实和相关性上有依据。

Consider a common scenario where a developer might need to provide a small amount of additional data to a model, perhaps in the form of spreadsheets or PDFs.

设想一个常见情形：开发者可能需要给模型提供少量额外数据，形式也许是电子表格或 PDF。

![How agents interact with structured and unstructured data](image_009_page_27.png)

图 10：智能体如何与结构化和非结构化数据交互？智能体与私有文档、网站、结构化数据之间还隔着一个问号。

Data Stores allow developers to provide additional data in its original format to an agent, eliminating the need for time-consuming data transformations, model retraining, or fine-tuning. The Data Store converts the incoming document into a set of vector database embeddings that the agent can use to extract the information it needs to supplement its next action or response to the user.

数据存储允许开发者把额外数据以其原始格式提供给智能体 (Agent)，不必再花时间做数据变换、重新训练模型或微调 (Fine-tuning)。数据存储把进来的文档转换成一组向量数据库嵌入 (embedding)，智能体可以用它们抽出所需信息，来补充下一步行动或给用户的响应。

![Data stores connect agents to real-time data sources](image_010_page_28.png)

图 11：数据存储把智能体连接到各类新的实时数据源：私有文档、网站和结构化数据。

---

## Implementation and application

实现与应用

In the context of Generative AI agents, Data Stores are typically implemented as a vector database that the developer wants the agent to have access to at runtime. While we won’t cover vector databases in depth here, the key point to understand is that they store data in the form of vector embeddings, a type of high-dimensional vector or mathematical representation of the data provided. One of the most prolific examples of Data Store usage with language models in recent times has been the implementation of Retrieval Augmented Generation (RAG) based applications. These applications seek to extend the breadth and depth of a model’s knowledge beyond the foundational training data by giving the model access to data in various formats like:

在生成式 AI (Generative AI) 智能体的语境里，数据存储通常实现为开发者希望智能体在运行时能够访问的向量数据库。这里不深入讲向量数据库，关键是要理解：它们以向量嵌入的形式存储数据，也就是所提供数据的一种高维向量或数学表示。近来，语言模型使用数据存储最常见的例子，是基于检索增强生成 (Retrieval Augmented Generation, RAG) 的应用。这些应用试图把模型的知识在广度和深度上延伸到基础训练数据之外，办法是让模型访问各种格式的数据，例如：

- Website content
- Structured Data in formats like PDF, Word Docs, CSV, Spreadsheets, etc.
- Unstructured Data in formats like HTML, PDF, TXT, etc.

- 网站内容

- 结构化数据，格式如 PDF、Word 文档、CSV、电子表格等

- 非结构化数据，格式如 HTML、PDF、TXT 等

![One-to-many relationship between agents and data stores](image_011_page_29.png)

图 12：智能体与数据存储的一对多关系。数据存储可以代表各类预先索引的数据：非结构化存储对应入职 PDF，网站存储对应 cloud.google.com/blog，结构化存储对应财务表格。

The underlying process for each user request and agent response loop is generally modeled as seen in Figure 13.

每一次用户请求与智能体响应的循环，其底层过程大体如图 13 所示。

1. A user query is sent to an embedding model to generate embeddings for the query
2. The query embeddings are then matched against the contents of the vector database using a matching algorithm like SCaNN
3. The matched content is retrieved from the vector database in text format and sent back to the agent
4. The agent receives both the user query and retrieved content, then formulates a response or action
5. A final response is sent to the user

1. 用户查询被送到一个嵌入模型，为查询生成嵌入

2. 再用类似 SCaNN 的匹配算法，把查询嵌入与向量数据库的内容进行匹配

3. 匹配到的内容以文本形式从向量数据库取出，送回智能体

4. 智能体同时收到用户查询和取回的内容，然后组织响应或行动

5. 最终响应发给用户

![Lifecycle of a user request and agent response in a RAG application](image_012_page_30.png)

图 13：基于 RAG 的应用中，用户请求与智能体响应的生命周期。用户查询生成嵌入，嵌入进入向量数据库，取回内容交给智能体，智能体再给出响应。

The end result is an application that allows the agent to match a user’s query to a known data store through vector search, retrieve the original content, and provide it to the orchestration layer and model for further processing. The next action might be to provide a final answer to the user, or perform an additional vector search to further refine the results.

最终得到的应用，能让智能体通过向量搜索把用户查询匹配到一个已知的数据存储，取回原始内容，再交给编排层 (Orchestration Layer) 和模型做进一步处理。下一步行动可以是向用户给出最终答案，也可以再做一次向量搜索，把结果收得更准。

A sample interaction with an agent that implements RAG with ReAct reasoning/planning can be seen in Figure 14.

图 14 是一个实现了 RAG、并采用 ReAct 推理 / 规划的智能体交互示例。

![Sample RAG application with ReAct reasoning and planning](image_013_page_31.png)

图 14：带 ReAct 推理 / 规划的 RAG 应用示例。用户问「我们的育儿假政策是什么？」；思考是去找最匹配的数据存储；行动是向量搜索；观察来自 pdf 数据存储；最终答案概括 Google 的休假政策。可选工具还有网站数据存储和表格数据存储。

---

## Tools recap

工具回顾

To summarize, extensions, functions and data stores make up a few different tool types available for agents to use at runtime. Each has their own purpose and they can be used together or independently at the discretion of the agent developer.

总结一下：扩展、函数和数据存储，是智能体在运行时可以使用的几种不同工具类型。每一种都有自己的用途，可以一起用，也可以单独用，由智能体开发者决定。

| | Extensions | Function Calling | Data Stores |
| --- | --- | --- | --- |
| Execution | Agent-Side Execution | Client-Side Execution | Agent-Side Execution |
| Use Case | • Developer wants agent to control interactions with the API endpoints<br>• Useful when leveraging native pre-built Extensions (i.e. Vertex Search, Code Interpreter, etc.)<br>• Multi-hop planning and API calling (i.e. the next agent action depends on the outputs of the previous action / API call) | • Security or Authentication restrictions prevent the agent from calling an API directly<br>• Timing constraints or order-of-operations constraints that prevent the agent from making API calls in real-time. (i.e. batch operations, human-in-the-loop review, etc.)<br>• API that is not exposed to the internet, or non-accessible by Google systems | Developer wants to implement Retrieval Augmented Generation (RAG) with any of the following data types:<br>• Website Content from pre-indexed domains and URLs<br>• Structured Data in formats like PDF, Word Docs, CSV, Spreadsheets, etc.<br>• Relational / Non-Relational Databases<br>• Unstructured Data in formats like HTML, PDF, TXT, etc. |

| | 扩展 | 函数调用 | 数据存储 |
| --- | --- | --- | --- |
| 执行 | 智能体侧执行 | 客户端执行 | 智能体侧执行 |
| 使用场景 | • 开发者希望由智能体控制与 API 端点的交互<br>• 在利用原生预制扩展时很有用（例如 Vertex Search、代码解释器等）<br>• 多跳规划与 API 调用（即智能体的下一步行动取决于上一步行动 / API 调用的输出） | • 安全或认证限制使智能体不能直接调用 API<br>• 时序约束或操作顺序约束，使智能体不能实时发起 API 调用（例如批处理、人在回路审核等）<br>• API 不暴露在互联网上，或 Google 系统访问不到 | 开发者希望用下列任一数据类型实现检索增强生成 (RAG)：<br>• 来自预先索引的域名和 URL 的网站内容<br>• 结构化数据，格式如 PDF、Word 文档、CSV、电子表格等<br>• 关系型 / 非关系型数据库<br>• 非结构化数据，格式如 HTML、PDF、TXT 等 |

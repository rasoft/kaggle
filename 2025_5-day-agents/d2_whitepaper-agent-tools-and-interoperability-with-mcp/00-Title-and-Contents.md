# Agent Tools & Interoperability with MCP

智能体工具与互操作性：模型上下文协议 (Agent Tools & Interoperability with MCP)

Authors: Mike Styer, Kanchana Patlolla, Madhurranjan Mohaan, Santiago Díaz, and Anant Nawalgaria

作者：Mike Styer、Kanchana Patlolla、Madhurranjan Mohaan、Santiago Díaz、Anant Nawalgaria

Updated May 2026

2026 年 5 月更新

---

## Acknowledgements

致谢

Content contributors

内容贡献者

Antony Arul

Ruben Gonzalez

Che Liu

Kimberly Milam

Geir Sjurseth

Curators and editors

策划与编辑

Anant Nawalgaria

Kanchana Patlolla

Designer

设计师

Michael Lanning

---

## Table of contents

目录

The printed table of contents runs one page ahead of the page numbers in the footers. The list below follows the footer page numbers.

印刷目录的页码比页脚页码大 1。下面按页脚页码列出。

Introduction: Models, Tools and Agents — 6

引言：模型、工具与智能体 — 6

Tools and tool calling — 8

工具与工具调用 — 8

What do we mean by a tool? — 8

工具是什么 — 8

Types of tools — 9

工具的类型 — 9

Built-in tools — 11

内置工具 — 11

Agent Tools — 12

智能体工具 — 12

Best Practices — 14

最佳实践 — 14

Documentation is important — 15

文档很重要 — 15

Describe actions, not implementations — 17

描述动作，不要描述实现 — 17

Publish tasks, not API calls — 18

发布任务，不要发布 API 调用 — 18

Make tools as granular as possible — 18

工具尽量拆细 — 18

Design for concise output — 19

为简洁输出而设计 — 19

Use validation effectively — 19

用好校验 — 19

Understanding the Model Context Protocol — 20

理解模型上下文协议 — 20

The "N x M" Integration Problem and the need for Standardization — 20

「N × M」集成问题，以及为什么需要标准化 — 20

Core Architectural Components: Hosts, Clients, and Servers — 21

核心架构组件：宿主、客户端与服务器 — 21

The Communication Layer: JSON-RPC, Transports, and Message Types — 23

通信层：JSON-RPC、传输与消息类型 — 23

Key Primitives: Tools and others — 24

关键原语：工具及其他 — 24

Tool Definition — 26

工具定义 — 26

Tool Results — 29

工具结果 — 29

Structured Content — 29

结构化内容 — 29

Error Handling — 30

错误处理 — 30

Other Capabilities — 31

其他能力 — 31

Resources — 32

资源 — 32

Prompts — 32

提示 — 32

Sampling — 33

采样 — 33

Elicitation — 33

征询 — 33

Roots — 34

根 — 34

Model Context Protocol: For and Against — 35

模型上下文协议：赞成与反对 — 35

Capabilities and Strategic Advantages — 35

能力与战略优势 — 35

Accelerating Development and Fostering a Reusable Ecosystem — 35

加快开发，并培育可复用的生态 — 35

Architectural Flexibility and Future-Proofing — 36

架构灵活性与面向未来 — 36

Foundations for Governance and Control — 37

治理与控制的基础 — 37

Critical Risks and Challenges — 38

关键风险与挑战 — 38

Enterprise Readiness Gaps — 39

企业就绪程度的缺口 — 39

Security in MCP — 41

MCP 中的安全 — 41

New threat landscape — 41

新的威胁版图 — 41

Risks and Mitigations — 42

风险与缓解 — 42

Tool Shadowing — 44

工具遮蔽 — 44

Malicious Tool Definitions and Consumed Contents — 46

恶意工具定义与被消费的内容 — 46

Sensitive information Leaks — 47

敏感信息泄露 — 47

No support for limiting the scope of access — 48

不支持限制访问范围 — 48

Conclusion — 49

结论 — 49

Appendix — 50

附录 — 50

Confused Deputy problem — 50

混淆代理人问题 — 50

The Attack — 51

攻击 — 51

The Result — 52

结果 — 52

Endnotes — 53

尾注 — 53

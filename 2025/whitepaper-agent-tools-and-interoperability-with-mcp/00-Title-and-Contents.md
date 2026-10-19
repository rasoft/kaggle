# Agent Tools & Interoperability with MCP

<mark>智能体工具与互操作性：模型上下文协议 (Agent Tools & Interoperability with MCP)</mark>

Authors: Mike Styer, Kanchana Patlolla, Madhurranjan Mohaan, Santiago Díaz, and Anant Nawalgaria

<mark>作者：Mike Styer、Kanchana Patlolla、Madhurranjan Mohaan、Santiago Díaz、Anant Nawalgaria</mark>

Updated May 2026

<mark>2026 年 5 月更新</mark>

---

## Acknowledgements

<mark>致谢</mark>

Content contributors

<mark>内容贡献者</mark>

Antony Arul

Ruben Gonzalez

Che Liu

Kimberly Milam

Geir Sjurseth

Curators and editors

<mark>策划与编辑</mark>

Anant Nawalgaria

Kanchana Patlolla

Designer

<mark>设计师</mark>

Michael Lanning

---

## Table of contents

<mark>目录</mark>

The printed table of contents runs one page ahead of the page numbers in the footers. The list below follows the footer page numbers.

<mark>印刷目录的页码比页脚页码大 1。下面按页脚页码列出。</mark>

Introduction: Models, Tools and Agents — 6

<mark>引言：模型、工具与智能体 — 6</mark>

Tools and tool calling — 8

<mark>工具与工具调用 — 8</mark>

What do we mean by a tool? — 8

<mark>工具是什么 — 8</mark>

Types of tools — 9

<mark>工具的类型 — 9</mark>

Built-in tools — 11

<mark>内置工具 — 11</mark>

Agent Tools — 12

<mark>智能体工具 — 12</mark>

Best Practices — 14

<mark>最佳实践 — 14</mark>

Documentation is important — 15

<mark>文档很重要 — 15</mark>

Describe actions, not implementations — 17

<mark>描述动作，不要描述实现 — 17</mark>

Publish tasks, not API calls — 18

<mark>发布任务，不要发布 API 调用 — 18</mark>

Make tools as granular as possible — 18

<mark>工具尽量拆细 — 18</mark>

Design for concise output — 19

<mark>为简洁输出而设计 — 19</mark>

Use validation effectively — 19

<mark>用好校验 — 19</mark>

Understanding the Model Context Protocol — 20

<mark>理解模型上下文协议 — 20</mark>

The "N x M" Integration Problem and the need for Standardization — 20

<mark>「N × M」集成问题，以及为什么需要标准化 — 20</mark>

Core Architectural Components: Hosts, Clients, and Servers — 21

<mark>核心架构组件：宿主、客户端与服务器 — 21</mark>

The Communication Layer: JSON-RPC, Transports, and Message Types — 23

<mark>通信层：JSON-RPC、传输与消息类型 — 23</mark>

Key Primitives: Tools and others — 24

<mark>关键原语：工具及其他 — 24</mark>

Tool Definition — 26

<mark>工具定义 — 26</mark>

Tool Results — 29

<mark>工具结果 — 29</mark>

Structured Content — 29

<mark>结构化内容 — 29</mark>

Error Handling — 30

<mark>错误处理 — 30</mark>

Other Capabilities — 31

<mark>其他能力 — 31</mark>

Resources — 32

<mark>资源 — 32</mark>

Prompts — 32

<mark>提示 — 32</mark>

Sampling — 33

<mark>采样 — 33</mark>

Elicitation — 33

<mark>征询 — 33</mark>

Roots — 34

<mark>根 — 34</mark>

Model Context Protocol: For and Against — 35

<mark>模型上下文协议：赞成与反对 — 35</mark>

Capabilities and Strategic Advantages — 35

<mark>能力与战略优势 — 35</mark>

Accelerating Development and Fostering a Reusable Ecosystem — 35

<mark>加快开发，并培育可复用的生态 — 35</mark>

Architectural Flexibility and Future-Proofing — 36

<mark>架构灵活性与面向未来 — 36</mark>

Foundations for Governance and Control — 37

<mark>治理与控制的基础 — 37</mark>

Critical Risks and Challenges — 38

<mark>关键风险与挑战 — 38</mark>

Enterprise Readiness Gaps — 39

<mark>企业就绪程度的缺口 — 39</mark>

Security in MCP — 41

<mark>MCP 中的安全 — 41</mark>

New threat landscape — 41

<mark>新的威胁版图 — 41</mark>

Risks and Mitigations — 42

<mark>风险与缓解 — 42</mark>

Tool Shadowing — 44

<mark>工具遮蔽 — 44</mark>

Malicious Tool Definitions and Consumed Contents — 46

<mark>恶意工具定义与被消费的内容 — 46</mark>

Sensitive information Leaks — 47

<mark>敏感信息泄露 — 47</mark>

No support for limiting the scope of access — 48

<mark>不支持限制访问范围 — 48</mark>

Conclusion — 49

<mark>结论 — 49</mark>

Appendix — 50

<mark>附录 — 50</mark>

Confused Deputy problem — 50

<mark>混淆代理人问题 — 50</mark>

The Attack — 51

<mark>攻击 — 51</mark>

The Result — 52

<mark>结果 — 52</mark>

Endnotes — 53

<mark>尾注 — 53</mark>

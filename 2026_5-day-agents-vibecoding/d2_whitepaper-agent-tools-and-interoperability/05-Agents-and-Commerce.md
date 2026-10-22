# Agents and Commerce (AP2 and UCP)

智能体与商务（AP2 与 UCP）

## Autonomous Procurement with a workflow example

用一个工作流例子看自主采购

Vibe coders learn checkout, catalog, order capability and mandate with their agents.

氛围编码者 (vibe coder) 和他们的智能体 (Agent) 一起学习结账、目录、下单能力，以及授权委托 (Mandate)。

---

## Key characteristics and benefits of Protocols

协议的关键特征与好处

Typed schemas, Security and open source (Integration debt and vendor neutrality)

带类型的 schema、安全，以及开源（集成债与厂商中立）。

Lab recommendations: https://codelabs.developers.google.com/next26/adk-agent-commerce#0

实验建议：https://codelabs.developers.google.com/next26/adk-agent-commerce#0

---

While earlier sections focused on how coding agents interact with tools, other agents, and user interfaces within an Agentic framework, those interactions are often limited to "read" operations using protocols like MCP, A2A, and A2UI. As these systems evolve, agents must transition toward executing "actions" that carry real-world financial implications.

前面几节关注的是，编码智能体在智能体框架里如何与工具 (Tools)、其他智能体和用户界面交互。这些交互常常限于「读」操作，用的是 MCP（模型上下文协议，Model Context Protocol）、A2A（智能体对智能体，Agent-to-Agent）和 A2UI（智能体到界面，Agent-to-User Interface）这类协议。随着这些系统演化，智能体必须转向执行带着真实财务后果的「动作」。

Prioritizing commerce protocols and building a robust operational harness ensures your agents adhere strictly to industry standards when managing transactions.

把商务协议放在优先位置，并建起稳健的运维驾驭层 (Harness)，才能保证智能体在管理交易时严格遵守行业标准。

To understand how to implement these systems, we must first explore the nature of these protocols and their complementary roles.

要理解怎么实现这些系统，得先看清这些协议的性质，以及它们如何互补。

---

## What is AP2 and UCP?

AP2 和 UCP 是什么？

![Figure 8: AP2 and UCP Ecosystem](image_011_page_44.png)

图 8：AP2 与 UCP 生态。你的 ADK 智能体向 UCP 发请求，UCP 覆盖结账、购物车、目录和订单，再向智能体商务发出请求。智能体商务把支付处理、握手、护栏和授权委托交给 AP2，AP2 完成后再回到 UCP，最后回到你的智能体。

Imagine you and your roommates are starving at 2:00 AM. You are too busy studying to stop, so you deploy your AI Smart Assistant to get food for the apartment. Here is how UCP (Universal Commerce Protocol) and AP2 (Agent Payments Protocol) split the workload to get that burrito to your dorm lobby.

想象你和室友凌晨 2 点饿得不行。你忙着学习，停不下来，于是派出 AI 智能助手给整间公寓买吃的。通用商务协议 (Universal Commerce Protocol, UCP) 和智能体支付协议 (Agent Payments Protocol, AP2) 是这样分工，把那份卷饼送到宿舍大厅的：

---

## UCP (Universal Commerce Protocol): The Ultimate Food Delivery App

UCP（通用商务协议）：终极外卖应用

In 2024, your AI would have to manually open Chrome, go to the local burrito place's poorly designed website, try to click the "extra guac" checkbox, and hope the site doesn't crash. Instead, UCP acts like a universal translator. Every restaurant on campus publishes their menu, hours, and customization options in a clean, standard machine language.

在 2024 年，你的 AI 得手动打开 Chrome，走进当地卷饼店那设计糟糕的网站，试着去点「加份鳄梨酱」的复选框，还得盼着网站别崩。UCP 则像一台通用翻译器。校园里每家餐厅都用干净、标准的机器语言发布菜单、营业时间和定制选项。

Your AI uses UCP to ask the restaurant’s system, "Are you still open? Do you have vegetarian burritos?". To build an order one could ask: "One chicken burrito, no onions, add sour cream, and a side of chips" and the restaurant responds back with the tax, delivery fee, and expected arrival time.

你的 AI 用 UCP 问餐厅的系统：「还营业吗？有素食卷饼吗？」要拼一份订单，可以问：「一份鸡肉卷饼，不要洋葱，加酸奶油，再加一份薯条。」餐厅回以税额、配送费和预计到达时间。

In short: UCP is how your AI talks to the store, looks at the options, and builds the perfect order. Prior to UCP, your application would have been able to discover and get information. However the interactions between these different providers need to be orchestrated individually. By standardizing the interaction, we make it easier for non-humans to interact with each other.

简而言之：UCP 是你的 AI 跟店家说话、看选项、拼出那份刚好的订单的方式。在 UCP 之前，应用能够发现并取得信息。但不同提供方之间的交互，仍得逐个编排 (Orchestration)。把交互标准化之后，非人类之间彼此打交道就容易得多。

---

## AP2 (Agent Payments Protocol): The Parent's Credit Card with Strict Rules

AP2（智能体支付协议）：带着严格规则的家长信用卡

Now the food is in the cart, but your AI needs to pay. You obviously aren't going to type your actual debit card number into an AI prompt and say "Go wild."

现在食物已经在购物车里，但你的 AI 得付钱。你显然不会把真实的借记卡号打进 AI 提示词，然后说「随便花」。

AP2 is the open, shared protocol that provides a common language for secure, compliant transactions between agents and merchants that lets your AI pay for the food only within rules you set.

AP2 是开放的、共享的协议。它为智能体和商户之间安全、合规的交易提供共同语言，让你的 AI 只在你设定的规则之内为食物付款。

- **The Guardrails (The Mandate):** Before you send the AI off, you approve a digital rule: "You can spend up to $25 at Taco Bell."

**护栏 (Guardrails)（授权委托）：** 把 AI 派出去之前，你批准一条数字规则：「你在 Taco Bell 最多可以花 25 美元。」

- **The Handshake:** When the AI checks out, it doesn't show your card number. It shows a digital, encrypted "promissory note" signed by you that says: "My human approved this $18.50 order." The restaurant's bank instantly verifies this digital signature.

**握手 (Handshake)：** AI 结账时不出示你的卡号。它出示一张由你签署的、加密的数字「付款承诺」：「我的人类批准了这笔 18.50 美元的订单。」餐厅的银行立刻验证这个数字签名。

- **No Hidden Fees:** If the restaurant tries to sneakily charge you $50 instead of $18.50, the AP2 protocol blocks it instantly because it violates the rules you signed off on.

**没有隐藏费用：** 如果餐厅想偷偷收 50 美元而不是 18.50 美元，AP2 协议会立刻拦住，因为它违反了你签过字的规则。

In short: AP2 is the secure lockbox that lets your AI pay for things using your money, but ensures it can never buy a $1,000 TV by mistake.

简而言之：AP2 是一只安全保险箱。它让你的 AI 用你的钱付款，同时保证它绝不会失手买下一台 1,000 美元的电视。

**Table 3: Comparison for UCP and AP2**

表 3：UCP 与 AP2 的对照

| UCP | AP2 |
| --- | --- |
| Brain that decides what to buy, handles the menu, and puts the food in the cart. | Is the wallet that securely handles how to pay for it without you getting scammed. |
| Integrates with any business provider | Integrates with payment |
| Unified integration<br>Shared language<br>Extensible architecture<br>Security-first approach | Authorization & Auditability<br>Authenticity of Intent<br>Agent Error and Hallucination<br>Accountability |

| UCP | AP2 |
| --- | --- |
| 决定买什么的大脑：处理菜单，把食物放进购物车。 | 是钱包：安全地处理怎么付钱，让你不被骗。 |
| 与任何商业提供方集成 | 与支付集成 |
| 统一集成；共享语言；可扩展架构；安全优先 | 授权与可审计；意图的真实性；智能体错误与幻觉；问责 |

- If you are a developer building your UCP agent for a merchant or the payment processor, follow the instructions [here](https://developers.google.com/merchant/ucp/guides/integration-ui/integration).

如果你是开发者，正在为商户或支付处理方构建 UCP 智能体，按[这里](https://developers.google.com/merchant/ucp/guides/integration-ui/integration)的说明做。

- If you are a developer building your AP2 agent for a merchant or the payment processor, follow the instructions [here](https://ap2-protocol.org/ap2/implementation_considerations/#roles).

如果你是开发者，正在为商户或支付处理方构建 AP2 智能体，按[这里](https://ap2-protocol.org/ap2/implementation_considerations/#roles)的说明做。

- If you are a developer building an agent that consumes an AP2 agent such as a shopper, follow the instructions [here](https://ap2-protocol.org/ap2/implementation_considerations/#roles).

如果你是开发者，正在构建消费 AP2 智能体的一方，例如购物者，按[这里](https://ap2-protocol.org/ap2/implementation_considerations/#roles)的说明做。

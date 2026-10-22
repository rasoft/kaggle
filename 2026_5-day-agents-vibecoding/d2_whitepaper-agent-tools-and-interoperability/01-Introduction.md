# Introduction

引言

> Software's next evolution isn't written: it's orchestrated by interoperable agents.

软件的下一场演化不再是写出来的：它由可互操作的智能体 (Agent) 编排而成。

---

In Day 1, we outlined the paradigm shift from traditional software development to Agentic Engineering, introducing the Factory Model where your primary output as a developer is no longer raw syntax, but the system that produces code. We defined the core architecture of this system:

在第 1 天，我们勾勒了从传统软件开发到智能体工程 (Agentic Engineering) 的范式转移，并引入工厂模型 (Factory Model)：开发者的主要产出不再是原始语法，而是那个生产代码的系统。我们定义了这套系统的核心架构：

![Agent equals Model plus Harness](2026_5-day-agents-vibecoding/d2_whitepaper-agent-tools-and-interoperability/images/image_001_page_6.png)

智能体 = 模型 (Model) + 驾驭层 (Harness)。

---

If Agentic Engineering represents the factory floor you are orchestrating, then MCP, A2A, A2UI, AP2, and UCP are the Industry Standards—the uniform nuts and bolts and screw sizes, data formats, and communication channels—that allow your machinery to safely interact with the rest of the world.

如果智能体工程是你正在编排的厂房，那么 MCP、A2A、A2UI、AP2 和 UCP 就是行业标准：统一的螺母、螺栓和螺距，统一的数据格式和通信信道。有了它们，你的机器才能安全地与外部世界交互。

Without these open protocols, every agent you build exists as an isolated "custom machine" in a garage. You are forced to spend your hours and tokens writing fragile, bespoke wrappers for every single tool and API connection, trapping you in a low-leverage Conductor role.

没有这些开放协议，你造出的每一个智能体都只是车库里一台孤立的「定制机器」。你不得不把时间和 token 花在为每一个工具和 API 连接编写脆弱的专用包装器上，把自己困在低杠杆的指挥 (Conductor) 角色里。

By adopting standardized interoperability layers, you transform your agent's Harness into a modular, plug-and-play platform. You spend less time debugging custom JSON payloads and more time directing high-level intent as an Orchestrator.

采用标准化的互操作性 (Interoperability) 层之后，智能体的驾驭层会变成模块化、即插即用的平台。你少花时间调试定制 JSON 载荷，把更多时间用来以编排者 (Orchestrator) 的身份下达高层意图。

- OpenResponses & Interactions API are both “Power Plugs”, modern API approaches to LLM inference which support long running tasks. These blur the line between a stateless single turn and a stateful agent.

OpenResponses 和 Interactions API 都是「电源插头」：面向大语言模型 (LLM) 推理的现代 API，支持长时间运行的任务。它们模糊了无状态单轮与有状态智能体之间的界线。

- MCP (Model Context Protocol) acts as the "USB-C" within your agent's harness, instantly connecting models to databases, filesystems, and web APIs.

MCP（模型上下文协议，Model Context Protocol）是智能体驾驭层里的「USB-C」，把模型立刻接到数据库、文件系统和 Web API 上。

- Skills are “Playbooks”, very simple markdown instructions and scripts or tools which can be used in a sandbox environment like a terminal.

技能 (Skills) 是「剧本」(Playbooks)：非常简单的 Markdown 指令，加上可以在终端这类沙箱环境里使用的脚本或工具 (Tools)。

- A2A (Agent-to-Agent) serves as the "Factory Radio", allowing specialized agents to negotiate, brain-storm, and delegate tasks to each other.

A2A（智能体对智能体，Agent-to-Agent）是「工厂无线电」，让专门的智能体彼此协商、头脑风暴，并把任务委派出去。

- A2UI (Agent-to-User Interface) behaves like a "Generative Display Window", turning raw, complex JSON outputs into safe, interactive visual components for human operators.

A2UI（智能体到界面，Agent-to-User Interface）像一扇「生成式展示窗」，把原始、复杂的 JSON 输出变成给人类操作者使用的安全、可交互视觉组件。

- AP2 and UCP act as the "Global Supply Chain & Transaction Network", allowing agents to securely negotiate and execute autonomous commercial transactions.

AP2（智能体支付协议，Agent Payments Protocol）和 UCP（通用商务协议，Universal Commerce Protocol）是「全球供应链与交易网络」，让智能体能够安全地协商并执行自主商业交易。

---

This paper focuses on how vibe coders can rapidly utilize some of these protocols to construct a virtual data and execution team in a single afternoon.

这篇关注氛围编码者 (vibe coder) 如何在一个下午里，用其中一些协议迅速搭起一支虚拟的数据与执行团队。

![Figure 1: Ecosystem of Agent Protocols](image_002_page_8.png)

图 1：智能体协议生态。智能体逻辑居中，经 A2A 连接其他智能体，经 MCP 连接工具，经 AP2 连接商务网关，经 UCP 连接供应链与发现，经 A2UI 连接用户界面。

---

## Why this paper, why now

为什么是这篇，为什么是现在

In the era of vibecoding with less structure, harnesses and protocols help build trust in the agent development process. While velocity of outcome remains the primary driver for practitioners and developers, standardized protocols allow us to expand much further in achieving complex goals by transforming isolated "custom machines" into modular, interoperable platforms. Without agreed upon open standards, developers are creating tech debt, each API is a standard-of-one. These are low-leverage tasks, writing fragile, bespoke wrappers for every tool, maintaining them over time and adapting to other’s needs. Adopting these layers allows for a shift from being a mere builder to a high-level orchestrator.

在结构更少的氛围编码 (vibe coding) 时代，驾驭层和协议帮助人们信任智能体的开发过程。结果的速度仍然是实践者和开发者的首要驱动力，但标准化协议让我们走得更远：把孤立的「定制机器」变成模块化、可互操作的平台，从而达成复杂目标。没有公认的开放标准，开发者就在制造技术债，每一个 API 都是只属于自己的标准。为每个工具写脆弱的专用包装器、长期维护、再去迁就别人的需求，都是低杠杆的活。采用这些层，人才能从单纯的建造者，转成高层编排者。

---

## Who this paper is for

这篇写给谁

This paper is specifically designed for software engineers, engineering managers, architects, and technical leaders who recognize that the shift toward Agentic Engineering requires strict adherence to protocols to maintain the fidelity and reliability of outcomes. It serves as a practical guide for "vibe coders" who prioritize speed and visual results, demonstrating how to construct a virtual data and execution team.

这篇专门写给软件工程师、工程经理、架构师和技术负责人：他们已经看到，走向智能体工程必须严格遵守协议，结果的保真和可靠才站得住。它也是一份给「氛围编码者」的实用指南。这类人把速度和看得见的结果放在前面。文中演示如何组建一支虚拟的数据与执行团队。

> **Applied Tip:**
>
> In the Day 1 whitepaper, we recommended using an AGENTS.MD file to provide standard guidance for coding agents.
>
> Always begin by thinking deeply before you code—explicitly stating your assumptions, surfacing tradeoffs, and halting to ask for clarification the moment you encounter ambiguity rather than guessing silently.
>
> Write only the absolute minimum amount of code required to solve the immediate problem, strictly avoiding speculative features, unrequested abstractions, or predictive configurations.
>
> When editing existing code, make highly surgical changes by restricting your updates only to the exact lines necessary to fulfill the request, maintaining the existing style perfectly, and leaving adjacent, unbroken code completely untouched unless your changes directly orphaned an import or variable.
>
> Finally, approach every task through goal-driven execution by breaking it down into a clear, step-by-step plan with strong success criteria, such as writing a reproducing or failing test first and independently looping through verification until that specific goal is strictly met.

**实践提示：**

第 1 天的白皮书建议用一份 AGENTS.MD，给编码智能体提供标准指引。

动手写代码之前，先想清楚：明确写出你的假设，把取舍摆到台面上，一遇到含糊就停下来问，不要默默猜测。

只写解决眼前问题所必需的最少代码。推测性功能、没人要的抽象、预先设想的配置，一律不做。

改已有代码时做手术式修改：只动完成请求所必需的那些行，完整保持原有风格。相邻且没坏的代码不要碰，除非你的改动直接让某个 import 或变量变成孤儿。

最后，用目标驱动的方式做每一件事：拆成清晰的逐步计划，并带上硬的成功标准。例如先写一个能复现或会失败的测试，再独立循环验证，直到这个具体目标被严格满足。

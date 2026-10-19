# Agent-to-Agent (A2A) Interoperability

<mark>智能体对智能体 (A2A) 互操作性</mark>

As AI systems transition into distributed networks of specialized domain experts, standardized communication becomes essential for scaling. This section explores the Agent-to-Agent (A2A) protocol as the foundational layer that resolves ecosystem fragmentation, enabling developers to discover, orchestrate, and monetize a globally interoperable virtual workforce.

<mark>当 AI 系统变成由领域专家组成的分布式网络，标准化通信就成了扩张的前提。这一节把智能体对智能体协议 (Agent-to-Agent, A2A) 当作解决生态碎片化的基础层：开发者可以借此发现、编排 (Orchestration) 并变现一支全球可互操作的虚拟劳动力。</mark>

---

## The Evolution of Agentic Architectures

<mark>智能体架构的演化</mark>

To understand where Vibe Coding fits into the evolution of agentic architectures, we can observe a recurring pattern in technology: the shift from manual, low-level configuration to high-level, intent-based, declarative orchestration when users don’t say HOW to build something but WHAT they need.

<mark>要理解氛围编码 (Vibe Coding) 落在智能体架构演化的哪一段，可以看技术里反复出现的一种模式：从手工的、低层的配置，转向高层的、基于意图的声明式编排。用户不再说怎么造，只说需要什么。</mark>

A parallel trend is found in the history of IT infrastructure where we transitioned from manual configurations to "Infrastructure as Code" declarative scripts. A similar trend happened in the history of Machine Learning. The visionary premise from Google behind Automated Machine Learning (AutoML) was to democratize AI by automating the "drudge work" of model creation:

<mark>IT 基础设施的历史上有一条平行的轨迹：从手工配置转到「基础设施即代码」的声明式脚本。机器学习的历史里也发生过类似的事。Google 提出自动机器学习 (AutoML) 时的设想，是把创建模型 (Model) 的「苦力活」自动化，从而把 AI 交到更多人手里：</mark>

> "One way we hope to make AI more accessible is by simplifying the creation of machine learning models called neural networks. Today, designing neural nets is extremely time intensive... That’s why we’ve created an approach called AutoML, showing that it’s possible for neural nets to design neural nets. We hope AutoML will take an ability that a few PhDs have today …."<sup>1</sup>

<mark>「我们希望让 AI 更容易获得的一种办法，是简化被称为神经网络的机器学习模型的创建。今天，设计神经网络极其耗时……所以我们做了一种叫 AutoML 的方法，表明神经网络可以设计神经网络。我们希望 AutoML 能接过今天只有少数博士才有的那种能力……。」<sup>1</sup></mark>

Today, technology enables us to vibe code entire applications. However, the trajectory of agentic architectures used to vibe code these applications is currently mirroring one of the most significant shifts in software history: the transition from Monolithic to Microservices architectures.

<mark>今天，技术已经让我们能用氛围编码做出完整的应用。但用来氛围编码这些应用的智能体架构，正在重演软件史上最重要的一次转移：从单体架构走向微服务架构。</mark>

Just as early web applications were built as single, massive codebases where every function (billing, UI, database) was tightly coupled, many initial vibe coding projects relied on a "Swiss Army knife" Single Agent Monolith. This involves relying on a single, highly sophisticated prompt where one agent wears multiple hats with many connected tools to handle everything from database queries to UI rendering and testing. While this allows a developer to wire together a prototype in a weekend, it eventually hits the same "Monolithic Ceiling" that plagued early web apps:

<mark>早期 Web 应用是单一、巨大的代码库，计费、界面、数据库每一项功能都紧耦合。许多最初的氛围编码项目也靠一把「瑞士军刀」式的单智能体单体。它依赖一条高度复杂的提示词：一个智能体 (Agent) 戴很多顶帽子，接上一大堆工具 (Tools)，从数据库查询到界面渲染和测试全都包下来。开发者可以在一个周末把原型接起来，但最终会撞上曾经困住早期 Web 应用的同一面「单体天花板」(Monolithic Ceiling)：</mark>

- **Scaling Friction:** You cannot optimize just the "Database logic" without potentially confusing the "UI logic" residing in the same prompt. Also, the more tools a single agent has access to, the worse its decision-making becomes. The search space for its next action is simply too large, leading to hallucinated parameters or triggering the wrong tools.

<mark>**扩张摩擦：** 你没法只优化「数据库逻辑」，而不可能搅乱同一条提示词里的「界面逻辑」。而且，单个智能体能用的工具越多，决策就越差。下一步动作的搜索空间太大，就会幻觉出参数，或触发错误的工具。</mark>

- **Contextual Overload:** Shoving overarching system instructions, dozens of complex tool schemas, and ongoing conversation history into a single prompt quickly maxes out the model's working memory.

<mark>**上下文过载：** 把统领全局的系统指令、几十个复杂的工具 schema，以及进行中的对话历史，一股脑塞进同一条提示词，模型的工作记忆很快就会顶满。</mark>

- **The Single Point of Failure:** A bug in one "tool" or instruction can cause the entire agent to hallucinate or crash. Irrelevant or corrupted data stored in context gets carried over, breaking future reasoning.

<mark>**单点故障：** 一个「工具」或一条指令里的缺陷，就能让整个智能体幻觉或崩溃。上下文里无关或损坏的数据会被带下去，打断之后的推理 (Reasoning)。</mark>

To overcome these bottlenecks one can follow a similar blueprint laid out by ML engineers and software engineers years ago. When early AutoML models successfully proved their business value, teams rarely left those auto-generated black boxes running the core business. To reach production scale they had to break this black box apart into observable, maintainable stages—data versioning, feature stores, drift detection. By specializing the components they applied a fundamental law of system design: specialization as a scaling mechanism.

<mark>要越过这些瓶颈，可以沿用机器学习工程师和软件工程师多年前画出的那张蓝图。早期 AutoML 模型证明了商业价值之后，团队很少让那些自动生成的黑箱继续跑核心业务。要到生产规模，他们必须把黑箱拆成可观察、可维护的阶段：数据版本、特征库、漂移检测。把组件专门化，用的是系统设计的一条基本定律：专门化是一种扩张机制。</mark>

![Figure 3: Monolithic Multi-agent Architecture](2026/whitepaper-agent-tools-and-interoperability/images/image_006_page_19.png)

<mark>图 3：单体多智能体架构。同一个进程里，协调者带着自己的系统指令和工具，把任务分给多个专家。每个专家有自己的系统指令、工具子集和模型，但它们不跨网络边界通信。</mark>

Internal specialization works by logically partitioning a monolithic agent into distinct, purpose-built sub-agents. Each agent is governed by a highly focused system prompt and a relevant subset of tools. It is still monolith because these internal sub-agents do not communicate across network boundaries. Instead, they share the same runtime and underlying memory.

<mark>内部专门化的做法，是把一个单体智能体在逻辑上切成各司其职的子智能体。每个智能体由一条高度聚焦的系统提示词，以及相关的一组工具来约束。它仍然是单体，因为这些内部子智能体不跨网络边界通信。它们共享同一个运行时和底层记忆 (Memory)。</mark>

This logical partitioning allows developers to modularize complex definitions while maintaining the low-latency execution and simplified state management inherent to a single-process application. At the same time this modularity addresses the inherent limitations of single-agent systems through several key technical improvements:

<mark>这种逻辑切分让开发者把复杂定义模块化，同时保住单进程应用固有的低延迟执行和简化的状态管理。与此同时，这种模块化用几项关键的技术改进，补上单智能体系统的固有限制：</mark>

- **Reduction of Search Space:** By restricting a sub-agent's tools and skills (e.g., giving a DB agent only query tools), we drastically reduce tool-call errors and hallucinations.

<mark>**缩小搜索空间：** 限制子智能体的工具和技能 (Skills)（例如只给数据库智能体查询工具），工具调用错误和幻觉会大幅下降。</mark>

- **Mitigation of Attention Dilution:** Specialization allows the underlying LLM to focus on a single domain prompt, leading to sharper reasoning.

<mark>**减轻注意力稀释：** 专门化让底层大语言模型 (LLM) 专注于一条领域提示词，推理更锐利。</mark>

- **Optimization of Contextual Load:** Because the orchestrator routes tasks instead of processing the entire logic tree, sub-agents maintain a high signal-to-noise ratio in their context windows.

<mark>**优化上下文负载：** 编排者 (Orchestrator) 负责路由任务，而不是自己处理整棵逻辑树，子智能体的上下文窗口因此保持较高的信噪比。</mark>

As agentic architectures mature, a significant ecosystem shift based on distributed multi-agent architectures is underway. Industry leaders—including Google, Salesforce, ServiceNow, and Workday—are moving beyond the provision of APIs. These organizations are deploying domain-specific AI agents designed to navigate their proprietary ecosystems with native precision.

<mark>随着智能体架构成熟，一场基于分布式多智能体架构的生态转移正在发生。行业领先者，包括 Google、Salesforce、ServiceNow 和 Workday，正在越过「只提供 API」这一步。这些组织在部署领域专用的 AI 智能体，让它们以原生精度在各自的专有生态里穿行。</mark>

![Figure 4: Distributed Multi-Agent Architecture](image_007_page_21.png)

<mark>图 4：分布式多智能体架构。编排者经互联网或内网，把任务委派给网络边界另一侧的远程领域智能体。每个专家可以由不同的框架、语言和团队或产品来实现。</mark>

This shift presents a strategic opportunity for developers. However, to reach the next tier of scale, technical and business leaders must ruthlessly prioritize their focus through a modern "Build vs. Buy" lens.

<mark>这次转移给开发者一个战略机会。但要上到下一档规模，技术和业务负责人必须用现代的「自建还是外购」(Build vs. Buy) 视角，狠心地排定重心。</mark>

While it is technically feasible to construct a multi-agent system using custom-built sub-agents for third-party platforms (e.g. custom subagent for ServiceNow or custom subagent for Salesforce etc), this approach introduces a significant Maintenance Tax. By opting for bespoke development of domain specialists, the developer assumes full responsibility for updating prompt logic and tool definitions reflecting upstream product updates and API schema changes.

<mark>用自建子智能体去对接第三方平台，技术上做得到（例如为 ServiceNow 写一个定制子智能体，或为 Salesforce 写一个）。但这样做会带上一笔可观的维护税 (Maintenance Tax)。选择自己开发领域专家，开发者就要全权负责更新提示词逻辑和工具定义，以跟上上游产品更新和 API schema 变化。</mark>

A better architectural strategy for building high-value applications would be to leverage official specialist agents. These agents are maintained by teams with deep domain expertise, ensuring maximum reliability and performance. By offloading the maintenance of specialist domain logic to these official entities, the Orchestrator—and by extension, the developers—can focus entirely on the unique user value and core innovation of their application.

<mark>构建高价值应用时，更好的架构策略是使用官方专家智能体。这些智能体由具备深厚领域经验的团队维护，可靠性和性能都尽量拉满。把专家领域逻辑的维护交给这些官方主体之后，编排者，以及站在它背后的开发者，就可以把全部注意力放在应用独有的用户价值和核心创新上。</mark>

However, attempting to orchestrate this virtual team of distributed AI specialists introduces a new bottleneck: fragmentation. Every one of these specialist agents can be built by a different team, using different technologies. Google’s agent might be written in Python, Go or Java using ADK, Salesforce’s agent might run on a LangChain framework, and Workday’s might use something completely bespoke. They exist outside our network boundaries, they speak different languages, expect completely different payload structures, process conversational state differently, and rely on varying transport layers.

<mark>可是，要编排这支由分布式 AI 专家组成的虚拟团队，会冒出一个新瓶颈：碎片化。每一个专家智能体都可能由不同团队、用不同技术造出来。Google 的智能体可能用智能体开发套件 (Agent Development Kit, ADK)，以 Python、Go 或 Java 写成；Salesforce 的智能体可能跑在 LangChain 上；Workday 的可能完全是定制的。它们处在我们的网络边界之外，说不同的语言，期望完全不同的载荷结构，以不同方式处理对话状态，并依赖不同的传输层。</mark>

If a developer has to write custom integration code and handle bespoke error-correction loops for every single specialist they want to hire, the "Virtual Team" concept instantly turns into an integration endeavor. The maintenance tax of keeping all those custom bridges from collapsing would consume the entire project.

<mark>如果开发者每「雇用」一个专家，都要写定制集成代码，并处理专用的纠错循环，「虚拟团队」立刻就变成一项集成工程。为了不让那些定制桥梁坍塌而付出的维护税，会吃掉整个项目。</mark>

This chaos of fragmentation is exactly what the Agent-to-Agent (A2A) protocol [A2A] is designed to standardize. A2A, originally developed by Google and now donated to the Linux Foundation, introduces a universal layer of communication for agentic systems. It acts as the lingua franca for the AI ecosystem, abstracting away networking transport nuances, the underlying frameworks, programming languages, and payload disparities.

<mark>碎片化造成的这种混乱，正是 A2A 协议 [A2A] 要标准化的东西。A2A 最初由 Google 开发，现已捐赠给 Linux Foundation。它为智能体系统 (Agentic System) 引入一层通用通信。它是 AI 生态的通用语，把网络传输的细节、底层框架、编程语言和载荷差异都抽象掉。</mark>

It ensures that the central Orchestrator can discover, onboard, and collaborate with any specialist agent in the ecosystem, completely agnostic to how that specialist was built under the hood. Just as HTTP standardized the web, A2A standardizes the virtual workforce.

<mark>它保证中心编排者能够发现、接入并与生态里的任何专家智能体协作，完全不必在意这个专家底层是怎么造的。正如 HTTP 标准化了 Web，A2A 标准化了虚拟劳动力。</mark>

---

> "Does the caller need a result, or does the caller need another participant to take responsibility?" — that's the cleanest framing I've seen for this decision. The smell test of a central agent prompt growing into an accidental workflow engine is exactly how most teams discover they needed collaboration semantics three months too late.<sup>19</sup>

<mark>「调用方需要的是一个结果，还是需要另一个参与者来承担责任？」这是我见过的、对这个决定最干净的表述。中心智能体的提示词渐渐长成一台意外的工作流引擎，这种异味检验，正是大多数团队发现自己需要协作语义的方式，而且总是晚了三个月。<sup>19</sup></mark>

But this raises the next architectural question: If we are just delegating to external specialists, why can't we just treat them as standard tools?

<mark>这就引出下一个架构问题：如果我们只是委派给外部专家，为什么不能把它们当成标准工具？</mark>

The nature of the engagement with specialists and tools is fundamentally different. Imagine a homeowner renovating a kitchen. They face a choice: purchase the individual tools and manuals to attempt the build themselves, or delegate the project to a domain specialist who builds kitchens for a living.

<mark>与专家打交道，和与工具打交道，性质根本不同。想象一位房主在翻新厨房。他面临选择：买齐工具和手册自己干，还是把项目交给以造厨房为业的领域专家。</mark>

Tools are just passive instruments; a specialist is a collaborative partner. When you hire that specialist, you don't just hand them a single blueprint and walk away expecting a perfect kitchen to magically appear. They will hit edge cases or an oversight in your original design requiring them to pause, consult you on trade-offs, and resume.

<mark>工具只是被动的器具；专家是协作伙伴。你雇了这位专家，不会只递一张蓝图就走开，指望完美的厨房凭空出现。他们会撞上边界情况，或你原设计里的疏漏，于是停下来，就取舍征询你，然后再继续。</mark>

---

## Bounded vs. Unbounded Domains

<mark>有界领域与无界领域</mark>

This is exactly one of the reasons why treating a specialist AI agent as a simple tool does not scale. A standard tool or API operates on a fire-and-forget mechanism. It expects a single, perfectly formatted request (the blueprint payload) and returns a response. Real-world software environments often contain the digital equivalent of crooked walls: ambiguous data structures, misleading requirements, and conflicting user preferences.

<mark>这正是不能把专家 AI 智能体当成简单工具来扩展的原因之一。标准工具或 API 按「发出即忘」工作。它期望一次格式完美的请求（那张蓝图载荷），然后返回响应。真实的软件环境里常常有数字版的歪墙：含糊的数据结构、误导性的需求，以及互相冲突的用户偏好。</mark>

An agent, however, operates in an unbounded problem-solving space. Real-world software environments are full of ambiguous data structures, misleading requirements, and conflicting user preferences. You rarely can specify all necessary details in a complex workflow without multi-turn clarification. The digital equivalent of crooked walls.

<mark>智能体则在一个无界的解题空间里工作。真实的软件环境充满含糊的数据结构、误导性的需求和互相冲突的用户偏好。复杂工作流里，你很少能在没有多轮澄清的情况下写全所有必要细节。这就是数字版的歪墙。</mark>

---

## The GOTO Problem in Agentic Architecture

<mark>智能体架构里的 GOTO 问题</mark>

Because an agent's domain is unbounded, trying to force an agent into a standard tool wrapper introduces the architectural equivalent of a GOTO statement into your orchestrator.

<mark>因为智能体的领域是无界的，硬把它塞进标准工具包装器，等于往编排者里引入架构意义上的 GOTO 语句。</mark>

When you call a collaborative agent, the control flow leaves the expected, structured context. The agent might hit an interrupted state, request more information, and potentially never return the expected output to the original caller if the user changes their mind or abandons the prompt.

<mark>你调用一个协作型智能体时，控制流会离开预期中的结构化上下文。智能体可能进入中断状态，要求更多信息；如果用户改了主意或放弃了提示，它还可能永远不把预期输出交还给原来的调用方。</mark>

You need a paradigm that isolates this messy, multi-turn state. You need a protocol that allows the domain agent to pause its execution, reach back out to the Orchestrator, negotiate a solution, and then resume its work without losing its conversational state.

<mark>你需要一种范式，把这种凌乱的多轮状态隔离开。你需要一种协议，让领域智能体暂停执行，回头找到编排者，协商出一个解，然后在不丢失对话状态的情况下继续自己的工作。</mark>

That is exactly the gap the A2A protocol fills. By isolating this collaborative routing to the A2A layer, we keep the tool layer (MCP) clean, predictable, and strictly structured.

<mark>这正是 A2A 协议填上的缺口。把这种协作式路由隔离到 A2A 层，工具层（MCP）就能保持干净、可预期、严格结构化。</mark>

---

## Building the Virtual Workforce

<mark>组建虚拟劳动力</mark>

The introduction of the A2A protocol and the shift toward specialization does more than just solve technical bottlenecks—it creates the foundations for new marketplaces for expertise which represents a new model in how value is delivered.

<mark>引入 A2A 协议、转向专门化，解决的不只是技术瓶颈。它为新的专业能力市场打下基础，这是价值交付方式的一种新模型。</mark>

Without A2A, a developer might build an application and struggle to maintain its growing complexity. In the A2A era, that same developer can focus on perfecting a high-value niche—such as an agent that specializes in "Real-time Regulatory Compliance". Whether built as a sophisticated multi-agent monolith or a distributed app, these systems can now be exposed to the world as A2A-compliant agents. This means that a specialist vibe coded in one part of the world can be discovered and "hired" by another Orchestrator across the globe.

<mark>没有 A2A，开发者造出一个应用之后，会疲于维护不断增长的复杂度。在 A2A 时代，同一位开发者可以专注打磨一个高价值的缝隙，例如专门做「实时监管合规」的智能体。无论它是精巧的多智能体单体，还是分布式应用，这些系统现在都可以作为符合 A2A 的智能体暴露给世界。这意味着，在世界一角用氛围编码做出的专家，可以被地球另一边的编排者发现并「雇用」。</mark>

---

## The Agent Card

<mark>智能体名片</mark>

To facilitate this discovery, every agent is defined by an Agent Card. This is the standardized "CV" of the AI world, providing a machine-readable identity that outlines:

<mark>为了让这种发现发生，每个智能体都由一张智能体名片 (Agent Card) 来定义。它是 AI 世界里标准化的「简历」，提供一份机器可读的身份，写明：</mark>

- **Capabilities:** What tasks the agent can perform.

<mark>**能力：** 这个智能体能做哪些任务。</mark>

- **Security & Compliance:** Its data handling policies and permission requirements.

<mark>**安全与合规：** 它的数据处理政策和权限要求。</mark>

- **Interaction Schemas:** How other agents should communicate with it via the A2A protocol.

<mark>**交互 schema：** 其他智能体应如何经由 A2A 协议与它通信。</mark>

---

## Registries: From Public Marketplaces to Private Enterprises

<mark>注册表：从公开市场到企业内部</mark>

Once an agent is equipped with its Agent Card, it can be registered within an [Agent Registry](https://docs.cloud.google.com/agent-registry/register-agents) whose goal is to turn Agents into discoverable services. This offers two primary paths for developers:

<mark>智能体配上名片之后，就可以登记进[智能体注册表 (Agent Registry)](https://docs.cloud.google.com/agent-registry/register-agents)。注册表的目标是把智能体变成可发现的服务。开发者有两条主要路径：</mark>

1. **Public Registries (Marketplaces):** Like a global talent agency, public registries allow developers to list their specialist agents for the world to find. This paves the way for building specialist agents for a specific industry and licensing its expertise to thousands of other orchestrators.

<mark>1. **公开注册表（市场）：** 像一家全球人才机构，公开注册表让开发者把自己的专家智能体列出来，供全世界寻找。这就铺平了一条路：为某个行业打造专家智能体，再把它的专业能力授权给成千上万的其他编排者。</mark>

2. **Private Registries:** Within the enterprise, Agent Registries provide a secure, governed environment. Developers inside a large corporation can build a specialist agent that automates an internal workflow and register it for use by other departments, ensuring that expertise is shared across corporate boundaries without compromising security.

<mark>2. **私有注册表：** 在企业内部，智能体注册表提供安全、受治理的环境。大公司里的开发者可以造一个自动化内部工作流的专家智能体，登记给其他部门使用，让专业能力跨过公司内部边界共享，同时不牺牲安全。</mark>

Ultimately, the A2A protocol transforms the act of building isolated agentic applications into building the foundational members of a global, interoperable digital workforce.

<mark>最终，A2A 协议把「建造孤立的智能体应用」变成「建造一支全球可互操作的数字劳动力的基础成员」。</mark>

---

## Implementing A2A Protocols

<mark>实现 A2A 协议</mark>

The practical implementation of the A2A architecture enables two distinct development motions:

<mark>A2A 架构的实际实现，打开两种不同的开发动作：</mark>

- exposing AI agent as A2A agent (the supply side)

<mark>把 AI 智能体暴露为 A2A 智能体（供给侧）</mark>

- orchestrating remote A2A agents (the demand side)

<mark>编排远程 A2A 智能体（需求侧）</mark>

### Exposing A2A Agent

<mark>把智能体暴露为 A2A 智能体</mark>

Packaging an agent for the A2A ecosystem involves three core steps:

<mark>把一个智能体打包进 A2A 生态，有三个核心步骤：</mark>

- **Defining the Agent Card:** Formal agent specification.

<mark>**定义智能体名片：** 正式的智能体规格。</mark>

- **Implementing the Agent Executor (The Translation Layer):** It translates incoming A2A requests and responses into the specific calls required by the underlying agentic frameworks (e.g., ADK, LangGraph, or bespoke enterprise code).

<mark>**实现智能体执行器（翻译层）：** 它把进来的 A2A 请求和响应，翻译成底层智能体框架所需的具体调用（例如 ADK、LangGraph，或定制的企业代码）。</mark>

- **Establishing the A2A Endpoint:** Executor must be exposed as an A2A-compliant endpoint.

<mark>**建立 A2A 端点：** 执行器必须暴露为一个符合 A2A 的端点。</mark>

![Figure 5: Supply-side exposure and demand-side consumption](2026/whitepaper-agent-tools-and-interoperability/images/image_008_page_27.png)

<mark>图 5：供给侧把原生 AI 智能体暴露为 A2A 服务器，需求侧通过 A2A 客户端消费它。智能体坐在 A2A 执行器里，执行器接到 A2A 服务器，再与 A2A 客户端相连。</mark>

### Connecting Remote A2A Agents

<mark>连接远程 A2A 智能体</mark>

In a mature ecosystem, an application does not natively possess deep knowledge of every domain it touches. Instead, it acts as an Orchestrator—a central hub whose primary cognitive load is dedicated to understanding user intent, managing the overarching workflow, and delegating specific tasks to specialized, remote A2A agents.

<mark>在成熟的生态里，一个应用并不会天生就深知它触及的每一个领域。它充当编排者：一个中心枢纽，主要的认知负荷用来理解用户意图、管理总工作流，并把具体任务委派给专门的远程 A2A 智能体。</mark>

Remote A2A agents operate as an autonomous, domain-bound contractor which communicates over the A2A protocol. Connecting to these remote agents generally follows one of two architectural patterns (code sample from Google ADK): direct point-to-point integration:

<mark>远程 A2A 智能体像一个自主的、受领域约束的承包商，通过 A2A 协议通信。连接这些远程智能体，通常遵循两种架构模式之一（代码样例来自 Google ADK）。一种是直接的点对点集成：</mark>

**Snippet 2: Direct remote A2A agent instantiation via a hardcoded endpoint.**

<mark>代码片段 2：通过写死的端点，直接实例化远程 A2A 智能体。</mark>

```python
# 1. Direct Instantiation via Hardcoded Endpoint
# Ideal for specific vendor integrations or private agents
billing_specialist = RemoteA2aAgent(
    name="billing_agent",
    endpoint="https://api.vendor.com/v1/billing/a2a"
)
```

or by using agent registry to discover agents:

<mark>另一种是用智能体注册表来发现智能体：</mark>

**Snippet 3: Indirect remote A2A agent discovery and instantiation via an Agent Registry.**

<mark>代码片段 3：经由智能体注册表，间接发现并实例化远程 A2A 智能体。</mark>

```python
# 2. InDirect Instantiation via Agent Registry
registry = AgentRegistry(project_id=project_id, location=location)
#The registry resolves resource names and handles authentication validation
agent_name = f"projects/{project_id}/locations/{location}/agents/YOUR_AGENT_ID"
my_remote_agent = registry.get_remote_a2a_agent(agent_name=agent_name)
```

---

## The Extensibility Layer: A2A as the Foundation for UI and Commerce

<mark>扩展层：A2A 作为界面与商务的基础</mark>

By resolving the fragmentation inherent in the early AI ecosystem, A2A protocol establishes a unified communication layer which in turn enables developers to build atop this standardized substrate. While the core A2A protocol functions as a transport and negotiation backbone, realizing rich, transactional applications very often demand highly specialized capabilities.

<mark>A2A 协议化解了早期 AI 生态固有的碎片化，建立起统一的通信层，开发者因而可以在这块标准化基底上继续建造。核心 A2A 协议是传输与协商的骨干，但要做出丰富的、带交易的应用，往往需要高度专门的能力。</mark>

This requirement is addressed through the mechanism of [A2A Extensions](https://a2a-protocol.org/latest/topics/extensions/).<sup>1</sup> It provides a standardized pattern for agents to securely advertise, negotiate, and execute optional, higher-order functionalities that transcend basic message passing.

<mark>这个要求由 [A2A 扩展 (A2A Extensions)](https://a2a-protocol.org/latest/topics/extensions/) 来满足。<sup>1</sup> 它提供一套标准化模式，让智能体能够安全地宣告、协商并执行可选的、更高阶的功能，这些功能超出基本的消息传递。</mark>

Three foundational frameworks that operate as native extensions atop the core A2A foundation include the Agent-to-User Interface (A2UI), designed to generate dynamic, stateful user experiences; the Universal Commerce Protocol (UCP), engineered to facilitate secure, autonomous agentic commerce; and the Agent Payments Protocol (AP2) which lays the groundwork for trusted, verifiable agentic payments. All three are discussed in more detail in the following sections.

<mark>有三个基础框架作为原生扩展，建在核心 A2A 之上：智能体到界面 (Agent-to-User Interface, A2UI)，用来生成动态、有状态的用户体验；通用商务协议 (Universal Commerce Protocol, UCP)，用来促成安全、自主的智能体商务；以及智能体支付协议 (Agent Payments Protocol, AP2)，为可信、可验证的智能体支付打底。三者都会在后面几节展开。</mark>

---

## Monetizing A2A Agents

<mark>让 A2A 智能体变现</mark>

Making an agent work is only half the battle; the other half is ensuring long-term commercial sustainability. Following the success of the Software-as-a-Service (SaaS) paradigm, the A2A protocol naturally enables an Agent-as-a-Service (AaaS) model. This allows specialized agents to be offered in a consumption-based model through various sales channels.

<mark>让智能体跑起来只是战役的一半；另一半是保证长期的商业可持续。顺着软件即服务 (SaaS) 范式的成功，A2A 协议自然引出智能体即服务 (Agent-as-a-Service, AaaS) 模型。专门的智能体可以按消费计费，经多种销售渠道提供。</mark>

One example is utilizing the Google Cloud Marketplace as a monetization engine. Independent agent/software vendors and developers can list their A2A agents on the marketplace to instantly leverage the existing base of Google Cloud enterprise customers. Customers can procure these specialists and at the same time utilize their existing GCP financial commitments. Win-win for everyone.

<mark>一个例子是把 Google Cloud Marketplace 当作变现引擎。独立的智能体或软件供应商和开发者，可以把 A2A 智能体列到市场上，立刻用上 Google Cloud 已有的企业客户基础。客户采购这些专家的同时，还能用上已有的 GCP 财务承诺。对各方都是双赢。</mark>

The marketplace infrastructure automatically handles the "hard part"—complex billing—by providing native support for hybrid pricing, such as the "Flat fee with usage" model. This allows vendors to charge a predictable base fee while monetizing compute or token-based overages.

<mark>市场基础设施自动处理「难的部分」，也就是复杂计费。它原生支持混合定价，例如「固定费用加用量」模型。供应商可以收一笔可预期的基础费，同时对计算或基于 token 的超额部分变现。</mark>

![Figure 6: The Agent-as-a-Service lifecycle](image_009_page_30.png)

<mark>图 6：智能体即服务 (AaaS) 的生命周期。独立软件供应商打磨智能体，放到 GCP 市场变现（商店、Google Cloud、订阅或用量、承诺消耗），部署到客户环境并由智能体注册表治理，再由 A2A 客户端消费：Gemini Enterprise 应用、人到智能体界面、智能体到智能体交互、作为专门子智能体的编排者智能体。</mark>

Agents registered in the Google Cloud Marketplace are directly accessible to Gemini Enterprise app users. Gemini Enterprise is an advanced agentic platform that brings the best of Google AI to every employee for every workflow. It empowers teams to discover, create, share, and run AI agents within a single secure environment. By integrating with Agent Registries and operating as a native A2A Client, the platform augments the human experience by giving employees access to a broad ecosystem of specialized workers. At the same time Gemini Enterprise is a clear example of both an Agent as a Service platform (via its Assistant API), and it is also a host for remote agents.

<mark>登记在 Google Cloud Marketplace 上的智能体，Gemini Enterprise 应用的用户可以直接使用。Gemini Enterprise 是一个高级智能体平台，把 Google AI 里最好的部分带到每位员工的每条工作流。它让团队在同一个安全环境里发现、创建、分享并运行 AI 智能体。平台与智能体注册表集成，并作为原生 A2A 客户端运行，让员工接触到一大片专门工作者的生态，从而增强人的体验。与此同时，Gemini Enterprise 既是一个智能体即服务平台（经由它的 Assistant API），也是远程智能体的宿主。</mark>

While cloud marketplaces and traditional payment gateways will handle the majority of Agent-as-a-Service (AaaS) billing, the A2A protocol also supports permissionless, machine-to-machine microtransactions for developers who want to avoid managing user accounts entirely.

<mark>云市场和传统支付网关会处理智能体即服务的大部分计费。A2A 协议还支持无需许可的、机器对机器的微交易，给那些完全不想管理用户账户的开发者。</mark>

By utilizing the A2A Extensions framework [A2AEXT], an agent's server can implement the x402 (or L402) standard. In this pattern, the server intercepts a request and if “unpaid” returns an HTTP 402 Payment Required status code, bundled with a machine-readable invoice. The calling agent executes the payment autonomously and retries the request with a cryptographic proof-of-payment token. This provides a standardized option for pay-per-call endpoints that require strictly stateless, automated billing.

<mark>利用 A2A 扩展框架 [A2AEXT]，智能体的服务器可以实现 x402（或 L402）标准。在这种模式里，服务器拦截请求；如果「未付款」，就返回 HTTP 402 Payment Required，并附上一张机器可读的账单。调用方智能体自主完成支付，再带着加密的付款证明令牌重试请求。这就给按次付费的端点一个标准化选项，这类端点要求严格无状态的自动计费。</mark>

---

## The Extensibility Layer: A2A as the Foundation for UI and Commerce

<mark>扩展层：A2A 作为界面与商务的基础</mark>

By resolving the fragmentation inherent in the early AI ecosystem, A2A protocol establishes a unified communication layer which in turn enables developers to build atop this standardized substrate. While the core A2A protocol functions as a transport and negotiation backbone, realizing rich, transactional applications very often demand highly specialized capabilities.

<mark>A2A 协议化解了早期 AI 生态固有的碎片化，建立起统一的通信层，开发者因而可以在这块标准化基底上继续建造。核心 A2A 协议是传输与协商的骨干，但要做出丰富的、带交易的应用，往往需要高度专门的能力。</mark>

This requirement is addressed through the mechanism of [A2A Extensions](https://a2a-protocol.org/latest/topics/extensions/) [A2AEXT]. It provides a standardized pattern for agents to securely advertise, negotiate, and execute optional, higher-order functionalities that transcend basic message passing.

<mark>这个要求由 [A2A 扩展](https://a2a-protocol.org/latest/topics/extensions/) [A2AEXT] 来满足。它提供一套标准化模式，让智能体能够安全地宣告、协商并执行可选的、更高阶的功能，这些功能超出基本的消息传递。</mark>

Two foundational frameworks that operate as native extensions atop the core A2A foundation include the Agent-to-User Interface (A2UI), designed to generate dynamic, stateful user experiences, and the Universal Commerce Protocol (UCP), engineered to facilitate secure, autonomous agentic commerce. Both are discussed in more detail in the following sections.

<mark>有两个基础框架作为原生扩展，建在核心 A2A 之上：智能体到界面 (A2UI)，用来生成动态、有状态的用户体验；以及通用商务协议 (UCP)，用来促成安全、自主的智能体商务。两者都会在后面几节展开。</mark>

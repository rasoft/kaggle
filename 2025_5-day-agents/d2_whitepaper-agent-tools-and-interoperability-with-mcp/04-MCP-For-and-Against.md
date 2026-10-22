# Model Context Protocol: For and Against

模型上下文协议：赞成与反对

MCP adds several significant new capabilities to the AI developer's toolbox. It also has some important limitations and drawbacks, particularly as its usage expands from the locally deployed, developer augmentation scenario to remotely deployed, enterprise integration applications. In this section we will look first at MCP's advantages and new capabilities; then we consider the pitfalls, shortcomings, challenges and risks MCP introduces.

MCP（模型上下文协议，Model Context Protocol）给 AI 开发者的工具箱增加了几项重要的新能力。它也有一些重要的局限和缺点，尤其是当用法从本地部署、增强开发者的场景，扩展到远程部署、企业集成应用的时候。本节先看 MCP 的优势和新能力，再看它引入的陷阱、短板、挑战和风险。

---

## Capabilities and Strategic Advantages

能力与战略优势

### Accelerating Development and Fostering a Reusable Ecosystem

加快开发，并培育可复用的生态

The most immediate benefit of MCP is in simplifying the integration process. MCP provides a common protocol for tool integration with LLM-based applications. This should help reduce the development cost, and therefore time to market, for new AI-driven features and solutions. MCP may also help foster a "plug-and-play" ecosystem where tools become reusable and shareable assets. Several public MCP server registries and marketplace have emerged already, which allow developers to discover, share, and contribute pre-built connectors. To avoid potential fragmentation of the MCP ecosystem, the MCP project recently launched the MCP Registry<sup>30</sup>, which provides both a central source of truth for public MCP servers, and also an OpenAPI specification to standardize MCP server declarations. If the MCP registry catches on, this may create network effects which could accelerate the growth of the AI tool ecosystem.

MCP 最直接的好处是简化集成过程。MCP 为大语言模型 (LLM) 应用的工具集成提供了一套公共协议。这应当有助于降低新的 AI 驱动功能与方案的开发成本，从而缩短上市时间。MCP 也可能帮助培育一个「即插即用」的生态，让工具 (Tools) 成为可复用、可共享的资产。若干公开的 MCP 服务器注册表和市场已经出现，开发者可以在其中发现、分享并贡献预制连接器。为避免 MCP 生态可能的碎片化，MCP 项目最近推出了 MCP Registry<sup>30</sup>，它既是公开 MCP 服务器的中心事实来源，也提供一份 OpenAPI 规范来标准化 MCP 服务器声明。如果 MCP 注册表流行起来，可能产生网络效应，加快 AI 工具生态的增长。

### Dynamically Enhancing Agent Capabilities and Autonomy

动态增强智能体的能力与自主性

MCP enhances agent function calling in several important ways.

MCP 从几个重要方面增强了智能体 (Agent) 的函数调用。

- Dynamic Tool Discovery: MCP-enabled applications can discover available tools at runtime instead of having those tools hard-coded, allowing for greater adaptability and autonomy.

动态工具发现：支持 MCP 的应用可以在运行时发现可用工具，而不必把这些工具硬编码进去，从而有更大的适应性和自主性。

- Standardizing and Structuring Tool Descriptions: MCP also expands on basic LLM function calling by providing a standard framework for tool descriptions and interface definitions.

标准化并结构化工具描述：MCP 还在基本的大语言模型函数调用之上扩展，为工具描述和接口定义提供一套标准框架。

- Expanding LLM Capabilities: Finally, by enabling the growth of an ecosystem of tool providers, MCP dramatically expands the capabilities and information available to LLMs.

扩展大语言模型的能力：最后，通过促成工具提供方生态的增长，MCP 大幅扩展了大语言模型可用的能力和信息。

### Architectural Flexibility and Future-Proofing

架构灵活性与面向未来

By standardizing the agent-tool interface, MCP decouples the agent's architecture from the implementation of its capabilities. This promotes a modular and composable system design, aligning with modern architectural paradigms like the "agentic AI mesh". In such an architecture, logic, memory, and tools are treated as independent, interchangeable components, making such systems easier to debug, upgrade, scale, and maintain over the long term. Such a modular architecture also allows an organization to switch underlying LLM providers or replace a backend service without needing to re-architect the entire integration layer, provided the new components are exposed via a compliant MCP server.

通过标准化智能体与工具的接口，MCP 把智能体的架构与其能力的实现解耦。这推动模块化、可组合的系统设计，与「智能体 AI 网格」(agentic AI mesh) 这类现代架构范式一致。在这种架构里，逻辑、记忆 (Memory) 和工具被当作独立、可互换的组件，使系统在长期内更容易调试、升级、扩展和维护。这种模块化架构也让组织可以切换底层大语言模型提供方，或替换后端服务，而不必重新设计整层集成，前提是新组件通过符合规范的 MCP 服务器暴露出来。

### Foundations for Governance and Control

治理与控制的基础

While MCP's native security features are currently limited (as detailed in the next section), its architecture does at least provide the necessary hooks for implementing more robust governance. For instance, security policies and access controls can be embedded within the MCP server, creating a single point of enforcement that ensures any connecting agent adheres to predefined rules. This allows an organization to control what data and actions are exposed to its AI agents.

MCP 的原生安全特性目前有限（详见下一节），但它的架构至少提供了实现更稳健治理所需的挂钩。例如，安全策略和访问控制可以嵌在 MCP 服务器里，形成单一的强制执行点，确保任何连接上来的智能体都遵守预定义规则。这让组织能够控制向其 AI 智能体暴露哪些数据和动作。

The Gemini Enterprise Agent Platform provides native infrastructure to enforce this governance. Central to this is the Agent Registry, a unified catalog for discovering and managing approved tools, MCP servers, and agent configurations across the enterprise. Pairing with this is Agent Identity, a system that assigns a unique, cryptographic ID to every individual agent. This guarantees complete traceability, verifiable auditing, and the ability to apply fine-grained access controls at the agent level, ensuring that any action taken via MCP is fully authorized.

Gemini 企业智能体平台 (Gemini Enterprise Agent Platform) 提供执行这套治理的原生基础设施。核心是智能体注册表 (Agent Registry)，一份在全企业范围内发现并管理已批准工具、MCP 服务器和智能体配置的统一目录。与之配套的是智能体身份 (Agent Identity)：为每一个智能体分配唯一的加密 ID。这保证了完整的可追溯性、可验证的审计，以及在智能体层面施加细粒度访问控制的能力，从而确保经 MCP 采取的任何动作都经过充分授权。

Furthermore, the protocol specification itself establishes a philosophical foundation for responsible AI by explicitly recommending user consent and control. The specification mandates that hosts should obtain explicit user approval before invoking any tool or sharing private data. This design principle promotes the implementation of "human-in-the-loop" workflows, where the agent can propose an action but must await human authorization before execution, providing a critical safety layer for autonomous systems.

此外，协议规范本身通过明确建议用户同意与控制，为负责任的 AI 建立了理念基础。规范要求宿主在调用任何工具或分享私有数据之前，应当获得用户的明确批准。这一设计原则推动实现「人在回路」(human-in-the-loop) 工作流：智能体可以提议一个动作，但执行前必须等待人类授权，从而为自主系统提供关键的安全层。

---

## Critical Risks and Challenges

关键风险与挑战

A key focus for enterprise developers adopting MCP is the need to layer in support for enterprise-level security requirements (authentication, authorization, user isolation, etc.). Security is such a critical topic for MCP that we dedicate a separate section of this whitepaper to it (see Section 5). In the remainder of this section, we will look at other considerations for deploying MCP in enterprise applications.

采用 MCP 的企业开发者有一个重点：需要分层补上企业级安全要求（认证、授权、用户隔离等）。安全对 MCP 如此关键，本文专门用一节来讨论（见第 5 节）。本节其余部分看在企业应用中部署 MCP 的其他考量。

### Performance and Scalability Bottlenecks

性能与可扩展性瓶颈

Beyond security, MCP's current design presents fundamental challenges to performance and scalability, primarily related to how it manages context and state.

除了安全，MCP 当前的设计对性能和可扩展性提出了根本挑战，主要与它管理上下文和状态的方式有关。

- Context Window Bloat: For an LLM to know which tools are available, the definitions and parameter schemas for every tool from every connected MCP server must be included in the model's context window. This metadata can consume a significant portion of the available token, resulting in increased cost and latency, and causing the loss of other critical context information.

上下文窗口膨胀 (Context Window Bloat)：要让大语言模型知道有哪些工具可用，每一个已连接 MCP 服务器上每一个工具的定义和参数模式，都必须放进模型的上下文窗口。这些元数据会吃掉可用 token 的很大一块，导致成本和延迟上升，并挤掉其他关键的上下文信息。

- Degraded Reasoning Quality: An overloaded context window can also degrade the quality of the AI's reasoning. With many tool definitions in a prompt, the model may have difficulty identifying the most relevant tool for a given task or may lose track of the user's original intent. This can lead to erratic behavior, such as ignoring a useful tool or invoking an irrelevant one, or ignoring other important information contained in the request context.

推理质量下降：过载的上下文窗口也会降低 AI 的推理 (Reasoning) 质量。提示里有许多工具定义时，模型可能难以为给定任务找出最相关的工具，或丢失用户的原始意图。这会导致不稳定的行为，例如忽略一个有用的工具、调用一个无关的工具，或忽略请求上下文里的其他重要信息。

- Stateful Protocol Challenges: Using stateful, persistent connections for remote servers can lead to more complex architectures that are harder to develop and maintain. Integrating these stateful connections with predominantly stateless REST APIs often requires developers to build and manage complex state-management layers, which can hinder horizontal scaling and load balancing.

有状态协议的挑战：对远程服务器使用有状态、持久的连接，会导致更复杂、更难开发和维护的架构。把这些有状态连接与以无状态为主的 REST API 集成，常常要求开发者构建并管理复杂的状态管理层，这会妨碍水平扩展和负载均衡。

The issue of context window bloat represents an emerging architectural challenge -- the current paradigm of pre-loading all tool definitions into the prompt is simple but does not scale. This reality may force a shift in how agents discover and utilize tools. One potential future architecture might involve a RAG-like approach for tool discovery itself.<sup>31</sup> An agent, when faced with a task, would first perform a "tool retrieval" step against a massive, indexed library of all possible tools to find the few most relevant ones. Based on that response, it would load the definitions for that small subset of tools into its context window for execution. This would transform tool discovery from a static, brute-force loading process into a dynamic, intelligent, and scalable search problem, creating a new and necessary layer in the agentic AI stack. Dynamic tool retrieval does, however, open another potential attack vector; if an attacker gains access to the retrieval index, he or she could inject a malicious tool schema into the index and trick the LLM into calling an unauthorized tool.

上下文窗口膨胀是一个正在出现的架构挑战：当前把全部工具定义预装进提示的范式很简单，但无法扩展。这一现实可能迫使智能体发现和使用工具的方式发生转变。一种可能的未来架构，是对工具发现本身采用类似检索增强生成 (RAG) 的方法。<sup>31</sup> 智能体面对一项任务时，先对所有可能工具的庞大索引库做一步「工具检索」，找出少数最相关的工具。根据这次响应，它再把这一小部分工具的定义载入上下文窗口去执行。这会把工具发现从静态、蛮力的装载过程，变成动态、智能、可扩展的搜索问题，并在智能体 AI 栈里增加一层新的、必要的层次。不过，动态工具检索也打开了另一条潜在的攻击路径：如果攻击者获得检索索引的访问权，就可以把恶意工具模式注入索引，诱使大语言模型调用未授权的工具。

### Enterprise Readiness Gaps

企业就绪程度的缺口

While MCP is rapidly being adopted, several critical enterprise-grade features are still evolving or not yet included in the core protocol, creating gaps that organizations must address themselves.

尽管 MCP 正在被迅速采用，若干关键的企业级特性仍在演进，或尚未纳入核心协议，由此形成组织必须自己补上的缺口。

- Authentication and Authorization: The initial MCP specification did not originally include a robust, enterprise-ready standard for authentication and authorization. While the specification is actively evolving, the current OAuth implementation has been noted to conflict with some modern enterprise security practices<sup>32</sup>.

认证与授权：最初的 MCP 规范原本没有包含稳健、达到企业就绪程度的认证与授权标准。规范正在积极演进，但当前的 OAuth 实现已被指出与一些现代企业安全实践相冲突<sup>32</sup>。

- Identity Management Ambiguity: The base MCP protocol does not natively standardize identity propagation, making it ambiguous whether an action is initiated by a user, an agent, or a system account. The Gemini Enterprise Agent Platform resolves this natively through Agent Identity, which assigns cryptographic, verifiable identities to agents, enabling strict accountability and fine-grained access control.

身份管理的含糊：基础 MCP 协议并不原生标准化身份传递，因此一个动作究竟由用户、智能体还是系统账户发起，是含糊的。Gemini 企业智能体平台通过智能体身份原生解决这一点：为智能体分配可加密验证的身份，从而实现严格的问责和细粒度访问控制。

- Lack of Native Observability: The base protocol does not define standards for observability primitives like logging, tracing, and metrics, essential capabilities for debugging, health monitoring and threat detection. To address this, enterprise software providers are building features on top of MCP with offerings like the Apigee API management platform, which adds a layer of observability and governance to MCP traffic. While MCP lacks built-in observability primitives, to help enterprise platforms fill this void, Google Cloud’s new Agent Observability suite provides OTel-compliant telemetry, detailed execution traces, and logging. Furthermore, Agent Simulation enables developers to stress-test agents at scale against synthetic traffic, ensuring reliability before deploying to production.

缺少原生可观测性：基础协议没有为日志、追踪和指标这类可观测性原语定义标准，而这些是调试、健康监测和威胁检测所必需的能力。为此，企业软件提供方正在 MCP 之上构建特性，例如 Apigee API 管理平台，它为 MCP 流量增加一层可观测性和治理。尽管 MCP 缺少内置的可观测性原语，为帮助企业平台填上这个空白，Google Cloud 新的智能体可观测性套件 (Agent Observability) 提供符合 OTel 的遥测、详细的执行追踪和日志。此外，智能体仿真 (Agent Simulation) 让开发者能针对合成流量大规模压力测试智能体，在部署到生产之前确认可靠性。

MCP was designed for open, decentralized innovation, which spurred its rapid growth, and in the local deployment scenario, this approach is successful. However, the most significant risks it presents—supply chain vulnerabilities, inconsistent security, data leakage, and a lack of observability—are all consequences of this decentralized model. As a result, major enterprise players are not adopting the "pure" protocol but are instead wrapping it in layers of centralized governance. These managed platforms impose the security, identity, and control that extend the base protocol.

MCP 是为开放、去中心化的创新而设计的，这推动了它的快速增长；在本地部署场景里，这种做法是成功的。然而，它呈现出的最显著风险——供应链漏洞、不一致的安全、数据泄露，以及缺少可观测性——都是这种去中心化模型的后果。因此，主要的企业参与者并不是在采用「纯」协议，而是用一层层集中治理把它包起来。这些托管平台施加了扩展基础协议的安全、身份和控制。

# Introduction: Models, Tools and Agents

引言：模型、工具与智能体

**Unifying Agents, Tools, and the World**

把智能体、工具与世界连成一体

---

Without access to external functions, even the most advanced foundation model<sup>1</sup> is just a pattern prediction engine. An advanced model can do many things well -- passing law exams<sup>2</sup>, writing code<sup>3</sup> or poetry<sup>4</sup>, creating images<sup>5</sup> and videos<sup>6</sup>, solving math problems<sup>7</sup> -- but on its own it can only generate content based on the data it was previously trained on. It can't access any new data about the world except what is fed into it in its request context; it can't interact with an external system; and it can't take any action to influence its environment.

如果不能调用外部函数，再先进的基础模型 (foundation model)<sup>1</sup> 也只是一台模式预测引擎。先进的模型 (Model) 能做好很多事：通过法律考试<sup>2</sup>、写代码<sup>3</sup>或诗<sup>4</sup>、生成图像<sup>5</sup>和视频<sup>6</sup>、解数学题<sup>7</sup>。但单靠自身，它只能根据先前训练过的数据生成内容。除了请求上下文里喂进去的东西，它接触不到关于世界的新数据；它不能与外部系统交互；也不能采取任何行动去影响所处的环境。

Most modern foundation models now have the capacity to call external functions, or tools, to address this limitation. Like apps on a smartphone, tools enable an AI system to do more than just generate patterns. These tools act as the agent's "eyes" and "hands," allowing it to perceive and act on the world.

如今大多数现代基础模型都能调用外部函数，也就是工具 (Tools)，用来补上这个缺口。工具像智能手机上的应用，让 AI 系统不只是生成模式。这些工具是智能体 (Agent) 的「眼睛」和「手」，让它能够感知世界，并对世界采取行动。

---

With the advent of Agentic AI, tools become even more important to AI systems. An AI Agent uses a foundation model's reasoning capability to interact with users and achieve specific goals for them, and external tools give the agent that capacity. With the capacity to take external actions, agents can have a dramatic impact on enterprise applications.<sup>8</sup>

智能体式 AI (Agentic AI) 出现之后，工具对 AI 系统更加重要。AI 智能体用基础模型的推理 (Reasoning) 能力与用户交互，并为用户达成具体目标；外部工具给了智能体这种能力。一旦能对外采取行动，智能体就会对企业应用产生剧烈影响。<sup>8</sup>

Connecting external tools to foundation models carries significant challenges, though, both basic technical issues as well as important security risks. The Model Context Protocol<sup>9</sup> was introduced in 2024 as a way to streamline the process of integrating tools and models, and address some of these technical and security challenges.

把外部工具接到基础模型上，挑战却不小：既有基本的技术问题，也有重要的安全风险。模型上下文协议 (Model Context Protocol, MCP)<sup>9</sup> 在 2024 年提出，用来简化工具与模型的集成，并应对其中一部分技术与安全挑战。

In this paper we talk first about the nature of tools used by foundation models: what they are and how to use them. We give some best practices and guidelines for designing effective tools and using them effectively. We then look at the Model Context Protocol, talking about its basic components and some of the challenges and risks it entails. Finally, we take a deeper look at the security challenges posed by MCP as it is introduced in an enterprise environment and connected to high-value external systems.

本文先谈基础模型所用工具的本质：它们是什么，以及怎么用。我们给出设计有效工具、并有效使用它们的若干最佳实践和准则。接着看模型上下文协议，谈它的基本组件，以及它带来的一部分挑战和风险。最后，我们更深入地看 MCP 进入企业环境、并连接到高价值外部系统时提出的安全挑战。

To facilitate this transition from AI experimentation to secure, production-scale agentic systems, Google Cloud has evolved Vertex AI into the Gemini Enterprise Agent Platform. This comprehensive, end-to-end platform is designed around four foundational pillars: Build, Scale, Govern, and Optimize. By providing native infrastructure for tool integration, state management, and strict enterprise security, the platform allows organizations to deploy robust autonomous agents with confidence.

为了推动从 AI 实验走向安全、生产规模的智能体系统 (Agentic System)，Google Cloud 已把 Vertex AI 演进为 Gemini 企业智能体平台 (Gemini Enterprise Agent Platform)。这个端到端的完整平台围绕四根支柱设计：构建 (Build)、扩展 (Scale)、治理 (Govern)、优化 (Optimize)。平台提供工具集成、状态管理和严格企业安全的原生基础设施，让组织能够有把握地部署稳健的自主智能体 (Autonomous Agent)。

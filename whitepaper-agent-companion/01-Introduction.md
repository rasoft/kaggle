# Introduction

<mark>引言</mark>

Generative AI agents mark a leap forward from traditional, standalone language models, offering a dynamic approach to problem-solving and interaction. As defined in the original Agents paper, an agent is an application engineered to achieve specific objectives by perceiving its environment and strategically acting upon it using the tools at its disposal. The fundamental principle of an agent lies in its synthesis of reasoning, logic, and access to external information, enabling it to perform tasks and make decisions beyond the inherent capabilities of the underlying model. These agents possess the capacity for autonomous operation, independently pursuing their goals and proactively determining subsequent actions, often without explicit instructions.

<mark>生成式 AI 智能体 (Agent) 相对传统的、独立运行的语言模型迈进了一大步，为解题和交互提供了一种动态方式。按照最初那篇《智能体》白皮书的定义，智能体是一种为达成特定目标而设计的应用：它感知环境，并用手头的工具 (Tools) 有策略地作用于环境。智能体的基本原则，是把推理 (Reasoning)、逻辑和对外部信息的访问合在一起，从而能完成底层模型凭自身做不到的任务和决策。这些智能体具备自主运行的能力，可以独立追求目标，并主动决定下一步动作，常常不需要明确指令。</mark>

> The future of AI is agentic.
>
> <mark>AI 的未来是智能体式的。</mark>

---

The architecture of an agent is composed of three essential elements that drive its behavior and decision-making:

<mark>智能体的架构由三个基本要素组成，它们驱动着智能体的行为与决策：</mark>

- **Model:** Within the agent's framework, the term "model" pertains to the language model (LM) that functions as the central decision-making unit, employing instruction-based reasoning and logical frameworks. The model can vary from general-purpose to multimodal or fine-tuned, depending on the agent's specific requirements.

<mark>- **模型 (Model)：** 在智能体的框架里，「模型」指作为中央决策单元的语言模型 (LM)。它采用基于指令的推理和逻辑框架。按智能体的具体要求，模型可以是通用的，也可以是多模态的，或经过微调的。</mark>

- **Tools:** Tools are critical for bridging the divide between the agent's internal capabilities and the external world, facilitating interaction with external data and services. These tools empower agents to access and process real-world information. Tools can include extensions, functions, and data stores. Extensions bridge the gap between an API and an agent, enabling agents to seamlessly execute APIs. Functions are self-contained modules of code that accomplish specific tasks. Data stores provide access to dynamic and up-to-date information, ensuring a model’s responses remain grounded in factuality and relevance.

<mark>- **工具 (Tools)：** 工具用来填平智能体内部能力与外部世界之间的鸿沟，让智能体能与外部数据和服务交互。这些工具使智能体能够访问并处理现实世界的信息。工具可以包括扩展 (Extension)、函数 (Function) 和数据存储 (Data Store)。扩展把 API 和智能体接起来，让智能体能顺畅地执行 API。函数是完成特定任务的自包含代码模块。数据存储提供动态、最新的信息，使模型的回答保持在事实和相关性上有依据。</mark>

- **Orchestration layer:** The orchestration layer is a cyclical process that dictates how the agent assimilates information, engages in internal reasoning, and leverages that reasoning to inform its subsequent action or decision. This layer is responsible for maintaining memory, state, reasoning, and planning. It employs prompt engineering frameworks to steer reasoning and planning, facilitating more effective interaction with the environment and task completion. Reasoning techniques such as ReAct, Chain-of-Thought (CoT), and Tree-of-Thoughts (ToT) can be applied within this layer.

<mark>- **编排层 (Orchestration Layer)：** 编排层是一个循环过程，规定智能体如何吸收信息、进行内部推理，并借助这些推理决定下一步行动或决策。这一层负责维护记忆 (Memory)、状态、推理和规划 (Planning)。它用提示工程框架来引导推理和规划，从而更有效地与环境交互、完成任务。ReAct、思维链 (Chain-of-Thought, CoT) 和思维树 (Tree-of-Thoughts, ToT) 等推理技术都可以用在这一层。</mark>

---

Building on these foundational concepts, this companion paper is designed for developers and serves as a "102" guide to more advanced topics. It offers in-depth explorations of agent evaluation methodologies and practical applications of Google agent products for enhancing agent capabilities in solving complex, real-world problems.

<mark>在这些基础概念之上，这份伴读面向开发者，相当于进阶主题的「102」指南。它深入讨论智能体评估方法，以及 Google 智能体产品的实际用法，用来增强智能体解决复杂现实问题的能力。</mark>

While exploring these theoretical concepts, we'll examine how they manifest in real-world implementations, with a particular focus on automotive AI as a compelling case study. The automotive domain exemplifies the challenges and opportunities of multi-agent architectures in production environments. Modern vehicles demand conversational interfaces that function with or without connectivity, balance between on-device and cloud processing for both safety and user experience, and seamlessly coordinate specialized capabilities across navigation, media control, messaging, and vehicle systems. Through this automotive lens, we'll see how different coordination patterns — hierarchical, collaborative, and peer-to-peer — come together to create robust, responsive user experiences in environments with significant constraints. This case study illustrates the practical application of multi-agent systems that businesses across industries can adapt to their specific domains.

<mark>在展开这些理论概念时，我们会看它们如何落在真实实现里，并以汽车 AI 作为一个有说服力的案例。汽车领域集中体现了生产环境中多智能体架构的挑战与机会。现代车辆需要的对话界面，在有网和没网时都要能用；为了安全和体验，要在端侧处理与云端处理之间取得平衡；还要在导航、媒体控制、消息和车辆系统之间无缝协调各项专用能力。透过这个汽车视角，我们会看到层级、协作和对等这几种协调模式如何组合起来，在约束很强的环境里做出稳健、响应及时的用户体验。这个案例说明，多智能体系统可以怎样被各行业的企业改造成适合自己领域的做法。</mark>

Anyone who has built with gen AI quickly realizes it’s easy to get from an idea to a proof-of-concept, but it can be quite difficult to ensure high quality results and get to production — gen AI agents are no exception. Quality and Reliability are the most cited concerns for deploying to production, and the “AgentOps” process is a solution to optimize agent building.

<mark>凡是用生成式 AI 做过东西的人很快都会发现：从想法走到概念验证很容易，要保证高质量结果并进入生产却相当难。生成式 AI 智能体也不例外。质量和可靠性是部署到生产时被提到最多的顾虑，「智能体运维 (AgentOps)」流程就是用来优化智能体构建的一种办法。</mark>

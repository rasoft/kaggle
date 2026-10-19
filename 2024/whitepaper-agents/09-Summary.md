# Summary

<mark>总结</mark>

In this whitepaper we’ve discussed the foundational building blocks of Generative AI agents, their compositions, and effective ways to implement them in the form of cognitive architectures. Some key takeaways from this whitepaper include:

<mark>本白皮书讨论了生成式 AI (Generative AI) 智能体 (Agent) 的基础构件、它们如何组成，以及以认知架构 (Cognitive Architecture) 的形式有效实现它们的方式。要点如下：</mark>

1. Agents extend the capabilities of language models by leveraging tools to access real-time information, suggest real-world actions, and plan and execute complex tasks autonomously. Agents can leverage one or more language models to decide when and how to transition through states and use external tools to complete any number of complex tasks that would be difficult or impossible for the model to complete on its own.
2. At the heart of an agent’s operation is the orchestration layer, a cognitive architecture that structures reasoning, planning, decision-making and guides its actions. Various reasoning techniques such as ReAct, Chain-of-Thought, and Tree-of-Thoughts, provide a framework for the orchestration layer to take in information, perform internal reasoning, and generate informed decisions or responses.
3. Tools, such as Extensions, Functions, and Data Stores, serve as the keys to the outside world for agents, allowing them to interact with external systems and access knowledge beyond their training data. Extensions provide a bridge between agents and external APIs, enabling the execution of API calls and retrieval of real-time information. Functions provide a more nuanced control for the developer through the division of labor, allowing agents to generate Function parameters which can be executed client-side. Data Stores provide agents with access to structured or unstructured data, enabling data-driven applications.

<mark>1. 智能体借助工具 (Tools) 扩展语言模型的能力：访问实时信息、建议现实世界中的动作，并自主地规划 (Planning) 和执行复杂任务。智能体可以利用一个或多个语言模型，决定何时以及如何在状态之间转移，并使用外部工具去完成模型独自很难或无法完成的任意数量的复杂任务。</mark>

<mark>2. 智能体运作的核心是编排层 (Orchestration Layer)，一种组织推理 (Reasoning)、规划、决策并引导其行动的认知架构。ReAct、思维链 (Chain-of-Thought) 和思维树 (Tree-of-Thoughts) 等多种推理技术，为编排层提供了框架：接收信息、进行内部推理，并生成有依据的决策或响应。</mark>

<mark>3. 扩展 (Extensions)、函数 (Functions) 和数据存储 (Data Stores) 这类工具，是智能体通往外部世界的钥匙，使它们能与外部系统交互，并访问训练数据之外的知识。扩展在智能体与外部 API 之间架起桥梁，使 API 调用得以执行，实时信息得以取回。函数通过分工，给开发者更细致的控制：智能体生成函数参数，再在客户端执行。数据存储让智能体访问结构化或非结构化数据，从而支撑数据驱动的应用。</mark>

The future of agents holds exciting advancements and we’ve only begun to scratch the surface of what is possible. As tools become more sophisticated and reasoning capabilities are enhanced, agents will be empowered to solve increasingly complex problems. Furthermore, the strategic approach of ‘agent chaining’ will continue to gain momentum. By combining specialized agents - each excelling in a particular domain or task - we can create a ‘mixture of agent experts’ approach, capable of delivering exceptional results across various industries and problem areas.

<mark>智能体的未来会有令人兴奋的进展，我们才刚刚触及可能之事的表层。随着工具更精密、推理能力更强，智能体将有能力解决越来越复杂的问题。此外，「智能体链接 (agent chaining)」这一策略性做法会继续获得势头。把各有所长的专门智能体组合起来——每一个都在某个领域或任务上出色——就可以形成一种「智能体专家混合 (mixture of agent experts)」的做法，能够在不同行业和问题领域交出出色的结果。</mark>

It’s important to remember that building complex agent architectures demands an iterative approach. Experimentation and refinement are key to finding solutions for specific business cases and organizational needs. No two agents are created alike due to the generative nature of the foundational models that underpin their architecture. However, by harnessing the strengths of each of these foundational components, we can create impactful applications that extend the capabilities of language models and drive real-world value.

<mark>要记住：构建复杂的智能体架构需要迭代的做法。实验和打磨，是为具体业务场景和组织需要找到方案的关键。由于支撑其架构的基础模型 (foundational model) 具有生成性，没有两个智能体是一模一样的。不过，用好这些基础组件各自的长处，我们就能做出有影响力的应用，延伸语言模型的能力，并带来现实世界的价值。</mark>

# What is an agent?

<mark>什么是智能体？</mark>

In its most fundamental form, a Generative AI agent can be defined as an application that attempts to achieve a goal by observing the world and acting upon it using the tools that it has at its disposal. Agents are autonomous and can act independently of human intervention, especially when provided with proper goals or objectives they are meant to achieve. Agents can also be proactive in their approach to reaching their goals. Even in the absence of explicit instruction sets from a human, an agent can reason about what it should do next to achieve its ultimate goal. While the notion of agents in AI is quite general and powerful, this whitepaper focuses on the specific types of agents that Generative AI models are capable of building at the time of publication.

<mark>最基本地说，生成式 AI (Generative AI) 智能体 (Agent) 可以定义成这样一种应用：它观察世界，并用手头的工具 (Tools) 对世界采取行动，以此设法达成一个目标。智能体是自主的，尤其是在给出了应当达成的目标之后，它可以不依赖人的介入而行动。智能体追求目标时也可以是主动的。即便人没有给出明确的指令集，智能体也能推理 (Reason) 下一步该做什么，才能走向最终目标。AI 里的智能体概念相当宽泛，也很有力。本白皮书只讨论出版时生成式 AI 模型能够构建的那一类智能体。</mark>

In order to understand the inner workings of an agent, let’s first introduce the foundational components that drive the agent’s behavior, actions, and decision making. The combination of these components can be described as a cognitive architecture, and there are many such architectures that can be achieved by the mixing and matching of these components. Focusing on the core functionalities, there are three essential components in an agent’s cognitive architecture as shown in Figure 1.

<mark>要理解智能体内部如何运作，先看驱动它的行为、行动和决策的基础组件。这些组件合在一起，可以称为认知架构 (Cognitive Architecture)。把这些组件以不同方式搭配，就能得到许多种架构。就核心功能而言，智能体的认知架构有三个必要组件，如图 1 所示。</mark>

![General agent architecture: orchestration, model, and tools inside the agent runtime](2025_5-day-genai/d3_whitepaper-agents/images/image_001_page_6.png)

<mark>图 1：智能体的一般架构与组件。用户查询进入智能体运行时；编排层包含画像、目标与指令，短期与长期记忆，以及基于模型的推理 / 规划；旁边是模型与工具；智能体响应返回给用户。</mark>

---

## The model

<mark>模型</mark>

In the scope of an agent, a model refers to the language model (LM) that will be utilized as the centralized decision maker for agent processes. The model used by an agent can be one or multiple LM’s of any size (small / large) that are capable of following instruction based reasoning and logic frameworks, like ReAct, Chain-of-Thought, or Tree-of-Thoughts. Models can be general purpose, multimodal or fine-tuned based on the needs of your specific agent architecture. For best production results, you should leverage a model that best fits your desired end application and, ideally, has been trained on data signatures associated with the tools that you plan to use in the cognitive architecture. It’s important to note that the model is typically not trained with the specific configuration settings (i.e. tool choices, orchestration/reasoning setup) of the agent. However, it’s possible to further refine the model for the agent’s tasks by providing it with examples that showcase the agent’s capabilities, including instances of the agent using specific tools or reasoning steps in various contexts.

<mark>在智能体的范围内，模型 (Model) 指的是充当智能体流程中心决策者的语言模型 (Language Model, LM)。智能体可以用一个或多个任意规模（小 / 大）的语言模型，只要它们能遵循基于指令的推理与逻辑框架，例如 ReAct、思维链 (Chain-of-Thought) 或思维树 (Tree-of-Thoughts)。模型可以是通用的、多模态的，也可以按你这套智能体架构的需要做微调 (Fine-tuning)。要在生产里取得最好的结果，应当选用最贴合最终应用的模型；理想情况下，它还在与你计划放进认知架构的那些工具相关的数据特征上受过训练。需要注意：模型通常并没有拿智能体的具体配置（也就是工具选择、编排 / 推理设置）来训练。不过，仍然可以进一步打磨模型，让它更适合智能体的任务：给它看一些展示智能体能力的例子，包括智能体在不同情境里使用特定工具或推理步骤的实例。</mark>

---

## The tools

<mark>工具</mark>

Foundational models, despite their impressive text and image generation, remain constrained by their inability to interact with the outside world. Tools bridge this gap, empowering agents to interact with external data and services while unlocking a wider range of actions beyond that of the underlying model alone. Tools can take a variety of forms and have varying depths of complexity, but typically align with common web API methods like GET, POST, PATCH, and DELETE. For example, a tool could update customer information in a database or fetch weather data to influence a travel recommendation that the agent is providing to the user. With tools, agents can access and process real-world information. This empowers them to support more specialized systems like retrieval augmented generation (RAG), which significantly extends an agent’s capabilities beyond what the foundational model can achieve on its own. We’ll discuss tools in more detail below, but the most important thing to understand is that tools bridge the gap between the agent’s internal capabilities and the external world, unlocking a broader range of possibilities.

<mark>基础模型 (foundational model) 生成文本和图像的能力很强，但仍然受限于无法与外部世界交互。工具补上了这条缺口，让智能体能与外部数据和服务交互，并打开比底层模型单独能做的更宽的行动范围。工具的形态和复杂程度各不相同，但通常对应常见的 Web API 方法，如 GET、POST、PATCH 和 DELETE。例如，一个工具可以更新数据库里的顾客信息，或取回天气数据，从而影响智能体给用户的旅行建议。有了工具，智能体就能访问并处理现实世界的信息。这使它们能够支持更专门的系统，比如检索增强生成 (Retrieval Augmented Generation, RAG)，把智能体的能力明显延伸到基础模型独自做不到的地方。工具的细节留到后面讲。最需要记住的是：工具连接的是智能体的内部能力与外部世界，从而打开更广的可能。</mark>

---

## The orchestration layer

<mark>编排层</mark>

The orchestration layer describes a cyclical process that governs how the agent takes in information, performs some internal reasoning, and uses that reasoning to inform its next action or decision. In general, this loop will continue until an agent has reached its goal or a stopping point. The complexity of the orchestration layer can vary greatly depending on the agent and task it’s performing. Some loops can be simple calculations with decision rules, while others may contain chained logic, involve additional machine learning algorithms, or implement other probabilistic reasoning techniques. We’ll discuss more about the detailed implementation of the agent orchestration layers in the cognitive architecture section.

<mark>编排层 (Orchestration Layer) 描述的是一个循环过程：它决定智能体如何接收信息、如何做内部推理，以及如何用这次推理来决定下一步行动或决策。一般而言，这个循环会一直进行，直到智能体达成目标，或到达一个停止点。编排层的复杂程度可以差很多，取决于智能体本身和它正在做的任务。有的循环只是带决策规则的简单计算；有的则包含链式逻辑、额外的机器学习算法，或其他概率推理技术。智能体编排层的具体实现，会在认知架构一节里再讲。</mark>

---

## Agents vs. models

<mark>智能体与模型</mark>

To gain a clearer understanding of the distinction between agents and models, consider the following chart:

<mark>要更清楚地分辨智能体和模型，可以看下面这张对照表：</mark>

| Models | Agents |
| --- | --- |
| Knowledge is limited to what is available in their training data. | Knowledge is extended through the connection with external systems via tools |
| Single inference / prediction based on the user query. Unless explicitly implemented for the model, there is no management of session history or continuous context. (i.e. chat history) | Managed session history (i.e. chat history) to allow for multi turn inference / prediction based on user queries and decisions made in the orchestration layer. In this context, a ‘turn’ is defined as an interaction between the interacting system and the agent. (i.e. 1 incoming event/query and 1 agent response) |
| No native tool implementation. | Tools are natively implemented in agent architecture. |
| No native logic layer implemented. Users can form prompts as simple questions or use reasoning frameworks (CoT, ReAct, etc.) to form complex prompts to guide the model in prediction. | Native cognitive architecture that uses reasoning frameworks like CoT, ReAct, or other pre-built agent frameworks like LangChain. |

| <mark>模型</mark> | <mark>智能体</mark> |
| --- | --- |
| <mark>知识限于训练数据里已有的内容。</mark> | <mark>知识通过工具与外部系统的连接得到延伸。</mark> |
| <mark>基于用户查询做单次推断 / 预测。除非专门为模型实现，否则不管理会话历史或连续上下文（例如聊天记录）。</mark> | <mark>管理会话历史（例如聊天记录），从而能基于用户查询以及编排层里做出的决策，进行多轮推断 / 预测。这里的「轮次 (turn)」指交互系统与智能体之间的一次交互（即 1 个传入事件 / 查询，加 1 次智能体响应）。</mark> |
| <mark>没有原生的工具实现。</mark> | <mark>工具是智能体架构里原生实现的。</mark> |
| <mark>没有原生的逻辑层。用户可以把提示写成简单问题，或用推理框架（CoT、ReAct 等）写成复杂提示，来引导模型预测。</mark> | <mark>有原生的认知架构，使用 CoT、ReAct 等推理框架，或其他预制的智能体框架，如 LangChain。</mark> |

---

## Cognitive architectures: How agents operate

<mark>认知架构：智能体如何运作</mark>

Imagine a chef in a busy kitchen. Their goal is to create delicious dishes for restaurant patrons which involves some cycle of planning, execution, and adjustment.

<mark>想象一位忙乱厨房里的厨师。目标是为餐厅客人做出美味的菜，这涉及规划 (Planning)、执行和调整的某种循环。</mark>

- They gather information, like the patron’s order and what ingredients are in the pantry and refrigerator.
- They perform some internal reasoning about what dishes and flavor profiles they can create based on the information they have just gathered.
- They take action to create the dish: chopping vegetables, blending spices, searing meat.

<mark>- 他们收集信息，比如客人点了什么，食品储藏室和冰箱里有哪些食材。</mark>

<mark>- 他们根据刚收集到的信息做内部推理：能做出哪些菜、哪些风味。</mark>

<mark>- 他们动手做菜：切菜、调香料、煎肉。</mark>

At each stage in the process the chef makes adjustments as needed, refining their plan as ingredients are depleted or customer feedback is received, and uses the set of previous outcomes to determine the next plan of action. This cycle of information intake, planning, executing, and adjusting describes a unique cognitive architecture that the chef employs to reach their goal.

<mark>过程中的每个阶段，厨师都会按需要调整：食材用尽或收到客人反馈时，就修正计划，并用此前的结果来决定下一步行动。这种接收信息、规划、执行、调整的循环，描述的就是厨师为达成目标而采用的一种独特认知架构。</mark>

Just like the chef, agents can use cognitive architectures to reach their end goals by iteratively processing information, making informed decisions, and refining next actions based on previous outputs. At the core of agent cognitive architectures lies the orchestration layer, responsible for maintaining memory, state, reasoning and planning. It uses the rapidly evolving field of prompt engineering and associated frameworks to guide reasoning and planning, enabling the agent to interact more effectively with its environment and complete tasks. Research in the area of prompt engineering frameworks and task planning for language models is rapidly evolving, yielding a variety of promising approaches. While not an exhaustive list, these are a few of the most popular frameworks and reasoning techniques available at the time of this publication:

<mark>智能体也像这位厨师一样，可以用认知架构来达成最终目标：反复处理信息、做出有依据的决策，并依据先前的输出修正下一步行动。智能体认知架构的核心是编排层，它负责维持记忆 (Memory)、状态、推理和规划。它借助快速演进的提示工程 (prompt engineering) 及相关框架来引导推理和规划，使智能体更能与环境有效交互并完成任务。语言模型的提示工程框架和任务规划研究发展很快，已经出现多种有希望的做法。下面不是完整清单，只是本文出版时最常用的几种框架和推理技术：</mark>

- ReAct, a prompt engineering framework that provides a thought process strategy for language models to Reason and take action on a user query, with or without in-context examples. ReAct prompting has shown to outperform several SOTA baselines and improve human interoperability and trustworthiness of LLMs.

<mark>- ReAct，一种提示工程框架。它为语言模型提供一套思考过程策略，使其能对用户查询进行推理并采取行动，可以带上下文示例，也可以不带。ReAct 提示已被证明优于若干当前最优 (SOTA) 基线，并提高了大语言模型 (LLM) 的人类互操作性与可信度。</mark>

- Chain-of-Thought (CoT), a prompt engineering framework that enables reasoning capabilities through intermediate steps. There are various sub-techniques of CoT including self-consistency, active-prompt, and multimodal CoT that each have strengths and weaknesses depending on the specific application.

<mark>- 思维链 (Chain-of-Thought, CoT)，一种通过中间步骤来实现推理能力的提示工程框架。CoT 有多种子技术，包括自洽 (self-consistency)、主动提示 (active-prompt) 和多模态 CoT。它们各有长短，取决于具体应用。</mark>

- Tree-of-thoughts (ToT), a prompt engineering framework that is well suited for exploration or strategic lookahead tasks. It generalizes over chain-of-thought prompting and allows the model to explore various thought chains that serve as intermediate steps for general problem solving with language models.

<mark>- 思维树 (Tree-of-Thoughts, ToT)，一种很适合探索或策略性前瞻任务的提示工程框架。它是思维链提示的推广，允许模型探索多条思维链，把它们当作用语言模型做一般问题求解时的中间步骤。</mark>

Agents can utilize one of the above reasoning techniques, or many other techniques, to choose the next best action for the given user request. For example, let’s consider an agent that is programmed to use the ReAct framework to choose the correct actions and tools for the user query. The sequence of events might go something like this:

<mark>智能体可以用上面的某一种推理技术，也可以用许多其他技术，为给定的用户请求选择下一步最好的行动。例如，设想一个被编程为使用 ReAct 框架的智能体，它要为用户查询选择正确的行动和工具。事件顺序大致如下：</mark>

1. User sends query to the agent
2. Agent begins the ReAct sequence
3. The agent provides a prompt to the model, asking it to generate one of the next ReAct steps and its corresponding output:
   a. Question: The input question from the user query, provided with the prompt
   b. Thought: The model’s thoughts about what it should do next
   c. Action: The model’s decision on what action to take next
      i. This is where tool choice can occur
      ii. For example, an action could be one of [Flights, Search, Code, None], where the first 3 represent a known tool that the model can choose, and the last represents “no tool choice”
   d. Action input: The model’s decision on what inputs to provide to the tool (if any)
   e. Observation: The result of the action / action input sequence
      i. This thought / action / action input / observation could repeat N-times as needed
   f. Final answer: The model’s final answer to provide to the original user query
4. The ReAct loop concludes and a final answer is provided back to the user

<mark>1. 用户把查询发给智能体</mark>

<mark>2. 智能体开始 ReAct 序列</mark>

<mark>3. 智能体向模型提供一段提示，要求它生成下一步 ReAct 步骤之一，以及对应的输出：</mark>

<mark>a. Question（问题）：来自用户查询的输入问题，随提示一起提供</mark>

<mark>b. Thought（思考）：模型关于下一步该做什么的想法</mark>

<mark>c. Action（行动）：模型对下一步采取什么行动的决定</mark>

<mark>i. 工具选择发生在这里</mark>

<mark>ii. 例如，一个行动可以是 [Flights, Search, Code, None] 之一。前 3 个代表模型可以选择的已知工具，最后一个表示「不选择工具」</mark>

<mark>d. Action input（行动输入）：模型决定向工具提供什么输入（如果有的话）</mark>

<mark>e. Observation（观察）：行动 / 行动输入这一序列的结果</mark>

<mark>i. 这一思考 / 行动 / 行动输入 / 观察可以根据需要重复 N 次</mark>

<mark>f. Final answer（最终答案）：模型针对原始用户查询给出的最终答案</mark>

<mark>4. ReAct 循环结束，最终答案返回给用户</mark>

![Example agent with ReAct reasoning in the orchestration layer](image_002_page_11.png)

<mark>图 2：编排层中带 ReAct 推理的智能体示例。用户说「我想订一张从奥斯汀到苏黎世的机票」；编排层依次产生 Question、Thought、Action（Flights 工具）、Action Input、Observation 和 Final Answer；可选工具包括 Flights、Search、Code 和 Calc；最终回复是「这里有一些你可能感兴趣的航班……」。</mark>

As shown in Figure 2, the model, tools, and agent configuration work together to provide a grounded, concise response back to the user based on the user’s original query. While the model could have guessed at an answer (hallucinated) based on its prior knowledge, it instead used a tool (Flights) to search for real-time external information. This additional information was provided to the model, allowing it to make a more informed decision based on real factual data and to summarize this information back to the user.

<mark>如图 2 所示，模型、工具和智能体配置一起工作，依据用户的原始查询，返回一个有依据、简洁的响应。模型本可以凭已有知识猜一个答案（也就是幻觉，hallucinated），但它改为使用工具（Flights）去搜索实时的外部信息。这些额外信息再提供给模型，使它能基于真实的事实数据做出更有依据的决定，并把这些信息总结给用户。</mark>

In summary, the quality of agent responses can be tied directly to the model’s ability to reason and act about these various tasks, including the ability to select the right tools, and how well that tools has been defined. Like a chef crafting a dish with fresh ingredients and attentive to customer feedback, agents rely on sound reasoning and reliable information to deliver optimal results. In the next section, we’ll dive into the various ways agents connect with fresh data.

<mark>总之，智能体响应的质量，直接取决于模型对这些不同任务进行推理和行动的能力，包括选对工具的能力，以及这些工具定义得好不好。就像厨师用新鲜食材做菜、并留意客人反馈一样，智能体要靠可靠的推理和可靠的信息，才能给出最好的结果。下一节会深入讲智能体连接新鲜数据的各种方式。</mark>

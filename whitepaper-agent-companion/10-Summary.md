# Summary

<mark>总结</mark>

This whitepaper (a companion to our earlier whitepaper on Agents) has explored the rapidly evolving landscape of generative AI agents, from their fundamental architecture to advanced evaluation techniques and the transformative potential of multi-agent systems.

<mark>本白皮书（我们早前那篇《智能体》白皮书的伴读）探索了生成式 AI 智能体 (Agent) 迅速变化的图景：从基础架构，到进阶的评估 (Evaluation) 技术，再到多智能体 (Multi-Agent) 系统的变革潜力。</mark>

---

## Key Takeaways for Developers

<mark>给开发者的要点</mark>

1. **AgentOps is Essential:** Building successful agents goes far beyond the initial proof-of-concept. Embrace AgentOps principles, integrating best practices from DevOps and MLOps, but also focusing on agent-specific elements like tool management, orchestration, memory, and task decomposition.

<mark>1. **智能体运维 (AgentOps) 必不可少：** 成功的智能体远不止最初的概念验证。拥抱 AgentOps 原则，把 DevOps 和 MLOps 的最佳实践纳进来，同时聚焦智能体特有的要素，例如工具 (Tools) 管理、编排、记忆和任务分解。</mark>

2. **Metrics Drive Improvement:** Start with business-level KPIs (like goal completion, user engagement, or revenue) as your "north star." Then, instrument your agents to track granular metrics related to critical tasks, user interactions, and agent actions (traces). Human feedback (👍👎, user surveys) is invaluable.

<mark>2. **用指标推动改进：** 先把业务层的关键绩效指标 (KPI)，如目标完成、用户参与或收入，当作「北极星」。再给智能体埋点，跟踪与关键任务、用户交互和智能体动作（追踪）相关的细粒度指标。人类反馈（👍👎、用户调查）非常宝贵。</mark>

3. **Automated Evaluation is Key:** Don't rely solely on manual testing. Implement automated evaluation frameworks that assess agent capabilities, trajectory (the steps taken), and the final response. Leverage techniques like exact match, in-order match, precision/recall for trajectory evaluation, and autoraters (LLMs as judges) for final response quality.

<mark>3. **自动评估是关键：** 不要只靠人工测试。建立自动化评估框架，用来评估智能体能力、轨迹（实际走过的步骤）和最终回答。轨迹评估可以利用精确匹配、按序匹配、精确率/召回率等技术；最终回答的质量则可以用自动评分器（以大语言模型 (LLM) 为裁判）。</mark>

4. **Human-in-the-Loop is Crucial:** Automated metrics are powerful, but human evaluation provides essential context, especially for subjective aspects like creativity, common sense, and nuance. Use human feedback to calibrate and validate your automated evaluation methods. Don't outsource the domain knowledge.

<mark>4. **人在回路至关重要：** 自动化指标很有力，但人工评估提供必不可少的上下文，尤其是创造力、常识和细微差别这类主观方面。用人类反馈来校准并验证自动化评估方法。不要把领域知识外包出去。</mark>

5. **Multi-Agent Systems Offer Advantages:** Consider multi-agent architectures for complex tasks. They can improve accuracy, efficiency, scalability, and fault tolerance. Understand different design patterns (sequential, hierarchical, collaborative, competitive) and choose the right one for your application.

<mark>5. **多智能体系统有其优势：** 复杂任务可以考虑多智能体架构。它们能提高准确性、效率、可扩展性和容错能力。弄清不同的设计模式（顺序、层级、协作、竞争），并为你的应用选对那一种。</mark>

6. **Agentic RAG Improves Relevance:** Move beyond traditional RAG by incorporating agents that actively refine search queries, evaluate retrieved information, and adapt to evolving knowledge. This leads to more accurate and contextually relevant responses.

<mark>6. **智能体式检索增强生成 (Agentic RAG) 能提高相关性：** 在传统检索增强生成 (RAG) 之上再进一步，纳入能主动精炼搜索查询、评估检索到的信息，并适应不断变化的知识的智能体。这样会得到更准确、也更贴合上下文的回答。</mark>

7. **Search Optimization is Foundational to RAG:** Before diving into complex agentic RAG, optimize your underlying search engine. Techniques like semantic chunking, metadata enrichment, fine-tuning embedding models, and using rankers can significantly improve retrieval quality.

<mark>7. **搜索优化是 RAG 的基础：** 在深入复杂的智能体式 RAG 之前，先优化底层搜索引擎。语义分块、元数据增强、微调嵌入模型，以及使用排序器等技术，都能显著提高检索质量。</mark>

8. **Agent and Tool Registries are Important:** As the number of Agents or Tools you are using grow, a registry to manage the capabilities, ontology, and performance becomes essential.

<mark>8. **智能体与工具注册表很重要：** 随着在用的智能体或工具越来越多，就需要一个注册表来管理能力、本体和性能。</mark>

9. **Security is Paramount:** When deploying agents, especially within an enterprise, prioritize security. Leverage platforms like Google Agentspace that offer built-in security features like RBAC, VPC Service Controls, and IAM integration.

<mark>9. **安全至关重要：** 部署智能体时，尤其是在企业内部，要把安全放在首位。借助 Google Agentspace 这类平台，它们自带 RBAC、VPC Service Controls 和 IAM 集成等安全能力。</mark>

10. **Efficient use of developer cycles:** The classic build vs buy design choices remain front of mind, as the industry of gen AI agents is rapidly evolving. Consider platforms and products as alternatives to building everything from scratch. This will buffer some of the churn of a fast changing industry and allow you to focus on your data, domain, and users.

<mark>10. **高效使用开发者的工时：** 自建还是购买，这个经典的设计选择仍然摆在面前，因为生成式 AI 智能体行业正在快速演变。可以把平台和产品当作从零造一切的替代。这样能缓冲这个快速变化的行业带来的一部分变动，让你专注于自己的数据、领域和用户。</mark>

11. **Agents in the enterprise:** Agents are transforming the way we work by making us much more productive, and the way automation can be accomplished. Knowledge workers will increasingly be managing fleets of agents and novel UX will emerge. Google Agentspace is a powerful tool allowing to put Enterprise Search, AI and AI Agents on top of company's data and workflows.

<mark>11. **企业中的智能体：** 智能体正在改变我们的工作方式，让我们高效得多，也在改变自动化得以完成的方式。知识工作者将越来越多地管理成群的智能体，新的用户体验也会出现。Google Agentspace 是一个有力的工具，可以把 Enterprise Search、AI 和 AI 智能体放到公司的数据与工作流之上。</mark>

---

## Future Directions for Agent Research and Development

<mark>智能体研究与开发的未来方向</mark>

The field of AI agents is undergoing rapid evolution. Key areas of ongoing research and development include:

<mark>AI 智能体这一领域正在快速演变。持续的研究与开发主要包括这些方向：</mark>

- **Advanced Evaluation Methods:** Developing more robust and scalable evaluation techniques, including process-based evaluation (focusing on reasoning), AI-assisted evaluation, and standardized benchmarks.

<mark>- **进阶评估方法：** 开发更稳健、更可扩展的评估技术，包括基于过程的评估（聚焦推理）、AI 辅助评估，以及标准化基准。</mark>

- **Multi-Agent Coordination:** Improving the coordination and communication mechanisms within multi-agent systems to enable more effective collaboration, task handling, and reasoning.

<mark>- **多智能体协调：** 改进多智能体系统内部的协调与通信机制，从而更有效地协作、处理任务并进行推理。</mark>

- **Real-World Adaptation:** Creating agents that can adapt and learn in dynamic, unpredictable real-world environments. Production systems like automotive AI illustrate how agents must balance between on-device performance for critical functions and cloud-based capabilities for complex tasks, often adapting to changing connectivity conditions.

<mark>- **适应现实世界：** 做出能在动态、不可预测的现实环境里适应并学习的智能体。汽车 AI 这类生产系统说明，智能体必须在关键功能的端侧性能与复杂任务的云端能力之间取得平衡，并常常要适应不断变化的连接状况。</mark>

- **Explainability and Interpretability:** Making agent behavior more transparent and understandable, allowing developers and users to gain deeper insights into their decision-making processes.

<mark>- **可解释性与可阐释性：** 让智能体的行为更透明、更好理解，使开发者和用户能更深入地理解它们的决策过程。</mark>

- **Long-Term Memory and Learning:** Developing more sophisticated memory mechanisms that allow agents to retain and utilize information over extended periods, enabling continuous learning and adaptation.

<mark>- **长期记忆与学习：** 开发更精细的记忆机制，让智能体能在更长时间里保留并使用信息，从而持续学习、持续适应。</mark>

- **Agent Communication Protocols:** Better defining how agents share tasks, knowledge, and messages, especially across remote systems which are opaque.

<mark>- **智能体通信协议：** 更好地定义智能体如何共享任务、知识和消息，尤其是跨越那些不透明的远程系统时。</mark>

- **From Agents to contractors:** In order for agents to get to next level of reliability and utility, we will need to step up the definition of tasks, making them into contracts with clear deliverables, validation mechanisms, and ability to negotiate ambiguities, similarly to how we contract work from other companies.

<mark>- **从智能体到承包方：** 要让智能体的可靠性与效用再上一个台阶，就需要把任务定义再提高一步，做成带有明确交付物、验证机制，以及协商模糊之处的能力的合约 (Contract)，就像我们向别的公司发包一样。</mark>

---

## Call to Action

<mark>行动号召</mark>

The future of AI is agentic. We encourage developers to embrace these concepts and begin building the next generation of intelligent applications. Start experimenting with the tools and techniques discussed in this whitepaper. Explore the resources available, such as Google Agentspace, NotebookLM Enterprise, Vertex Eval Service, Cloud Observability, and Vertex AI Search, to accelerate your development process. Dive into the provided code examples, tutorials, and documentation to gain hands-on experience. Build, evaluate, iterate, and contribute to the growing community of agent developers. The possibilities are limitless, and the time to build is now! Specifically, get started with the code and Colab notebooks in the references.

<mark>AI 的未来是智能体式的。我们鼓励开发者拥抱这些概念，开始构建下一代智能应用。先去试这本白皮书里讨论过的工具和技术。再去看现成的资源，例如 Google Agentspace、NotebookLM Enterprise、Vertex Eval Service、Cloud Observability 和 Vertex AI Search，用来加快开发过程。钻进提供的代码示例、教程和文档，取得动手经验。去构建、评估、迭代，并加入不断壮大的智能体开发者社区。可能性没有穷尽，现在就是构建的时候。具体来说，从参考文献里的代码和 Colab 笔记本开始。</mark>

# Production applications with Vertex AI agents

用 Vertex AI 智能体构建生产应用

While this whitepaper explored the core components of agents, building production-grade applications requires integrating them with additional tools like user interfaces, evaluation frameworks, and continuous improvement mechanisms. Google’s Vertex AI platform simplifies this process by offering a fully managed environment with all the fundamental elements covered earlier. Using a natural language interface, developers can rapidly define crucial elements of their agents - goals, task instructions, tools, sub-agents for task delegation, and examples - to easily construct the desired system behavior. In addition, the platform comes with a set of development tools that allow for testing, evaluation, measuring agent performance, debugging, and improving the overall quality of developed agents. This allows developers to focus on building and refining their agents while the complexities of infrastructure, deployment and maintenance are managed by the platform itself.

本白皮书讨论了智能体 (Agent) 的核心组件。要构建生产级应用，还需要把它们与其他工具集成起来，例如用户界面、评估框架和持续改进机制。Google 的 Vertex AI 平台把这个过程简化了：它提供一个全托管环境，包含前面讲过的全部基础要素。开发者可以用自然语言界面，快速定义智能体的关键要素——目标、任务指令、工具 (Tools)、用于任务委派的子智能体，以及示例——从而容易地构造出想要的系统行为。此外，平台还带有一套开发工具，用于测试、评估、衡量智能体表现、调试，并提高所开发智能体的整体质量。这样，开发者可以专注于构建和打磨智能体，基础设施、部署和维护的复杂性则由平台自己承担。

In Figure 15 we’ve provided a sample architecture of an agent that was built on the Vertex AI platform using various features such as Vertex Agent Builder, Vertex Extensions, Vertex Function Calling and Vertex Example Store to name a few. The architecture includes many of the various components necessary for a production ready application.

图 15 给出了一个在 Vertex AI 平台上构建的智能体架构示例，用到了 Vertex Agent Builder、Vertex 扩展 (Vertex Extensions)、Vertex 函数调用 (Vertex Function Calling) 和 Vertex 示例存储 (Vertex Example Store) 等多项能力。这个架构包含生产就绪应用所需的许多组件。

![Sample end-to-end agent architecture on Vertex AI](image_014_page_39.png)

图 15：在 Vertex AI 平台上构建的端到端智能体架构示例。用户经自定义 UI 进入智能体；智能体持有提示和工具定义，并与模型交互。函数执行环从智能体走到函数，再由自定义 UI 调用 Google Places API。扩展执行环从模型走到扩展和向量搜索 API，再回到模型。

You can try a sample of this prebuilt agent architecture from our official documentation.

可以在官方文档里试用这个预制智能体架构的示例。

# 5-Day AI Agents Intensive Course with Google

与 Google 一起的 5 日 AI 智能体高强度课程

Source: [https://www.kaggle.com/learn-guide/5-day-agents](https://www.kaggle.com/learn-guide/5-day-agents)

原文：[https://www.kaggle.com/learn-guide/5-day-agents](https://www.kaggle.com/learn-guide/5-day-agents)

Each English paragraph is followed by its Chinese translation.

英文段落后紧跟中文。

---

## What is the 5-Day AI Agents Intensive?

什么是 5 日 AI 智能体高强度课程？

The [5-Day AI Agents Intensive course with Google](https://blog.google/innovation-and-ai/technology/developers-tools/ai-agents-intensive-recap/) is a hands-on program originally held live from November 10 - 14, 2025. It is now available as a self-paced Kaggle Learn guide so anyone can explore the foundations, architecture and practical development of AI agents.

[与 Google 一起的 5 日 AI 智能体高强度课程](https://blog.google/innovation-and-ai/technology/developers-tools/ai-agents-intensive-recap/)是一门动手实践课程，最初于 2025 年 11 月 10 日至 14 日以直播形式举办。它现在作为自定进度的 Kaggle Learn 指南开放，任何人都可以借此探索 AI 智能体 (Agent) 的基础、架构与实际开发。

This course was crafted by Google's ML researchers and engineers to help developers explore the foundations and practical applications of AI agents. You'll learn the core components – models, tools, orchestration, memory and evaluation. Finally, you'll discover how agents move beyond LLM prototypes to become production-ready systems.

这门课程由 Google 的机器学习 (ML) 研究人员和工程师设计，帮助开发者探索 AI 智能体的基础与实际应用。你将学习这些核心组件：模型 (Model)、工具 (Tools)、编排 (Orchestration)、记忆 (Memory) 和评估 (Evaluation)。最后，你将了解智能体如何超越大语言模型 (LLM) 原型，成为可投入生产的系统。

Each day blends conceptual deep dives with hands-on examples, codelabs, and live discussions. By the end, you'll be ready to build, evaluate, and deploy agents that solve real-world problems.

每一天都把概念深入讲解、动手示例、代码实验 (codelab) 和直播讨论结合在一起。课程结束时，你将能够构建、评估并部署能解决真实问题的智能体。

---

## Welcome to our Agents Intensive Learn Guide!

欢迎来到智能体高强度学习指南！

### What's being covered?

课程涵盖什么？

- Day 1 - Introduction to Agents: Explore the foundational concepts of AI agents, their defining characteristics, and how agentic architectures differ from traditional LLM applications, laying the groundwork for building intelligent, autonomous systems.

  第 1 天 - 智能体入门：探索 AI 智能体的基础概念和定义特征，以及智能体架构 (agentic architecture) 与传统 LLM 应用有何不同，为构建智能、自主的系统打下基础。

- Day 2 - Agent Tools & Interoperability with Model Context Protocol (MCP): Dive into the world of tools, understanding how AI agents can "take action" by leveraging external functionalities and APIs, and explore the ease of discovering and using tools offered by the MCP.

  第 2 天 - 智能体工具与互操作性：模型上下文协议 (Model Context Protocol, MCP)：深入工具的世界，理解 AI 智能体如何借助外部功能和 API「采取行动」，并探索 MCP 在发现和使用工具上带来的便利。

- Day 3 - Context Engineering: Sessions & Memory: Explore how to build AI agents that can remember past interactions and maintain context. Learn how to implement short-term and long-term memory to create more robust agents capable of handling complex, multi-turn tasks.

  第 3 天 - 上下文工程 (Context Engineering)：会话 (Session) 与记忆：探索如何构建能记住过往交互并保持上下文的 AI 智能体。学习如何实现短期记忆和长期记忆，从而打造更能处理复杂多轮任务的稳健智能体。

- Day 4 - Agent Quality: Learn to build robust and reliable AI agents by mastering the critical disciplines of evaluating and improving agents. This session will cover observability, logging, and tracing to provide visibility, alongside key metrics and evaluation strategies to optimize agent performance.

  第 4 天 - 智能体质量：掌握评估和改进智能体这两项关键能力，学会构建稳健、可靠的 AI 智能体。本讲将介绍可观测性 (Observability)、日志和追踪 (tracing)，让智能体的行为可见，同时介绍关键指标和评估策略，以优化智能体表现。

- Day 5 - Prototype to Production: Go beyond local testing and learn to deploy and scale AI agents for real-world use. This session will cover the best practices for deploying your agents so that others can use them, including how to create a truly multi-agent system with the Agent2Agent (A2A) Protocol.

  第 5 天 - 从原型到生产：超越本地测试，学习如何为真实使用部署和扩展 AI 智能体。本讲将介绍部署智能体、让其他人也能使用它们的最佳实践，包括如何用智能体对智能体协议 (Agent2Agent Protocol, A2A) 创建真正的多智能体系统。

---

## Setup Instructions

环境准备

To ensure you are ready for the course, please complete these essential setup steps:

为确保你已准备好上课，请完成这些必要的准备步骤：

- Kaggle account: Sign up for a [Kaggle](https://www.kaggle.com/) account and [learn how Notebooks work](https://www.youtube.com/watch?v=BPQDZLPtgDc). Make sure to [phone verify](https://www.kaggle.com/settings) your account, it's necessary for the course's codelabs.

  Kaggle 账号：注册一个 [Kaggle](https://www.kaggle.com/) 账号，并[了解 Notebook 如何工作](https://www.youtube.com/watch?v=BPQDZLPtgDc)。请务必对账号进行[手机验证](https://www.kaggle.com/settings)，课程的代码实验需要这一步。

- AI Studio account: Sign up for an [AI Studio](https://aistudio.google.com/) account and ensure you can generate an [API key](https://aistudio.google.com/app/apikey).

  AI Studio 账号：注册一个 [AI Studio](https://aistudio.google.com/) 账号，并确认你能生成 [API 密钥](https://aistudio.google.com/app/apikey)。

- [Kaggle Discord](http://discord.gg/kaggle): Sign up for a Discord account and join us on the Kaggle Discord server to connect and collaborate with fellow learners in this course.

  [Kaggle Discord](http://discord.gg/kaggle)：注册一个 Discord 账号，并加入 Kaggle Discord 服务器，与本课程的其他学习者联系、协作。

---

## Day 1 (Introduction to Agents)

第 1 天（智能体入门）

Welcome to Day 1.

欢迎来到第 1 天。

This whitepaper introduces AI agents. It presents a taxonomy of agent capabilities, emphasizes the need for an Agent Ops discipline for reliability and governance, and discusses the importance of agent interoperability and security through identity and constrained policies.

这篇白皮书介绍 AI 智能体。它给出智能体能力的分类体系 (taxonomy)，强调需要建立智能体运维 (Agent Ops) 这一学科来保证可靠性与治理，并讨论通过身份和受约束的策略来实现智能体互操作性与安全的重要性。

In the codelabs, you'll be building your first AI agent and your first multi-agent system, using Agent Development Kit (ADK), powered by Gemini, and giving it the ability to use Google Search to answer questions with up-to-date information. In the second codelab, the focus will be on multi-agent systems, where you'll learn how to create teams of specialized agents and explore different architectural patterns.

在代码实验里，你将使用由 Gemini 驱动的智能体开发套件 (Agent Development Kit, ADK)，构建你的第一个 AI 智能体和第一个多智能体系统，并让它能够使用 Google Search，用最新信息回答问题。第二个代码实验聚焦多智能体系统：你将学习如何创建由专职智能体组成的团队，并探索不同的架构模式。

### Day 1 Assignments

第 1 天作业

1. Complete the Unit 1 – "Introduction to Agents":

   完成第 1 单元：「智能体入门」：

   - Listen to the [summary podcast episode](https://www.youtube.com/watch?v=zTxvGzpfF-g) for this unit.

     收听本单元的[摘要播客](https://www.youtube.com/watch?v=zTxvGzpfF-g)。

   - To complement the podcast, read the updated ["Introduction to Agents" whitepaper](https://www.kaggle.com/whitepaper-introduction-to-agents).

     作为播客的补充，阅读更新后的白皮书「[智能体入门](https://www.kaggle.com/whitepaper-introduction-to-agents)」。

   - Complete these codelabs on Kaggle:

     在 Kaggle 上完成这些代码实验：

     - [Build your first agent using Gemini and ADK.](https://www.kaggle.com/code/kaggle5daysofai/day-1a-from-prompt-to-action)

       [用 Gemini 和 ADK 构建你的第一个智能体。](https://www.kaggle.com/code/kaggle5daysofai/day-1a-from-prompt-to-action)

     - [Build your first multi-agent systems using ADK.](https://www.kaggle.com/code/kaggle5daysofai/day-1b-agent-architectures)

       [用 ADK 构建你的第一批多智能体系统。](https://www.kaggle.com/code/kaggle5daysofai/day-1b-agent-architectures)

   - Make sure you [phone verify](https://www.kaggle.com/settings) your Kaggle account before starting, it's necessary for the codelabs.

     开始之前，请务必对你的 Kaggle 账号进行[手机验证](https://www.kaggle.com/settings)，代码实验需要这一步。

   - We also have a [troubleshooting guide](https://www.kaggle.com/code/kaggle5daysofai/day-0-troubleshooting-and-faqs) for the codelabs. Be sure to check there for solutions to common problems.

     我们也为代码实验准备了[故障排查指南](https://www.kaggle.com/code/kaggle5daysofai/day-0-troubleshooting-and-faqs)。常见问题的解决办法请到那里查看。

   - Want to have an [interactive conversation](https://support.google.com/notebooklm/answer/15731776)? Try adding the whitepapers to [NotebookLM](https://notebooklm.google.com/).

     想进行一场[互动对话](https://support.google.com/notebooklm/answer/15731776)吗？试试把白皮书加到 [NotebookLM](https://notebooklm.google.com/)。

   - [Optional]: Watch the recorded [YouTube livestream](https://www.youtube.com/live/ZaUcqznlhv8). [Kanchana Patlolla](https://www.linkedin.com/in/kanchanapatlolla/) and [Anant Nawalgaria](https://www.linkedin.com/in/anant-nawalgaria/) hosted the first livestream on Kaggle's YouTube channel. They were joined by codelab authors Kristopher Overholt and Hangfei Lin, along with special guests from Google: Alan Blount, Mike Clark, Michael Gerstenhaber, and Antonio Gulli to discuss the assignments and shared insights.

     ［可选］：观看录制的 [YouTube 直播](https://www.youtube.com/live/ZaUcqznlhv8)。[Kanchana Patlolla](https://www.linkedin.com/in/kanchanapatlolla/) 和 [Anant Nawalgaria](https://www.linkedin.com/in/anant-nawalgaria/) 在 Kaggle 的 YouTube 频道主持了第一场直播。代码实验作者 Kristopher Overholt 和 Hangfei Lin 参加了直播，来自 Google 的特邀嘉宾还有 Alan Blount、Mike Clark、Michael Gerstenhaber 和 Antonio Gulli。他们讨论了作业，并分享了见解。

---

## Day 2 (Agent Tools & Interoperability with Model Context Protocol (MCP))

第 2 天（智能体工具与互操作性：模型上下文协议 (MCP)）

Welcome to Day 2.

欢迎来到第 2 天。

This whitepaper focuses on external tools functions that allow an agent to perform actions or retrieve real-time data beyond its training set and introduces best practices for designing effective tools. You'll learn about MCP, highlighting its architectural components, communication layer, risks and enterprise readiness gaps.

这篇白皮书聚焦外部工具函数：它们让智能体能够执行动作，或检索其训练集之外的实时数据。白皮书还介绍设计有效工具的最佳实践。你将学习 MCP，包括它的架构组件、通信层、风险，以及企业就绪方面的差距。

In the codelabs, you will create custom tools for your agents by turning your own Python functions into actions your agent can perform. You'll also use MCP and implement long-running operations where an agent can pause tool calls while waiting for human approval, before resuming.

在代码实验里，你将把自己的 Python 函数变成智能体能执行的动作，从而为智能体创建自定义工具。你还会使用 MCP，并实现长时间运行的操作 (long-running operation)：智能体可以在等待人工批准时暂停工具调用 (tool call)，然后再继续。

### Day 2 Assignments

第 2 天作业

Complete Unit 2 - "Agent Tools & Interoperability with Model Context Protocol (MCP)":

完成第 2 单元：「智能体工具与互操作性：模型上下文协议 (MCP)」：

- Listen to the [summary podcast episode](https://www.youtube.com/watch?v=Cr4NA6rxHAM) for this unit.

  收听本单元的[摘要播客](https://www.youtube.com/watch?v=Cr4NA6rxHAM)。

- To complement the podcast, read the updated ["Agent Tools & Interoperability with Model Context Protocol (MCP)" whitepaper](https://www.kaggle.com/whitepaper-agent-tools-and-interoperability-with-mcp).

  作为播客的补充，阅读更新后的白皮书「[智能体工具与互操作性：模型上下文协议 (MCP)](https://www.kaggle.com/whitepaper-agent-tools-and-interoperability-with-mcp)」。

- Complete these codelabs on Kaggle:

  在 Kaggle 上完成这些代码实验：

  - [Explore new ways to add tools to extend what your agents can do.](https://www.kaggle.com/code/kaggle5daysofai/day-2a-agent-tools)

    [探索为智能体添加工具、扩展其能力的新方法。](https://www.kaggle.com/code/kaggle5daysofai/day-2a-agent-tools)

  - [Explore best practices for tools, including using MCP and long-running operations.](https://www.kaggle.com/code/kaggle5daysofai/day-2b-agent-tools-best-practices)

    [探索工具的最佳实践，包括使用 MCP 和长时间运行的操作。](https://www.kaggle.com/code/kaggle5daysofai/day-2b-agent-tools-best-practices)

- [Optional]: Watch the recorded [YouTube livestream](https://www.youtube.com/live/8Gk1BE3uYek). Kanchana Patlolla and Anant Nawalgaria were joined by codelab author Laxmi Harikumar, along with Google guests Edward Grefenstette, Mike Styer, and Oriol Vinyals, as well as external speaker Alex Wissner-Gross from [Reified](https://reifiedllc.com/), to discuss the assignments and share insights.

  ［可选］：观看录制的 [YouTube 直播](https://www.youtube.com/live/8Gk1BE3uYek)。Kanchana Patlolla 和 Anant Nawalgaria 与代码实验作者 Laxmi Harikumar 一起参加，Google 嘉宾还有 Edward Grefenstette、Mike Styer 和 Oriol Vinyals，外部讲者是来自 [Reified](https://reifiedllc.com/) 的 Alex Wissner-Gross。他们讨论了作业并分享了见解。

---

## Day 3 (Context Engineering: Sessions & Memory)

第 3 天（上下文工程：会话与记忆）

Welcome to Day 3.

欢迎来到第 3 天。

This whitepaper explores context engineering as the practice of dynamically assembling and managing information within an agent's context window to create stateful and personalized AI experiences. It defines Sessions as the container for a single, immediate conversation's history, and Memory as the long-term persistence mechanism.

这篇白皮书把上下文工程视为一种实践：在智能体的上下文窗口 (context window) 里动态组装和管理信息，从而创造有状态 (stateful)、个性化的 AI 体验。它把会话定义为单次、当下对话历史的容器，把记忆定义为长期持久化机制。

In the codelabs, you will learn how to make agents stateful by managing conversation history through context engineering in ADK, and working memory within a session, allowing your agent to remember context and have coherent, multi-turn conversations. In the second notebook, you'll give your agent long-term memory that persists across different sessions.

在代码实验里，你将学习如何通过 ADK 中的上下文工程来管理对话历史，以及会话内的工作记忆 (working memory)，让智能体变得有状态，从而记住上下文并进行连贯的多轮对话。在第二个 Notebook 里，你将给智能体加上能跨不同会话持久保存的长期记忆。

### Day 3 Assignment

第 3 天作业

Complete Unit 3 - "Context Engineering: Sessions & Memory":

完成第 3 单元：「上下文工程：会话与记忆」：

- Listen to the [summary podcast episode](https://www.youtube.com/watch?v=FMcExVE15a4) for this unit.

  收听本单元的[摘要播客](https://www.youtube.com/watch?v=FMcExVE15a4)。

- To complement the podcast, read the updated ["Context Engineering: Sessions & Memory" whitepaper](https://www.kaggle.com/whitepaper-context-engineering-sessions-and-memory).

  作为播客的补充，阅读更新后的白皮书「[上下文工程：会话与记忆](https://www.kaggle.com/whitepaper-context-engineering-sessions-and-memory)」。

- Complete these codelabs on Kaggle:

  在 Kaggle 上完成这些代码实验：

  - [Build stateful agents and perform context engineering.](https://www.kaggle.com/code/kaggle5daysofai/day-3a-agent-sessions)

    [构建有状态的智能体，并进行上下文工程。](https://www.kaggle.com/code/kaggle5daysofai/day-3a-agent-sessions)

  - [Explore how to use memory with your agent.](https://www.kaggle.com/code/kaggle5daysofai/day-3b-agent-memory)

    [探索如何让你的智能体使用记忆。](https://www.kaggle.com/code/kaggle5daysofai/day-3b-agent-memory)

- [Optional]: Watch the recorded [YouTube livestream](https://www.youtube.com/live/8o-GXj8A3nE). Kanchana Patlolla and Anant Nawalgaria were joined by codelab author Kristopher Overholt, along with guests from Google: Steven Johnson, Kimberly Milam and Julia Wiesinger, and external speaker Jay Alammar from [Cohere](https://cohere.com/).

  ［可选］：观看录制的 [YouTube 直播](https://www.youtube.com/live/8o-GXj8A3nE)。Kanchana Patlolla 和 Anant Nawalgaria 与代码实验作者 Kristopher Overholt 一起参加，来自 Google 的嘉宾还有 Steven Johnson、Kimberly Milam 和 Julia Wiesinger，外部讲者是来自 [Cohere](https://cohere.com/) 的 Jay Alammar。

---

## Day 4 (Agent Quality)

第 4 天（智能体质量）

Welcome to Day 4.

欢迎来到第 4 天。

This whitepaper addresses the challenge of assuring quality in AI agents by introducing a holistic evaluation framework. The necessary technical foundation for this is Observability, built on three pillars: Logs (the diary), Traces (the narrative), and Metrics (the health report), enabling a continuous feedback loop using scalable methods like LLM-as-a-Judge and Human-in-the-Loop (HITL) evaluation.

这篇白皮书通过引入一套整体评估框架，来应对保证 AI 智能体质量的挑战。这项工作必要的技术基础是可观测性，它建立在三根支柱上：日志 (Logs)，好比日记；追踪 (Traces)，好比叙事；指标 (Metrics)，好比健康报告。在此之上，可以用大模型即评委 (LLM-as-a-Judge) 和人在回路 (Human-in-the-Loop, HITL) 评估这类可扩展方法，形成持续的反馈回路。

In the codelabs, you'll learn how to use logs, traces, and metrics to get full visibility into your agent's decision-making process, allowing you to debug failures and understand why your agent behaves the way it does. In the second codelab, you'll learn how to evaluate your agents to score your agent's response quality and tool usage.

在代码实验里，你将学习如何用日志、追踪和指标，完整看见智能体的决策过程，从而调试失败，并理解智能体为什么会那样行动。在第二个代码实验里，你将学习如何评估智能体，为它的回答质量和工具使用打分。

### Day 4 Assignment

第 4 天作业

Complete Unit 4 - "Agent Quality":

完成第 4 单元：「智能体质量」：

- Listen to the [summary podcast episode](https://www.youtube.com/watch?v=LFQRy-Ci-lk) for this unit.

  收听本单元的[摘要播客](https://www.youtube.com/watch?v=LFQRy-Ci-lk)。

- To complement the podcast, read the updated ["Agent Quality" whitepaper](https://www.kaggle.com/whitepaper-agent-quality).

  作为播客的补充，阅读更新后的白皮书「[智能体质量](https://www.kaggle.com/whitepaper-agent-quality)」。

- Complete these codelabs on Kaggle:

  在 Kaggle 上完成这些代码实验：

  - [Implement observability to help you debug your agents.](https://www.kaggle.com/code/kaggle5daysofai/day-4a-agent-observability)

    [实现可观测性，帮助你调试智能体。](https://www.kaggle.com/code/kaggle5daysofai/day-4a-agent-observability)

  - [Evaluate your agents.](https://www.kaggle.com/code/kaggle5daysofai/day-4b-agent-evaluation)

    [评估你的智能体。](https://www.kaggle.com/code/kaggle5daysofai/day-4b-agent-evaluation)

- [Optional]: Watch the recorded [YouTube livestream](https://www.youtube.com/live/JW1Yybfxyr4). Kanchana Patlolla and Anant Nawalgaria were joined by codelab author Sita Lakshmi Sangameswaran, along with guests from Google: Wafae Bakkali, Turan Bulmus and Sian Gooding, and external guest Jiwei Liu from [NVIDIA](https://www.nvidia.com/).

  ［可选］：观看录制的 [YouTube 直播](https://www.youtube.com/live/JW1Yybfxyr4)。Kanchana Patlolla 和 Anant Nawalgaria 与代码实验作者 Sita Lakshmi Sangameswaran 一起参加，来自 Google 的嘉宾还有 Wafae Bakkali、Turan Bulmus 和 Sian Gooding，外部嘉宾是来自 [NVIDIA](https://www.nvidia.com/) 的 Jiwei Liu。

---

## Day 5 (Prototype to Production)

第 5 天（从原型到生产）

Welcome to Day 5.

欢迎来到第 5 天。

This whitepaper provides a technical guide to the operational lifecycle of AI agents, focusing on deployment, scaling and productionization. It explores the challenges of transitioning agentic systems from prototypes to enterprise-grade solutions, with special attention to Agent2Agent (A2A) Protocol.

这篇白皮书提供 AI 智能体运行生命周期的技术指南，重点是部署、扩展和生产化。它探讨把智能体系统 (Agentic System) 从原型过渡到企业级方案的挑战，并特别关注 A2A 协议。

In the codelabs, you'll learn how to build systems of multiple, independent agents that can communicate and collaborate using A2A Protocol. You'll also learn how to take your agent from your local machine to a production-ready, scalable service, by deploying your agent to Vertex AI Agent Engine on Google Cloud.

在代码实验里，你将学习如何构建由多个独立智能体组成的系统，让它们用 A2A 协议通信和协作。你还将学习如何把智能体从本地机器变成可投入生产、可扩展的服务：把智能体部署到 Google Cloud 上的 Vertex AI Agent Engine。

### Final Assignment

最终作业

Complete Unit 5 - "Prototype to Production":

完成第 5 单元：「从原型到生产」：

- Listen to the [summary podcast episode](https://www.youtube.com/watch?v=8Wyt9l7ge-g) for this unit.

  收听本单元的[摘要播客](https://www.youtube.com/watch?v=8Wyt9l7ge-g)。

- To complement the podcast, read the updated ["Prototype to Production" whitepaper](https://www.kaggle.com/whitepaper-prototype-to-production).

  作为播客的补充，阅读更新后的白皮书「[从原型到生产](https://www.kaggle.com/whitepaper-prototype-to-production)」。

- Complete these codelabs on Kaggle:

  在 Kaggle 上完成这些代码实验：

  - [Explore how to use A2A Protocol to have agents interact with each other.](https://www.kaggle.com/code/kaggle5daysofai/day-5a-agent2agent-communication)

    [探索如何用 A2A 协议让智能体彼此交互。](https://www.kaggle.com/code/kaggle5daysofai/day-5a-agent2agent-communication)

  - [[Optional] Deploy your agent to Agent Engine on Google Cloud.](https://www.kaggle.com/code/kaggle5daysofai/day-5b-agent-deployment)

    [[可选] 把你的智能体部署到 Google Cloud 上的 Agent Engine。](https://www.kaggle.com/code/kaggle5daysofai/day-5b-agent-deployment)

- [Optional]: Watch the recorded [YouTube livestream](https://www.youtube.com/live/4XjPh5or0ws). Kanchana Patlolla and Anant Nawalgaria were joined by codelab author Laxmi Harikumar, along with guests from Google: Will Grannis, Sokratis Kartakis, Elia Secchi and Saurabh Tiwary.

  ［可选］：观看录制的 [YouTube 直播](https://www.youtube.com/live/4XjPh5or0ws)。Kanchana Patlolla 和 Anant Nawalgaria 与代码实验作者 Laxmi Harikumar 一起参加，来自 Google 的嘉宾还有 Will Grannis、Sokratis Kartakis、Elia Secchi 和 Saurabh Tiwary。

---

## Congratulations on completing the Agents Intensive Learn Guide!

恭喜你完成智能体高强度学习指南！

## Happy Kaggling!

祝你在 Kaggle 上学习愉快！

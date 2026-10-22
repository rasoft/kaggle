# Coding agents in practice

实践中的编码智能体 (Coding Agent)

Navigating this 80% problem effectively requires applying the right tool to the right phase of work. A developer operating as a 'Conductor' needs a different set of tools than one operating as an 'Orchestrator'. To understand how to map these operational modes to your daily workflow, we must categorise the current landscape of AI agents based on their autonomy and integration.

要有效应对这个 80% 问题，就要把合适的工具用到合适的工作阶段。作为「指挥 (Conductor)」运作的开发者，需要的工具不同于作为「编排者 (Orchestrator)」运作的人。要理解如何把这些运作模式映射到日常工作流，我们必须按自主程度和集成方式，给当前的 AI 智能体 (Agent) 图景分类。

A developer building an agent today does most of the work from a terminal, often in natural language, often with another coding agent doing the typing. This is new. A year ago the same task meant frameworks, SDKs, and cloud consoles. The patterns that have replaced them are worth naming clearly, both for the developer who wants to use coding agents in their day, and for the developer who wants to build agents of their own.

今天构建智能体的开发者，大部分工作在终端里完成，常常用自然语言，常常由另一个编码智能体 (coding agent) 来打字。这是新的。一年前，同样的任务意味着框架、SDK 和云控制台。取代它们的模式值得说清楚，无论是想在日常里使用编码智能体的开发者，还是想构建自己的智能体的开发者。

---

## Where coding agents fit in the developer's day

编码智能体出现在开发者一天中的哪里

Coding agents show up in three places in everyday work. Most developers use all three at once.

编码智能体出现在日常工作的三个地方。大多数开发者同时用这三种。

In the editor: Inline completion that suggests the next line as the developer types. Chat panels that explain or modify code in place. Whole-codebase awareness inside the IDE. This is where most people first meet AI in coding, and where the work stays in flow. Examples include GitHub Copilot, Cursor, Windsurf, JetBrains AI Assistant.

在编辑器里：开发者打字时建议下一行的行内补全。就地解释或修改代码的对话面板。IDE 内部对整个代码库的感知。大多数人第一次在编码中遇见 AI，就是在这里，工作也停留在心流里。例子包括 GitHub Copilot、Cursor、Windsurf、JetBrains AI Assistant。

In the terminal: Coding agents that the developer launches from the command line, hand a goal to in plain language, and let work across the codebase. Full file system access, multi-file edits, the ability to run tools and tests and iterate based on results. This is where serious vibe coding happens today. Examples include Antigravity CLI, Claude Code, Codex CLI, Open Code, and Cline.

在终端里：开发者从命令行启动编码智能体，用白话交给它一个目标，让它在代码库上工作。完整的文件系统访问、多文件编辑，以及运行工具和测试、再根据结果迭代的能力。今天认真的氛围编码 (vibe coding) 发生在这里。例子包括 Antigravity CLI、Claude Code、Codex CLI、Open Code 和 Cline。

In the background: Agents that take a task and run autonomously in cloud-hosted sandboxes, often for hours, often producing a pull request as output. The developer hands off and reviews it later. Examples include Google Jules, GitHub Copilot agent mode, Cursor's background agents and Google's specialized AlphaEvolve agent for designing advanced algorithms.

在后台：接过任务、在云托管沙箱里自主运行的智能体，常常跑上几小时，产出常常是一个拉取请求 (pull request)。开发者交出去，稍后再评审。例子包括 Google Jules、GitHub Copilot 智能体模式、Cursor 的后台智能体，以及 Google 专门用来设计高级算法的 AlphaEvolve 智能体。

In practice, an editor agent helps when the developer is in the middle of writing code and wants suggestions, quick edits, or explanations without leaving flow. A terminal agent fits multi-file work, exploration of unfamiliar codebases, and tasks where the agent needs to run code and react to what it observes. A background agent fits well-specified tasks the developer can describe in a paragraph and walk away from, like fixing a known bug, generating a test suite, or migrating code from one framework to another. The same developer often uses all three in a single day.

实践中，编辑器智能体适合开发者正在写代码、又想要不离开心流就得到建议、快速编辑或解释的时候。终端智能体适合多文件工作、探索不熟悉的代码库，以及智能体需要运行代码并对观察到的结果做出反应的任务。后台智能体适合开发者能用一段话描述、然后走开的、规格清楚的任务，例如修复一个已知缺陷、生成一套测试，或把代码从一个框架迁移到另一个。同一个开发者常常在一天里把三种都用上。

The right starting point depends on the task, not on which category sits highest on some autonomy ladder.

正确的起点取决于任务，不取决于哪一类在某条自主性阶梯上站得最高。

---

## Vibe Coding Production-ready Agents

用氛围编码做出可上生产的智能体

Everything discussed so far has been about using coding agents to build software: writing features, fixing bugs, generating tests, refactoring code. But what happens when the thing you need to build is itself an agent?

到目前为止讨论的，都是用编码智能体来构建软件：写功能、修缺陷、生成测试、重构代码。但当你需要构建的东西本身就是一个智能体时，会发生什么？

A customer support bot that handles refund requests. A research assistant that cross-references sources and produces grounded reports. An internal tool that monitors compliance and flags anomalies. These are not tasks you solve with a coding agent in your terminal. They are products that need their own tools, their own memory, their own evaluation, and their own deployment infrastructure.

一个处理退款请求的客户支持机器人。一个交叉核对来源并产出有依据报告的研究助手。一个监控合规并标出异常的内部工具。这些不是你在终端里用编码智能体就能解决的任务。它们是产品，需要自己的工具 (Tools)、自己的记忆 (Memory)、自己的评估 (evaluation)，以及自己的部署基础设施。

The same terminal-based workflow that produces prototype scripts now reaches these production agents. Building, evaluating, and deploying a real agent that runs at scale, with persistent memory, governance, and observability, has moved from a framework and cloud console task into something that happens in the same terminal, often by talking to the same coding agent the developer was already using.

曾经产出原型脚本的那套基于终端的工作流，现在也延伸到这些生产智能体。构建、评估和部署一个真正能在规模上运行的智能体，带持久记忆、治理和可观测性，已经从框架加云控制台的任务，变成发生在同一个终端里的事，常常就是跟开发者已经在用的那个编码智能体说话。

This workflow matters when the builder needs an agent that runs reliably for real users: persistent memory across sessions, scoped permissions on tools and data, eval coverage that catches regressions before they ship, observability that traces what the agent actually did. For one-off scripts or personal automation, a regular coding agent is enough; the agent is the destination. For agents that serve real users at scale, the agent is the product, and it needs the substrate underneath.

当构建者需要一个为真实用户可靠运行的智能体时，这套工作流才要紧：跨会话的持久记忆，工具和数据上划定范围的权限，在发布前抓住回归的评估覆盖，以及追踪智能体实际做了什么的可观测性。对一次性脚本或个人自动化，普通的编码智能体就够了；智能体是目的地。对在规模上服务真实用户的智能体，智能体是产品，它需要底下的基底。

Google's Agents CLI is built around this idea.<sup>14</sup> It is a small command-line tool that bundles a set of skills for building agents on Google Cloud, and crucially, it works with whichever coding agent the developer prefers, Claude Code, Codex, or another. After a one-time install, the coding agent gains seven new skills covering the full ADK lifecycle: scaffolding a project, writing the agent code, evaluating it, deploying it to Agent Runtime, and wiring up observability. The developer does not learn a new SDK. They describe what they want, and the coding agent uses the skills to do the right thing at each step.

Google 的 Agents CLI 就是围绕这个想法构建的。<sup>14</sup> 它是一个小的命令行工具，打包了一组在 Google Cloud 上构建智能体的技能 (Skill)，而且关键在于，它能配合开发者偏好的任何一个编码智能体，Claude Code、Codex 或其他。一次安装之后，编码智能体获得七个新技能，覆盖智能体开发套件 (Agent Development Kit, ADK) 的完整生命周期：搭建项目骨架、编写智能体代码、评估它、把它部署到 Agent Runtime，并接上可观测性。开发者不学新的 SDK。他们描述想要什么，编码智能体用这些技能在每一步做对的事。

Concretely, the entire build-evaluate-deploy loop looks like this:

具体来说，整个构建、评估、部署循环是这样的：

```text
# One-time setup
uvx google-agents-cli setup
# Then in your coding agent:
> Build a support agent that answers questions from our docs.
> evaluate it on the FAQ dataset
> Deploy it to Agent Engine
```

**Snippet 1: Agents CLI Setup and Build.**

片段 1：Agents CLI 的安装与构建。

Behind that single instruction, the coding agent scaffolds a project from a template, writes the ADK code, generates an evalset, runs it against the agent, deploys to Agent Runtime, and reports back. For developers who prefer to drive directly, the same operations are available as plain CLI commands (`agents-cli create`, `agents-cli playground`, `agents-cli eval`, `agents-cli deploy`).

在那一条指令背后，编码智能体从模板搭建项目，编写 ADK 代码，生成评估集 (evalset)，对照智能体运行它，部署到 Agent Runtime，然后回报。喜欢直接驾驶的开发者，同样的操作也可以用普通 CLI 命令完成（`agents-cli create`、`agents-cli playground`、`agents-cli eval`、`agents-cli deploy`）。

Production agents used to require a separate stack and a separate workflow from prototypes. Now the prototype that ran on the developer's laptop yesterday can become the production agent serving real users today, without a rewrite.

生产智能体曾经需要与原型分开的技术栈和工作流。现在，昨天还在开发者笔记本上跑的原型，今天就可以成为服务真实用户的生产智能体，不必重写。

The same workflow scales from one agent to many. ADK provides graph-based workflows, multi-agent workflows for building collaborative agents and interaction mechanisms like shared session state, LLM-driven delegation, and explicit invocation, that combine into whatever multi-agent pattern fits the problem.

同一套工作流可以从一个智能体扩展到许多个。ADK 提供基于图的工作流、用于构建协作智能体的多智能体工作流，以及共享会话状态、由大语言模型 (LLM) 驱动的委派和显式调用这类交互机制。它们组合成适合问题的任何多智能体模式。

Coordination across agents happens through shared session state for simple cases, through Model Context Protocol (MCP) for tool access, and through the Agent2Agent (A2A) protocol for cross-agent delegation.<sup>15</sup> Anthropic's engineering team published an experiment in early 2026 in which agent teams running on this kind of architecture built a working C compiler in Rust over two weeks, with humans setting direction and reviewing output but not writing the implementation.<sup>16</sup> The bottleneck moved from writing the code to specifying what it should do and verifying that the agents did it.

智能体之间的协调，简单情况下通过共享会话状态，工具访问通过模型上下文协议 (Model Context Protocol, MCP)，跨智能体委派通过智能体对智能体 (Agent2Agent, A2A) 协议。<sup>15</sup> Anthropic 工程团队在 2026 年初发表了一项实验：跑在这类架构上的智能体团队用两周时间，用 Rust 构建出一个能工作的 C 编译器，人设定方向并评审输出，但不写实现。<sup>16</sup> 瓶颈从写代码，移到了规定它该做什么，并验证智能体确实做了。

For builders, the practical implication is simple. The same vibe coding workflow that produces a script today produces a production agent tomorrow. The lifecycle, build, evaluate, deploy, observe, refine, lives in one place. The path from idea to running agent has collapsed from weeks to hours, and most of the work now happens in natural language.

对构建者来说，实际含义很简单。今天产出一个脚本的同一套氛围编码工作流，明天就产出一个生产智能体。生命周期，构建、评估、部署、观察、打磨，都住在一个地方。从想法到运行中的智能体，路径从几周塌缩到几小时，而且大部分工作现在发生在自然语言里。

The practices that make this workflow production-grade at team scale, from spec-driven development and structured code review to guardrails, sandboxing, and zero-trust development, are covered in the Day 5 companion paper: Spec-Driven Production Grade Development in the Age of Vibe Coding.

让这套工作流在团队规模上达到生产级的实践，从规格驱动开发和结构化代码评审，到护栏 (Guardrails)、沙箱化和零信任开发，写在第 5 天的配套论文里：《氛围编码时代的规格驱动生产级开发》。

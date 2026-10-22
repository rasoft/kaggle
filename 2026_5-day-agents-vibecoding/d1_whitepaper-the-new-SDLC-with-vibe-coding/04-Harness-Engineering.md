# Harness Engineering: What surrounds the model

驾驭层工程 (Harness Engineering)：模型周围是什么

If the developer is the factory manager, the AI model is merely the raw engine on the factory floor. An engine on its own cannot manufacture a car; it needs belts, gears, safety sensors, and an assembly line. In the context of AI-assisted development, this surrounding machinery is known as the Harness.

如果开发者是工厂经理，AI 模型 (Model) 就只是厂房里那台裸引擎。引擎自己造不出汽车；它需要皮带、齿轮、安全传感器和一条装配线。在 AI 辅助开发的语境里，这周围的机械被称为驾驭层 (Harness)。

There is a temptation, when builders start working with AI agents, to treat the model as the system. A new model comes out, the agent gets smarter. An older model and the agent gets worse. The model becomes the explanation for everything good and bad.

构建者开始与 AI 智能体 (Agent) 共事时，很容易把模型当成整个系统。新模型出来，智能体就更聪明。换回旧模型，智能体就变差。模型成了对一切好坏的解释。

That intuition is wrong, and it leads to the wrong investments. The model is one input into a running agent. Everything else, the prompts, the tools, the context policies, the hooks, the sandboxes, the sub-agents, the observability, is the harness: the scaffolding wrapped around the model that lets it actually finish something.<sup>11</sup>

这个直觉是错的，而且会导向错误的投入。模型只是运行中的智能体的一项输入。其余一切，提示、工具 (Tools)、上下文策略、钩子 (hooks)、沙箱 (sandbox)、子智能体、可观测性，才是驾驭层：包在模型外面、让它真正能把事情做完的脚手架。<sup>11</sup>

A useful equation:

一个有用的等式：

![Agent equals Model plus Harness](image_007_page_26.png)

智能体 = 模型 + 驾驭层（Agent = Model + Harness）。

A raw model is not an agent. It becomes one once a harness gives it state, tool execution, feedback loops, and enforceable constraints. The behaviour developers experience when working with Claude Code, Cursor, Codex, Antigravity, Aider, or Cline is dominated by what the harness does, not just by which model is underneath.

裸模型不是智能体。驾驭层给它状态、工具执行、反馈回路和可强制的约束之后，它才成为智能体。开发者在使用 Claude Code、Cursor、Codex、Antigravity、Aider 或 Cline 时体验到的行为，主要由驾驭层做什么决定，不只是底下是哪一个模型。

![Figure 7: Harness Anatomy](2026_5-day-agents-vibecoding/d1_whitepaper-the-new-SDLC-with-vibe-coding/images/image_008_page_27.png)

图 7：驾驭层解剖。智能体 = 模型 + 驾驭层。模型约占 10%，驾驭层约占 90%。核心是 LLM，周围是指令与规则文件、工具与 MCP 服务器、编排逻辑、护栏与钩子。向外是框架层（智能在这里被塑造）、开发者界面（CLI / IDE 集成）、云基础设施（托管运行时、部署配置、服务与伸缩），两侧还有会话与记忆存储、评估与测试、可观测性与追踪。模型是引擎。驾驭层是车、路和交通规则。

---

## What's in the harness

驾驭层里有什么

Concretely, a harness includes:

具体来说，驾驭层包括：

- Instructions and Rule Files: The text that defines who the agent is, what it cares about, and what it is forbidden from doing. This includes AGENTS.md, CLAUDE.md, GEMINI.md, skill files, and sub-agent prompts.

指令与规则文件：定义智能体是谁、在意什么、禁止做什么的文本。其中包括 AGENTS.md、CLAUDE.md、GEMINI.md、技能文件和子智能体提示。

- Tools: The functions, MCP servers, and APIs the agent can call, plus the prose around them that tells the model when and how to call them.

工具：智能体可以调用的函数、模型上下文协议 (Model Context Protocol, MCP) 服务器和 API，以及周围告诉模型何时、如何调用它们的说明文字。

- Sandboxes and execution environments: Where the agent's code actually runs, what it has access to, what it cannot reach.

沙箱与执行环境：智能体的代码实际在哪里跑，它能访问什么，它到不了什么。

- Orchestration logic: Sub-agent spawning, model routing, hand-offs between specialists, and the rules that govern when each one fires.

编排逻辑：拉起子智能体、模型路由 (model routing)、专家之间的交接，以及决定每一个何时触发的规则。

- Guardrails or Hooks: Deterministic code that runs at specific lifecycle points: before a tool call, after a file edit, before a commit. Hooks are the place for things the agent should never forget but often does.

护栏 (Guardrails) 或钩子：在特定生命周期点运行的确定性代码，例如工具调用之前、文件编辑之后、提交之前。钩子是放那些智能体绝不该忘、却经常忘记的事情的地方。

- Observability: Logs, traces, evaluations, cost and latency metering. Without observability, there is no way to tell whether the agent is doing well or quietly drifting.

可观测性：日志、追踪、评估 (evaluation)、成本与延迟计量。没有可观测性，就无法判断智能体是在做好，还是在悄悄漂移。

If that sounds like a lot of surface area, it is. And it is the team's surface area, not the model provider's.

如果这听起来表面积很大，那确实很大。而且这是团队的表面积，不是模型提供商的。

---

## Harness in SDLC

驾驭层在 SDLC 中

While the model itself determines how to accomplish a task, the harness is the scaffolding that provides access to the tools, sandboxes, and orchestration needed to execute it. Therefore, this harness must be present in every phase where an AI agent operates.

模型本身决定如何完成一项任务，驾驭层则是提供工具、沙箱和编排的脚手架，执行才成为可能。因此，AI 智能体运作的每一个阶段，都必须有这层驾驭层在场。

Here is how the harness actively operates across the different phases of the new SDLC:

驾驭层在新 SDLC 的各个阶段里是这样实际运作的：

### 1. Requirements, Planning, & Architecture (Configuring the Harness)

1. 需求、规划与架构（配置驾驭层）

This is where the harness is configured and calibrated. Before the AI writes any production code, the developer must set up the agent's environment.

这是配置和校准驾驭层的地方。在 AI 写下任何生产代码之前，开发者必须把智能体的环境搭好。

- Harness Configuration: Providing the Instructions and Rule Files (e.g., creating the AGENTS.md and defining architectural constraints) that the harness will load and make available to the model.

驾驭层配置：提供指令和规则文件（例如创建 AGENTS.md，并定义架构约束），驾驭层会加载它们，并提供给模型。

- The Action: The developer defines the tools the agent will have access to (like specific APIs or database schemas) and sets the fundamental rules the agent cannot break.

动作：开发者定义智能体将能访问的工具（例如特定 API 或数据库模式），并设定智能体不能打破的基本规则。

### 2. Implementation (Running the Harness)

2. 实现（运行驾驭层）

During active coding, the harness acts as the boundary that keeps the AI model focused, secure, and productive.

在实际编码期间，驾驭层充当边界，让 AI 模型保持专注、安全和有产出。

- Harness Components Used: Sandboxes, Execution Environments, and Tools.

用到的驾驭层组件：沙箱、执行环境和工具。

- The Action: As the model generates code, it executes it within the harness's isolated sandbox. If the model needs to read a file or search the web, it uses the tools provided by the harness.

动作：模型生成代码时，在驾驭层隔离的沙箱里执行它。如果模型需要读文件或搜索网页，它使用驾驭层提供的工具。

### 3. Testing & QA (The Feedback Loop)

3. 测试与质量保证（反馈回路）

Testing in an agentic workflow relies heavily on the harness to facilitate autonomous self-correction.

智能体工作流里的测试，严重依赖驾驭层来促成自主的自我纠正。

- Harness Components Used: Orchestration Logic and Guardrails.

用到的驾驭层组件：编排逻辑和护栏。

- The Action: When the agent writes a function, the harness provides the execution environment (such as a sandboxed terminal) that allows the automated tests to be executed. If a test fails, the orchestration logic captures the error output from that environment and routes it back to the model, asking it to try again. The harness is what creates this automated 'think -> act -> observe' loop.

动作：智能体写下一个函数时，驾驭层提供执行环境（例如沙箱终端），让自动化测试得以运行。如果测试失败，编排逻辑从那个环境捕获错误输出，送回模型，让它再试一次。正是驾驭层创造出这条自动化的「思考 → 行动 → 观察」循环。

### 4. Code Review, Deployment, & Maintenance (Observing the Harness)

4. 代码评审、部署与维护（观察驾驭层）

Even after the code is written, the harness ensures the agent behaves safely in live or near-live environments.

即使代码已经写完，驾驭层仍保证智能体在线上或接近线上的环境里安全行事。

- Harness Components Used: Hooks and Observability.

用到的驾驭层组件：钩子和可观测性。

- The Action: The harness runs deterministic hooks (e.g., blocking a commit if the agent tries to push a hard-coded password). Furthermore, the observability layer tracks token costs, latency, and agent drift, allowing human engineers to audit exactly why an agent made a specific deployment decision.

动作：驾驭层运行确定性钩子（例如，如果智能体试图推送硬编码的密码，就阻止提交）。此外，可观测性层跟踪 token 成本、延迟和智能体漂移，让人类工程师能够审计智能体为什么做出某一次具体的部署决策。

---

The transition from 'vibe coding' to 'agentic engineering' is not simply about the tools you use—a developer can vibe code or apply agentic engineering using the exact same agent. Instead, it is defined by how deliberately you configure and apply the harness. Vibe coding relies on minimal or implicit scaffolding aimed purely at rapid implementation. Agentic engineering relies on clear, extensive harness abstractions that guide the AI from the very first planning document all the way through to production monitoring.

从「氛围编码 (vibe coding)」到「智能体工程 (agentic engineering)」的转变，并不只是你用什么工具。开发者可以用完全同一个智能体去做氛围编码，也可以用它做智能体工程。差别在于你配置和应用驾驭层有多刻意。氛围编码依赖最少的、或隐式的脚手架，目标纯粹是快速实现。智能体工程依赖清楚、充分的驾驭层抽象，从第一份规划文档一直引导 AI 到生产监控。

The impact of this deliberate configuration is highly measurable. Public benchmarks make the size of the harness effect concrete. On Terminal Bench 2.0, one team moved a coding agent from outside the Top 30 to the Top 5 by changing only the harness, with no model change at all. A separate study at LangChain raised a coding agent's score on the same benchmark by 13.7 points by tweaking only the system prompt, tools, and middleware around a fixed model.

这种刻意配置的影响高度可测。公开基准把驾驭层效应的规模变得具体。在 Terminal Bench 2.0 上，有一个团队只改驾驭层、完全不改模型，就把一个编码智能体从 30 名开外抬进前 5。LangChain 的另一项研究只调整固定模型周围的系统提示、工具和中间件，就让同一基准上的编码智能体分数提高了 13.7 分。

The everyday version of this observation is crucial for teams adopting AI across the SDLC: when an agent does something wrong, the first instinct is to blame the model. More often, the failure traces back to a missing tool, a vague rule, an absent guardrail, or a context window stuffed with noise. Most agent failures, examined honestly, are configuration failures.

这个观察的日常版本，对在整个 SDLC 里采用 AI 的团队至关重要：智能体做错事时，第一反应是怪模型。更常见的是，失败可以追溯到一个缺失的工具、一条含糊的规则、一道缺席的护栏，或一个塞满噪声的上下文窗口。诚实地检查，大多数智能体失败都是配置失败。

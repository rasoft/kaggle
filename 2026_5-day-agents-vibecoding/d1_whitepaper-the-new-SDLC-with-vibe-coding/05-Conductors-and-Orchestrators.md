# The developer's evolving role: conductors and orchestrators

<mark>开发者角色的演变：指挥 (Conductor) 与编排者 (Orchestrator)</mark>

As AI takes over more of the implementation work, the developer's role is transforming in ways that are both exciting and disorienting. We find it useful to think of two modes that developers move between fluidly: conductor and orchestrator.<sup>12</sup>

<mark>随着 AI 接管更多实现工作，开发者的角色正在以既令人兴奋、又令人迷失的方式转变。我们觉得，把开发者在其间流畅切换的两种模式想成指挥 (conductor) 和编排者 (orchestrator)，是有用的。<sup>12</sup></mark>

![Figure 8: Conductor vs. Orchestrator](image_009_page_32.png)

<mark>图 8：指挥与编排者，与 AI 智能体 (Agent) 共事的两种模式。不是二选一，而是依任务两者都用。指挥是实时、同步、在 IDE 内：开发者发提示，智能体生成代码，开发者在行内评审，智能体再打磨。适合探索性编码、原型和学习新 API。编排者是异步、高层、多智能体：开发者定义具体任务，智能体独立工作，开发者评审 PR 或输出并批准或纠正。适合功能实现、迁移和测试生成。大多数开发者在细粒度控制和高杠杆委派之间流畅移动。</mark>

---

## The conductor: hands-on, real-time direction

<mark>指挥：亲手、实时的引导</mark>

In conductor mode, a developer works in real-time with an AI pair-programmer. They're in the IDE, watching code appear, guiding the AI with prompts and corrections, and maintaining fine-grained control over what gets written. The AI is a powerful instrument, but the developer is actively directing every movement.

<mark>在指挥模式下，开发者与一个 AI 结对程序员实时工作。人在 IDE 里，看着代码出现，用提示和纠正引导 AI，并对写下的内容保持细粒度控制。AI 是一件强有力的乐器，但每一个动作都由开发者主动指挥。</mark>

This mode is typical when working on complex logic, debugging tricky issues, or working in unfamiliar codebases where the developer needs to understand each change as it's made. Tools like GitHub Copilot, Google's Gemini Code Assist, Cursor, and Windsurf primarily support this mode through inline completions, chat interfaces, and edit-in-place capabilities.

<mark>处理复杂逻辑、调试棘手问题，或在不熟悉的代码库里工作时，这种模式很典型，因为开发者需要在每次改动发生时就理解它。GitHub Copilot、Google 的 Gemini Code Assist、Cursor 和 Windsurf 这类工具，主要通过行内补全、对话界面和原地编辑来支持这种模式。</mark>

The conductor mode is natural for developers who come from traditional engineering backgrounds. It preserves the sense of understanding and control that many engineers value. The risk is that it can also become a bottleneck - if the developer is personally directing every keystroke, the throughput improvement from AI is limited.

<mark>指挥模式对来自传统工程背景的开发者很自然。它保留了许多工程师看重的理解感和控制感。风险是它也可能变成瓶颈：如果开发者亲自指挥每一次按键，AI 带来的吞吐提升就有限。</mark>

---

## The orchestrator: async, multi-agent delegation

<mark>编排者：异步、多智能体委派</mark>

In orchestrator mode, the developer operates at a higher level of abstraction. They define goals, assign them to agents, and review results - but they're not watching code appear line by line. Agents may be working in the background, in parallel, on different parts of a codebase. The developer checks in periodically, reviews output, and provides course corrections.

<mark>在编排者模式下，开发者在更高的抽象层上运作。他们定义目标，把目标分配给智能体，并评审结果，但并不一行行看着代码出现。智能体可能在后台、并行地、在代码库的不同部分工作。开发者定期查看，评审输出，并提供航向修正。</mark>

This mode is typical for well-defined tasks like bug fixes, feature implementations against established patterns, codebase migrations, and test generation. Tools like Google's Jules, GitHub Copilot's agent mode, Cursor's background agents, and Claude Code support this mode through async task execution, often working in sandboxed environments with full access to the repository, build tools, and test suites.<sup>13</sup>

<mark>这种模式典型地用于定义清楚的任务，例如缺陷修复、按既有模式实现功能、代码库迁移和测试生成。Google 的 Jules、GitHub Copilot 的智能体模式、Cursor 的后台智能体和 Claude Code 通过异步任务执行支持这种模式，通常在沙箱环境里工作，并能完整访问仓库、构建工具和测试套件。<sup>13</sup></mark>

The orchestrator mode requires a different skill set. Instead of deep expertise in syntax and language idioms, it demands strong skills in:

<mark>编排者模式需要另一套技能。它要求的不是对语法和语言惯用法的深厚专长，而是这些方面的强能力：</mark>

- Specification: Defining tasks precisely enough that an agent can execute them without ambiguity

<mark>规格：把任务定义得足够精确，使智能体能没有歧义地执行</mark>

- Decomposition: Breaking large tasks into appropriately sized units for agent execution

<mark>分解：把大任务拆成适合智能体执行的尺寸</mark>

- Evaluation: Quickly assessing whether agent output meets quality standards

<mark>评估 (Evaluation)：迅速判断智能体输出是否达到质量标准</mark>

- System design: Designing the constraints, tests, and feedback loops that keep agents productive

<mark>系统设计：设计让智能体保持有产出的约束、测试和反馈回路</mark>

---

## The 80% problem

<mark>80% 问题</mark>

A persistent challenge in AI-assisted development is what we call the 80% problem: AI agents can rapidly generate approximately 80% of the code for a feature, but the remaining 20% - the edge cases, error handling, integration points, and subtle correctness requirements - demands deep contextual knowledge that current models often lack.<sup>14</sup>

<mark>AI 辅助开发里一个持久的挑战，是我们所说的 80% 问题：AI 智能体可以迅速生成一个功能大约 80% 的代码，但剩下的 20%，边界情况、错误处理、集成点和微妙的正确性要求，需要当前模型常常缺少的深层上下文知识。<sup>14</sup></mark>

The nature of AI errors has evolved from simple syntax mistakes to more insidious conceptual failures: wrong assumptions about business logic, failure to seek clarification on ambiguous requirements, missing edge cases, and architectural decisions that create subtle long-term maintenance burdens. These errors are harder to detect precisely because the code "looks right" and may even pass basic tests.

<mark>AI 错误的性质已经从简单的语法错误，演变成更隐蔽的概念失败：对业务逻辑的错误假设，在含糊需求上不去澄清，漏掉边界情况，以及造成微妙长期维护负担的架构决策。这些错误更难发现，恰恰因为代码「看起来是对的」，甚至可能通过基本测试。</mark>

The developers who navigate this challenge most effectively adopt a specific posture: they use AI for what it's good at (rapid implementation of well-specified tasks) while reserving their own attention for what AI struggles with (ambiguous requirements, architectural trade-offs, and correctness verification). They don't try to be faster by accepting everything the AI produces. They try to be faster by focusing their expertise where it matters most.

<mark>最有效地应对这一挑战的开发者采取一种特定姿态：他们把 AI 用在它擅长的地方（迅速实现规格清楚的任务），把自己的注意力留给 AI 吃力的地方（含糊的需求、架构权衡和正确性验证）。他们并不靠照单全收 AI 的产出而试图更快。他们靠把专长集中在最要紧的地方而试图更快。</mark>

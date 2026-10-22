# The Economics of AI Development

AI 开发的经济学

When evaluating the impact of AI on the software development life cycle, the conversation often begins and ends with developer velocity: how fast can we write code? However, for engineering leaders, the more critical metric is the Total Cost of Ownership (TCO).

评估 AI 对软件开发生命周期的影响时，对话常常从开发者速度开始，也在那里结束：我们能多快写出代码？但对工程负责人来说，更关键的指标是总拥有成本 (Total Cost of Ownership, TCO)。

To understand the true cost of AI-assisted development, we must look at how different workflows shift the financial and operational burdens between Capital Expenditure (CapEx)—the upfront investment to build something—and Operational Expenditure (OpEx)—the ongoing cost to run, fix, and maintain it. Crucially, in the AI era, OpEx is heavily dictated by the token economy.

要理解 AI 辅助开发的真实成本，必须看不同工作流如何在资本支出 (Capital Expenditure, CapEx) 和运营支出 (Operational Expenditure, OpEx) 之间转移财务与运营负担。资本支出是为了构建某样东西的前期投入。运营支出是运行、修复和维护它的持续成本。关键在于，在 AI 时代，运营支出在很大程度上由 token 经济决定。

![Figure 9: The Economics of AI Development](image_010_page_40.png)

图 9：AI 开发的经济学。横轴是时间与已交付的功能，纵轴是累计总拥有成本。氛围编码前期资本支出低，靠速度拿到第一份输出，但提示税、维护税、安全风险、上下文坍塌和 token 消耗会让曲线陡增。交叉点之后，氛围编码每个功能的成本高出 3 到 10 倍。智能体工程前期平台投入更高，之后靠抓住回归，以可持续的规模保持低边际运行成本。右侧对照：氛围编码约 12% 是资本支出、其余是高运行成本；智能体工程约 12% 是运营支出、其余是前期平台设计。

---

## The Hidden Debt of Vibe Coding (Low CapEx, High OpEx)

氛围编码的隐性债务（低资本支出，高运营支出）

At first glance, vibe coding appears incredibly cost-effective. The barrier to entry is essentially zero: a standard monthly subscription to an AI assistant and a few casual prompts. The CapEx is negligible because the developer relies entirely on the model's baseline capabilities rather than investing time in system design.

乍一看，氛围编码 (vibe coding) 极其划算。进入门槛基本上是零：一份标准的 AI 助手月度订阅，加上几条随意的提示。资本支出可以忽略，因为开发者完全依赖模型 (Model) 的基线能力，而不是把时间投进系统设计。

However, the economics of vibe coding hide a massive, compounding OpEx burden:

然而，氛围编码的经济账藏着一笔巨大、会复利的运营支出负担：

- The Token Burn Rate: Every interaction with a Large Language Model (LLM) incurs a cost based on input and output tokens. In vibe coding, developers often dump massive, unstructured files into the context window and repeatedly ask the model to fix its own unverified mistakes. This creates an expensive "prompting loop" that burns through API tokens with low first-pass success rates.

Token 燃烧率：每一次与大语言模型 (LLM) 的交互，都按输入和输出 token 计费。在氛围编码里，开发者常常把巨大的、无结构的文件倒进上下文窗口，并反复让模型去修它自己未经验证的错误。这造成昂贵的「提示循环」，以很低的一次通过率烧光 API token。

- Maintenance Tax: Code written through ad-hoc prompting often lacks structural consistency. When a bug arises six months later, human engineers must spend days reverse-engineering unstructured, AI-generated "spaghetti" code.

维护税：靠临时提示写出的代码常常缺少结构一致性。六个月后出现缺陷时，人类工程师必须花上几天，去逆向那些无结构的、AI 生成的「意大利面」代码。

- Security Remediation: Without an automated evaluation harness, the rapid generation of code leads to the rapid generation of vulnerabilities. The cost of fixing a security flaw in production is exponentially higher than catching it during the design phase.

安全补救：没有自动化的评估驾驭层 (evaluation harness)，代码的快速生成就会带来漏洞的快速生成。在生产环境修复一个安全缺陷的成本，比在设计阶段抓住它要高出指数级。

---

## The Investment of Agentic Engineering (High CapEx, Low OpEx)

智能体工程的投入（高资本支出，低运营支出）

Agentic engineering flips this economic model. It requires a deliberate, upfront investment of engineering time and resources before a single line of production code is generated.

智能体工程 (agentic engineering) 把这个经济模型翻过来。在生成一行生产代码之前，它要求对工程时间和资源做一次刻意的前期投入。

The CapEx in agentic engineering includes designing API schemas, building deterministic test suites, and, most importantly, structuring the agent's context. While this upfront cost is higher, the marginal cost of shipping and maintaining a feature drops dramatically. The AI operates within a strictly governed "factory," meaning its output is structurally sound, pre-tested, and aligned with company standards.

智能体工程里的资本支出包括设计 API 模式、构建确定性测试套件，以及最重要的，结构化智能体 (Agent) 的上下文。前期成本更高，但交付和维护一个功能的边际成本会急剧下降。AI 在一座被严格治理的「工厂」里运作，这意味着它的输出结构健全、预先测试过，并与公司标准对齐。

---

## Context Engineering as a Financial Lever

作为财务杠杆的上下文工程

In the token economy, context engineering is not just a technical skill—it is a financial strategy. LLMs charge for every piece of information you send them. Passing an entire 100,000-token repository into every prompt is financially unviable at scale.

在 token 经济里，上下文工程 (context engineering) 不只是一项技术技能，它是一种财务策略。大语言模型对你发给它们的每一份信息收费。把整个 10 万 token 的仓库塞进每一次提示，在规模上财务上不可行。

Effective context engineering ensures the model receives a dense, high-signal payload (such as a precise AGENTS.md file and architectural guardrails) rather than a sprawling, noisy one. By providing the right context upfront, developers dramatically increase the agent's first-pass success rate, avoiding the costly trial-and-error loops that plague vibe coding.

有效的上下文工程确保模型收到一份稠密、高信号的载荷（例如一份精确的 AGENTS.md 和架构护栏），而不是一份铺开的、嘈杂的载荷。事先提供正确的上下文，开发者会大幅提高智能体的一次通过率，避开困扰氛围编码的、昂贵的试错循环。

---

## Scaling Efficiency via Dynamic Context and Skills

用动态上下文和技能扩展效率

To truly optimize OpEx, advanced agentic engineering relies on dynamic context through the use of "skills" or tool calling (such as Model Context Protocol servers) which we cover in detail in day-3 paper.

要真正优化运营支出，进阶的智能体工程依赖动态上下文，办法是使用「技能 (skills)」或工具调用 (tool calling)（例如模型上下文协议服务器）。我们在第 3 天的论文里详细讨论。

---

## Intelligent Model Routing

智能模型路由 (Model Routing)

Furthermore, agentic engineering allows for intelligent model routing. In a vibe coding workflow, a developer typically relies on a single, massive frontier model for every interaction—paying premium token prices just to ask the AI to fix a typo or generate a basic unit test.

此外，智能体工程允许智能模型路由 (model routing)。在氛围编码工作流里，开发者通常每一次交互都依赖一个巨大的前沿模型，哪怕只是让 AI 改一个错字或生成一个基本单元测试，也支付溢价 token。

A well-designed factory model avoids this waste. It uses large, advanced models for highly complex tasks (Requirements, Architecture, and initial Implementation) but automatically routes deterministic, lower-complexity tasks (Test Generation, Code Review, and CI/CD monitoring) to smaller, faster, and significantly cheaper models. By orchestrating a multi-model ecosystem, engineering teams can maintain peak output quality while systematically driving down the operational token cost.

设计良好的工厂模型 (factory model) 避开这种浪费。它把大而先进的模型用于高度复杂的任务（需求、架构和最初的实现），但自动把确定的、复杂度较低的任务（测试生成、代码评审和 CI/CD 监控）路由到更小、更快、便宜得多的模型。通过编排一个多模型生态，工程团队可以保持峰值输出质量，同时系统性地压低运营 token 成本。

# 5. From Prototype to Production

5. 从原型到生产

Sections 1 to 4 covered what skills are, how to write one, and how to evaluate them. This section is about what changes when you put a working prototype in front of a real customer. The short version: the model is no longer the interesting part, and skills are the engineering primitive that lets you ship reliably.

第 1 节到第 4 节讲了技能 (Skill) 是什么、怎么写、怎么评估。这一节讲的是：当你把一个能跑的原型放到真实客户面前，什么会变。短版本是：模型 (Model) 不再是有意思的部分，技能才是让你可靠交付的工程原语。

Google's Agents CLI<sup>17</sup> in Agent Platform is a CLI and skills package for building, evaluating, and deploying AI agents on Google Cloud. Agents are built with Google's Agent Development Kit (ADK) and Agents CLI handles everything around it: scaffolding, evaluation, deployment, and observability.

Agent Platform 里的 Google Agents CLI<sup>17</sup> 是一套 CLI 和技能包，用来在 Google Cloud 上构建、评估和部署 AI 智能体 (Agent)。智能体用 Google 的 Agent Development Kit（ADK）构建，Agents CLI 处理周围的一切：脚手架、评估 (Evaluation)、部署和可观测性。

![Agents CLI install flow](image_005_page_29.png)

[图片_005：Agents CLI 安装流程 - 第 29 页]

Figure 5: The Agents CLI install flow. One uvx command installs seven skills into the developer's existing coding agent, covering the full agent lifecycle (workflow, ADK code, scaffold, eval, deploy, publish, observability). The same skills work across Claude Code, Codex CLI, Antigravity, and any other compliant coding agent.

图 5：Agents CLI 的安装流程。一条 uvx 命令把 7 个技能装进开发者已有的编码智能体，覆盖完整的智能体生命周期（工作流、ADK 代码、脚手架、评估、部署、发布、可观测性）。同一套技能可以在 Claude Code、Codex CLI、Antigravity，以及任何其他兼容的编码智能体上工作。

The working example points to three properties that generalize beyond Google’s setup:

这个能跑的例子指出三个可以推广到 Google 这套方案之外的性质：

- The expertise lives in the skills, not the runtime. The runtime is commoditized; the seven skills are the durable asset.

专长住在技能里，不住在运行时里。运行时 (runtime) 已经商品化；这 7 个技能才是耐久资产。

- The skills package composes with what you already use. Install the skills and your existing coding tool gains new capabilities; the same pattern to aim for internally: capabilities that compose into existing tooling, not another portal.

技能包和你已经在用的东西组合。装上技能，现有的编码工具就获得新能力。对内也该瞄准同一种模式：能力组合进现有工具，而不是再做一个门户。

- The full lifecycle ships as skills. Scaffold, build, evaluate, deploy, publish, observe. Every stage that once needed its own tooling now fits the skills format.

完整生命周期以技能的形式交付。脚手架、构建、评估、部署、发布、观察。曾经每个阶段都要自己的工具，现在都装得进技能格式。

---

## What's actually inside an agent runtime

智能体运行时里实际有什么

Underneath the framework, the agent loop has converged across vendors: the runtime maintains a conversation, calls the model, executes tools, reads files, returns a response. What’s striking inside one of these runtimes is how little of the code is about reasoning.

框架底下，智能体循环已经在各厂商之间收敛：运行时维持对话，调用模型，执行工具 (Tools)，读文件，返回响应。这些运行时内部令人吃惊的是，有多少代码其实跟推理 (Reasoning) 无关。

A recent reverse-engineering of Claude Code v2.1.88 (Liu, Zhao, Shang, and Shen, 2026)<sup>18</sup> found that 98.4% of the codebase is operational infrastructure: permission classifiers, context compaction pipelines, subagent delegation, session storage and only 1.6% is the agent loop itself. The model sits behind a remote API; the engineering around it is what makes the system production-grade. The companion site ccunpacked.dev maps the same architecture visually.

最近对 Claude Code v2.1.88 的逆向工程（Liu、Zhao、Shang 与 Shen，2026）<sup>18</sup> 发现，代码库的 98.4% 是运维基础设施：权限分类器、上下文压缩流水线、子智能体委派、会话存储；只有 1.6% 是智能体循环本身。模型坐在远程 API 后面；让系统达到生产级的，是周围的工程。配套网站 ccunpacked.dev 把同一套架构画了出来。

This is the architectural insight behind everything that follows. As foundation models converge in baseline reasoning, the differentiator for autonomous reliability becomes the deterministic engineering around the model and inside that engineering, the unit that gets composed and reused is the skill.

这是后面一切内容背后的架构洞见。当基础模型在基线推理上收敛，自主可靠性的差异化就变成模型周围的确定性工程；而在这套工程内部，被组合、被复用的单位就是技能。

![The demo-to-deploy confidence gap](image_006_page_31.png)

[图片_006：从演示到部署的信心落差 - 第 31 页]

Figure 6: The demo-to-deploy gap. Team confidence peaks early, then collapses on contact with a real customer environment. The instinct is to call it a model problem; it almost never is.

图 6：从演示到部署的落差。团队信心很早达到峰值，一接触真实客户环境就崩掉。本能是把它叫成模型问题；它几乎从来不是。

---

## Why skills are the unit of improvement

为什么技能是改进的单位

The naive theory of agent improvement is that better models produce better agents. In production, the model is the infrastructure and skills are the primitive that lets improvements ship. Each new skill is a small, owned, testable unit of capability (as we set up in Section 1). When a new edge case appears, it takes editing one SKILL.md; the agent's effective capability grows without the challenges of monolithic prompt engineering.

关于智能体改进的朴素理论是：更好的模型产出更好的智能体。在生产里，模型是基础设施，技能才是让改进能够交付的原语。每个新技能都是一小块有主人、可测试的能力单元（第 1 节已经铺垫过）。新的边界情况出现时，改一份 SKILL.md 就够了；智能体的有效能力在增长，却不必承受单体提示词工程的难题。

Three properties of skills make this work:

技能有三个性质让这件事成立：

- They are conditional. Loaded only when their description matches the task.

它们是有条件的。只有 description 匹配任务时才加载。

- They are composable. One skill can call tools from another, or chain downstream, without either knowing about the other (Section 7 develops the composition story in depth).

它们是可组合的。一个技能可以调用另一个技能的工具，或向下游串联，双方都不必知道对方（第 7 节会把组合这件事讲深）。

- They are owned. Each lives in a versioned folder with a clear author, so improvement is distributed rather than bottlenecked through a central platform team.

它们是有主人的。每个技能住在一个有版本、作者清楚的文件夹里，所以改进是分布式的，而不是卡在中央平台团队这个瓶颈上。

Compare against the alternatives:

拿它和替代方案比一比：

| Improvement style | Cycle time | Failure mode | Who can do it | Context Tax |
| --- | --- | --- | --- | --- |
| Model swap | Days to weeks | Regression in unrelated tasks | ML/platform team | None (weights-based) |
| System prompt edit | Minutes to hours | Context rot, instruction conflict | Whoever owns the prompt file | Static (every turn pays) |
| Fine-tune | Weeks to months | Catastrophic forgetting, overfitting | ML team only | None (weights-based) |
| New skill | Hours to days | Bounded with only matching turns | Any domain team | Dynamic (loaded on-demand when triggered) |

表 2：智能体改进方法的对比，涵盖周期、失败模式、组织所有权和上下文成本。

| 改进方式 | 周期 | 失败模式 | 谁能做 | 上下文税 |
| --- | --- | --- | --- | --- |
| 更换模型 | 数天到数周 | 无关任务上的回归 | 机器学习 / 平台团队 | 无（基于权重） |
| 修改系统提示词 | 数分钟到数小时 | 上下文腐烂 (Context Rot)、指令冲突 | 谁拥有提示词文件，谁就能改 | 静态（每一轮都付） |
| 微调 | 数周到数月 | 灾难性遗忘、过拟合 | 只有机器学习团队 | 无（基于权重） |
| 新增技能 | 数小时到数天 | 有界，只影响匹配的轮次 | 任何领域团队 | 动态（触发时按需加载） |

Table 2: Comparison of agent improvement methodologies across cycle times, failure modes, organizational ownership, and context costs.

表 2：从周期、失败模式、组织所有权和上下文成本，比较智能体改进方法。

---

## The failure mode that breaks demos: context overflow

让演示翻车的失败模式：上下文溢出 (Context Overflow)

The most common failure mode of agents in production is not hallucination. It is context overflow: the model receiving more context than it can effectively use, and degrading silently before the operator notices. Two strands of research ground this:

生产中智能体最常见的失败模式不是幻觉。它是上下文溢出：模型收到的上下文多过它能有效使用的量，并在操作者察觉之前静静变差。有两条研究支撑这一点：

Lost in the Middle (Liu et al., TACL 2024)<sup>19</sup>. Across multi-document QA and retrieval, performance is highest when relevant information sits at the start or end of the input and degrades in the middle; a U-curve that holds even for models trained on long contexts.

Lost in the Middle（Liu 等人，TACL 2024）<sup>19</sup>。在多文档问答和检索中，相关信息位于输入开头或结尾时表现最高，位于中间时下降；这条 U 形曲线即使对在长上下文上训练过的模型也成立。

Context Rot (Chroma Research, 2025)<sup>20</sup>. Across 18 frontier models; Claude 4 Opus and Sonnet, Gemini 2.5, Qwen3; performance degrades as input grows, even when task difficulty is held constant. Every model gets worse, and faster when relevant content is hard to distinguish from distractors. The noise typical of real agent contexts (tool outputs, half-relevant retrievals, intermediate reasoning) is among the worst.

上下文腐烂（Chroma Research，2025）<sup>20</sup>。在 18 个前沿模型上——Claude 4 Opus 与 Sonnet、Gemini 2.5、Qwen3——输入变长时表现下降，即便任务难度保持不变。每个模型都会变差；当相关内容和干扰项难以区分时，变差得更快。真实智能体上下文里典型的噪声（工具输出、半相关的检索、中间推理）属于最糟的那一类。

![Context rot as prompt size grows](image_007_page_33.png)

[图片_007：提示变长时的上下文腐烂 - 第 33 页]

Figure 7: Context rot in practice. As prompt size grows, accuracy on a fixed task degrades, long before the context window fills. The dashed line shows the naive expectation; the curve shows what 18 frontier models actually do (Liu et al. 2024; Chroma 2025).

图 7：实践中的上下文腐烂。提示变长时，固定任务上的准确率下降，而且远在上下文窗口填满之前。虚线是朴素预期；曲线是 18 个前沿模型实际的表现（Liu 等人 2024；Chroma 2025）。

---

## What this means for the token budget

这对 token 预算意味着什么

Progressive disclosure, covered in Section 2, is the architectural answer: metadata for every skill loads at startup, a skill’s body loads only when its description matches, and supporting files load only when the body references them.

第 2 节讲过的渐进式披露 (Progressive Disclosure) 就是架构上的答案：每个技能的元数据在启动时加载，技能正文只在 description 匹配时加载，支撑文件只在正文引用它们时加载。

The math is worth showing. Consider an agent with fifty distinct workflows. As a single system prompt, it loads 15,000 tokens every turn. As a skills library, it loads ~4,000 tokens of descriptions plus the ~2,000-token body of the one active skill with ~6,000 tokens total, with the other forty-nine bodies on disk. Anthropic has published examples where converting a workflow to skills cut active context from roughly 150,000 tokens to 2,000, a reduction of more than 98 percent.

这道算术值得写出来。考虑一个有 50 条不同工作流的智能体。做成一份系统提示词，它每一轮加载 15,000 token。做成技能库，它加载约 4,000 token 的描述，加上当前活跃技能约 2,000 token 的正文，合计约 6,000 token，其余 49 份正文留在磁盘上。Anthropic 发表过例子：把一条工作流改成技能后，活跃上下文从大约 150,000 token 降到 2,000，降幅超过 98%。

![Token economics of one prompt versus a skill library](image_008_page_34.png)

[图片_008：一份大提示词与技能库的 token 经济学 - 第 34 页]

Figure 8: Token economics: a single big prompt versus a fifty-skill library. The library has fifty units of capability available, but only the active body sits in context at any moment.

图 8：Token 经济学：一份大提示词对比一个 50 技能库。技能库有 50 个可用的能力单元，但任何时刻只有活跃的正文坐在上下文里。

Three practical implications follow:

由此有三条实践含义：

- Capacity is the wrong metric. A 1M-token window can show significant degradation at 50K tokens.

容量是错误的指标。一个 100 万 token 的窗口，在 5 万 token 时就可能明显变差。

- Active context is a budget, not a vessel. Every token in front of the model takes attention from every other. Treat the system prompt the way infra teams treat memory: a finite resource, allocated deliberately.

活跃上下文是预算，不是容器。放在模型面前的每一个 token，都在抢走其他 token 的注意力。对待系统提示词，要像基础设施团队对待内存：它是有限资源，要有意地分配。

- Skills resolve the constraint. They keep active context small while keeping available capability effectively unbounded.

技能解开这个约束。它们把活跃上下文保持得很小，同时让可用能力实际上不受限。

Once a team has a working library, the questions shift from maintaining a single skill to evolution, composition, and the larger ecosystem.

一旦团队有了一个能用的技能库，问题就从维护单个技能，转向演化、组合，以及更大的生态。

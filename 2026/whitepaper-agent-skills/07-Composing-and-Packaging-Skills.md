# 7. Composing and Packaging Skills

<mark>7. 组合与打包技能</mark>

Real workflows do not fit inside a skill. The composition problem is how skills reference each other, pass state, and avoid circular dependencies.

<mark>真实工作流装不进单个技能 (Skill)。组合问题是：技能如何互相引用、如何传递状态，以及如何避免循环依赖。</mark>

Passing raw LLM outputs between isolated skills in a monolithic system is ineffective: state gets obfuscated, execution becomes non-deterministic, and debugging is hard. Agent architecture has evolved from naive prompt chaining to predictable orchestration.

<mark>在一个单体系统里，把原始的大语言模型 (LLM) 输出在彼此隔离的技能之间传来传去，是无效的：状态被搅浑，执行变成非确定性的，调试也很难。智能体 (Agent) 架构已经从朴素的提示词串联，演化成可预测的编排 (Orchestration)。</mark>

---

## Execution Routing: DAG Orchestration

<mark>执行路由：有向无环图编排 (DAG Orchestration)</mark>

Early architectures proved brittle and susceptible to compounding errors when early stages hallucinated. The industry solution is Directed Acyclic Graph (DAG) orchestration.

<mark>早期架构很脆。前面阶段一旦幻觉，错误就会复合放大。业界的解法是有向无环图 (Directed Acyclic Graph, DAG) 编排。</mark>

- Decoupled State: State routing in a DAG architecture does not rely on accumulating execution history within the LLM's prompt.

<mark>解耦状态：DAG 架构里的状态路由，不依赖把执行历史堆进大语言模型的提示词。</mark>

- File Message Bus: The DAG controller orchestrates handoffs by passing structured schema references between subagent nodes.

<mark>文件消息总线：DAG 控制器通过在子智能体节点之间传递结构化的 schema 引用，来编排交接。</mark>

- Protected Attention: Abstracting the payload from the model's text input prevents context window bloat and preserves the model's capacity.

<mark>受保护的注意力：把载荷从模型 (Model) 的文本输入里抽走，可以防止上下文窗口臃肿，并保住模型的容量。</mark>

---

## Environment Packaging: Capability Profiles

<mark>环境打包：能力画像 (Capability Profile)</mark>

Activating every skill degrades natural language routing and overwhelms the context window. Architects should utilize tools to manage "Capability Profiles," which function as specialized personas tailored to specific execution states. A profile acts as a modular tool bundle defining:

<mark>把每个技能都激活，会劣化自然语言路由，并淹没上下文窗口。架构师应该用工具 (Tools) 来管理「能力画像」。它们是针对特定执行状态定制的专职人格。一份画像是一个模块化的工具包，定义：</mark>

- Active skills and tool access.

<mark>活跃的技能和工具访问权限。</mark>

- System instructions and operational guardrails.

<mark>系统指令和操作护栏。</mark>

- Automated workflows and subagent topologies.

<mark>自动化工作流和子智能体拓扑。</mark>

- LLM parameters, such as model choice and temperature.

<mark>大语言模型参数，例如模型选择和 temperature。</mark>

During execution, the orchestration layer unloads previous system instructions and flushes stale variables before swapping the new Capability Profile into memory. This strict teardown and rebuild process prevents context loss.

<mark>执行期间，编排层先卸下先前的系统指令、冲掉过期变量，再把新的能力画像换进内存。这种严格的拆除再重建，防止上下文丢失。</mark>

---

## Populating the Graph: The Canonical Skill Taxonomy

<mark>填充图：规范的技能分类</mark>

To build DAG, discrete engineering capabilities map to specific node functions within an execution graph nodes:

<mark>要构建 DAG，离散的工程能力要映射到执行图里的具体节点功能：</mark>

- Generator: Convert user intent into structured artifacts.

<mark>生成器 (Generator)：把用户意图转换成结构化制品。</mark>

- Reviewer & Gate: Deterministic gates blocking execution if validation fails.

<mark>审阅者与门禁 (Reviewer & Gate)：确定性门禁，校验失败就挡住执行。</mark>

- Pipeline: Orchestrate linear paths within the broader DAG environment.

<mark>流水线 (Pipeline)：在更大的 DAG 环境里编排线性路径。</mark>

- Inversion & Recovery: Force the agent to clarify assumption before execution.

<mark>倒置与恢复 (Inversion & Recovery)：在执行前迫使智能体澄清假设。</mark>

- Domain Context Wrappers: Act as reference nodes teaching domain conventions.

<mark>领域上下文包装器 (Domain Context Wrapper)：作为参考节点，教领域约定。</mark>

---

## Context Debt and Shifting Intelligence Left

<mark>上下文债务 (Context Debt) 与智能左移 (Shift Intelligence Left)</mark>

Skills burn model attention, which is a scarce resource. When authors attempt deterministic behavior at runtime by bloating skill descriptions (e.g., "ALWAYS DO X"), they accumulate Context Debt. Models learn to ignore these capitalized imperatives, exactly as a human developer ignores a wall of unreadable warning text.

<mark>技能消耗模型注意力，而注意力是稀缺资源。作者若想在运行时靠把技能描述写胖来得到确定性行为（例如「ALWAYS DO X」），就会积累上下文债务。模型会学会忽略这些全大写的命令，正如人类开发者会忽略一堵读不下去的警告文本。</mark>

The engineering best practice is to Shift Intelligence Left. Instead of hoping an LLM correctly interprets complex rules at runtime, distill subjective judgments into skills. By pushing logic out of the LLM's prompt and into standard, testable scripts, you reduce the chaotic surface area of your application.

<mark>工程上的最佳实践是智能左移。不要指望大语言模型在运行时正确解释复杂规则，而是把主观判断蒸馏进技能。把逻辑从大语言模型的提示词里推出去，推进标准的、可测试的脚本，你就缩小了应用里混乱的表面积。</mark>

---

## Architectural Tradeoffs

<mark>架构权衡</mark>

| Architecture | Mechanism | Primary Benefit | Best For |
| --- | --- | --- | --- |
| Linear Pipelines | Sequential text passing between fixed nodes. | Low engineering overhead and rapid prototyping. | Single-domain, low-complexity generative tasks. |
| DAG Orchestration | Graph-based parallel execution with file-bus state passing via schema references. | Cycle prevention and strict context isolation. | Multi-agent workflows requiring high reliability. |
| Capability Profiles | Swappable, version-controlled parameter and tool bundles. | Rapid persona switching with lifecycle memory purging. | Role-based deployment and domain-specific agents. |

<mark>表 3：多智能体技能系统中，线性流水线、DAG 编排与能力画像的架构权衡。</mark>

| <mark>架构</mark> | <mark>机制</mark> | <mark>主要收益</mark> | <mark>最适合</mark> |
| --- | --- | --- | --- |
| <mark>线性流水线</mark> | <mark>在固定节点之间顺序传递文本。</mark> | <mark>工程开销低，原型快。</mark> | <mark>单领域、低复杂度的生成任务。</mark> |
| <mark>DAG 编排</mark> | <mark>基于图的并行执行，经 schema 引用在文件总线上传递状态。</mark> | <mark>防止成环，并严格隔离上下文。</mark> | <mark>要求高可靠性的多智能体工作流。</mark> |
| <mark>能力画像</mark> | <mark>可替换、有版本控制的参数与工具包。</mark> | <mark>快速切换人格，并在生命周期内清除记忆。</mark> | <mark>基于角色的部署，以及领域专用智能体。</mark> |

Table 3: Architectural Tradeoffs among Linear Pipelines, DAG Orchestration, and Capability Profiles in multi-agent skill systems.

<mark>表 3：多智能体技能系统中，线性流水线、DAG 编排与能力画像之间的架构权衡。</mark>

---

## Actionable Best Practices

<mark>可执行的最佳实践</mark>

- Write Software, Not Rules: Replace negative LLM instructions with deterministic software constraints that make invalid actions impossible.

<mark>写软件，不写规矩：用确定性的软件约束替换否定式的大语言模型指令，让非法动作根本不可能发生。</mark>

- Implement Progressive Disclosure: Load complex instructions dynamically only when the skill is explicitly invoked.

<mark>实现渐进式披露 (Progressive Disclosure)：复杂指令只在技能被明确调用时动态加载。</mark>

- Decouple State: Never use the LLM context window as a database. Pass only URIs or pointers to the subagents via the file system or message bus.

<mark>解耦状态：永远不要把大语言模型的上下文窗口当数据库。只通过文件系统或消息总线，把 URI 或指针传给子智能体。</mark>

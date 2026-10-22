# From agents to contractors

从智能体到承包方

The common interface to define AI agents across various tools and platforms today is very simple, and usually includes specifying the goal, some textual instructions, the tools that the agent can use, and a set of examples. While this might be sufficient to prototype demos, it leads to potentially underspecified definitions, and might be one of the leading reasons that AI agents can struggle to get from prototype-to-production.

今天，在各种工具 (Tools) 和平台上定义 AI 智能体 (Agent) 的通用接口非常简单，通常包括指定目标、一些文本指令、智能体可以使用的工具，以及一组示例。这或许足以做出演示原型，但会导致定义可能欠指定，而这也许是 AI 智能体难以从原型走到生产的主要原因之一。

We propose to evolve the Agent interface to evolve them into "Contract adhering agents" which are aimed at solving complex tasks using AI Agents, more specifically in contexts where stakes are high.

我们建议演进智能体接口，把智能体演进为「遵循合约的智能体 (Contract-adhering Agent)」，旨在使用 AI 智能体解决复杂任务，更具体地说，针对利害关系很高的场景。

---

## Contracts

合约 (Contract)

The key idea of contractors is to specify and standardize the contracts between the requester and the agents, making it possible to:

承包方 (Contractor) 的核心想法，是明确并标准化请求方与智能体之间的合约，从而能够：

1. Define the outcomes as precisely as possible, similarly to what we would do in a real world scenario when agreeing on a service with a company we are contracting to do something for us. This allows the agent (contractor) to validate against the desired outcomes and iterate until the desired objective is achieved.

1. 尽可能精确地定义结果，就像在真实世界的场景中，我们与一家公司就一项服务达成约定、委托对方为我们做事时那样。这样，智能体（承包方）就能对照期望结果进行验证，并迭代直到达成期望目标。

2. Make it possible to negotiate the task as well as clarifying and refining it, in order to avoid any ambiguity in the definition, and fill any gap in common understanding of the goals.

2. 使任务可以被协商，同时加以澄清和细化，以避免定义中的任何歧义，并补上各方对目标的共同理解中的缺口。

3. Define the rules for the contractors to generate new subcontracts needed to solve the bigger one in a standard fashion (cf. section below on subcontracts).

3. 为承包方规定规则，使其能够以标准方式生成解决更大合约所需的新子合约（参见下文关于子合约的小节）。

Table 3: An example data model for the contracts.

表 3：合约的一种示例数据模型。

Contract, initial definition

合约，初始定义

| Fields | Description | Required |
| --- | --- | --- |
| Task/Project description | Provide a detailed description of what we expect the contractor to achieve. It should be as specific and as unambiguous as possible. | Yes |
| Deliverables & Specifications | Describe precisely the expected outcomes and deliverables from the contractor's task, including a list of specifications clarifying what makes the deliverable acceptable as outcome and details on how to verify that the deliverable is fulfilling the expectation. | Yes |
| Scope | Clarify the scope of the tasks that the contractor is responsible for completing, going into separate detail about every aspect of the task. Also used to clarify what is out of scope. | No |
| Expected Cost | Gives expectation in terms of cost for the task completion. This is usually a function of the complexity of the task combined with what tools will be used. | Yes |
| Expected Duration | Gives expectation in terms of duration for the task completion. | Yes |
| Input Sources | Specify what input sources can be used and considered to be useful to complete the task. | No |
| Reporting and Feedback | Specifies how the feedback loop should look like: how often we expect updates on the progress, and what mechanism/surface is used to provide feedback (emails, APIs, etc.). | Yes |

| 字段 | 说明 | 是否必需 |
| --- | --- | --- |
| 任务 / 项目描述 | 详细描述我们期望承包方达成什么。描述应尽可能具体，也尽可能无歧义。 | 是 |
| 交付物与规格 | 精确描述承包方任务的预期结果和交付物，包括一份规格清单，说明怎样的交付物才算可接受的结果，并给出如何验证该交付物符合预期的细节。 | 是 |
| 范围 | 阐明承包方负责完成的任务范围，并对任务的每个方面分别详述。也可用来说明哪些不在范围内。 | 否 |
| 预期成本 | 给出完成任务的成本预期。这通常是任务复杂度与将使用的工具相结合的函数。 | 是 |
| 预期时长 | 给出完成任务的时长预期。 | 是 |
| 输入来源 | 指明哪些输入来源可以使用，并被视为对完成任务有用。 | 否 |
| 报告与反馈 | 规定反馈回路应当是什么样子：我们期望多久获得一次进展更新，以及用什么机制 / 界面提供反馈（电子邮件、API 等）。 | 是 |

Table 4: An example data model for the iteration of messaging between contractors.

表 4：承包方之间消息迭代的一种示例数据模型。

Contract Iteration: Feedback & Negotiation

合约迭代：反馈与协商

| Fields | Description | Required |
| --- | --- | --- |
| Underspecification | Highlight aspects that are underspecified or need clarification from the task initiator. | No |
| Cost negotiation | Cost considered too high to complete the task. | No |
| Risk | Highlights potential risks in fulfilling the contract. | No |
| Additional input needed | Express the kinds of additional data or information that would be useful to fulfill the contract. | No |

| 字段 | 说明 | 是否必需 |
| --- | --- | --- |
| 欠指定 | 标出那些欠指定或需要任务发起方澄清的方面。 | 否 |
| 成本协商 | 完成任务的成本被认为过高。 | 否 |
| 风险 | 标出履行合约时的潜在风险。 | 否 |
| 所需额外输入 | 说明哪些额外的数据或信息会有助于履行合约。 | 否 |

---

## Contract Lifecycle

合约生命周期

The following illustration shows the lifecycle of defining, negotiating and executing the contract:

下图展示定义、协商和执行合约的生命周期：

![A diagram of the agent as contractor lifecycle from Agentspace](image_016_page_49.png)

[图 13：智能体作为承包方的生命周期，来自 Agentspace。流程从顶部实心圆开始，经「合约已提交」进入合约评估，评估可行性、成本与时长。若请求修订，则进入左侧的合约修订，对歧义、成本等提出修改建议；若接受合约，则进入右侧的合约执行，生成计划、执行任务并生成子合约。合约修订经「合约修订被接受或拒绝」进入合约执行。合约执行向上产出合约交付物，并向右侧回环「子合约已生成」。合约执行向下进入任务求解，其中包括候选生成、候选评审、候选评分、候选排序和候选演化；任务求解可以「建议修订」并回到合约修订，也可以返回合约执行。]

---

## Contract execution

合约执行

This requires the contractor runtime to be able to fulfill the contracts and solve the tasks behind contracts according to their defined specifications. Prioritizing quality and completeness over latency enables to fully leverage the capabilities of LLMs, for example by generating different solutions, and reviewing, scoring, and evolving them. An example of this methodology is shown below in the Co-Scientist study. The engine can iterate and self-validate the results and deliverables based on the provided expectations, and can improve and self-correct until the validators are fulfilled. The ability to concretely validate a solution against a set of objective criteria has proven to work extremely well in the context of AI and has been at the core of successful AI systems such as for example Alpha-Code.

这要求承包方运行时能够履行合约，并按照已定义的规格解决合约背后的任务。把质量和完整性置于延迟之上，才能充分发挥大语言模型 (LLM) 的能力，例如生成不同的解决方案，并对它们进行评审、评分和演化。这一方法的一个例子见下文的 Co-Scientist 研究。引擎可以依据所给预期，对结果和交付物进行迭代和自验证，并不断改进、自我纠正，直到验证条件得到满足。能够针对一组客观标准具体地验证解决方案，这在 AI 场景中已被证明极其有效，并且一直处于成功 AI 系统的核心，例如 Alpha-Code。

---

## Contract Negotiation

合约协商

One core hypothesis behind contracts in the context of automation agents specifically is that many tasks in the enterprise world can draw significant benefit from leveraging the power of LLMs when used in a less-constrained manner (latency and cost wise).

具体到自动化智能体这一场景，合约背后的一个核心假设是：企业世界里的许多任务，如果以约束更少的方式（就延迟和成本而言）运用大语言模型的能力，就能从中获得显著收益。

Being able to tackle more and more complex tasks and making it possible for customers to be able to rely on and trust the results of contractors will ensure real value for companies. Even that being said, we need to have a notion of relative priority in order to make sure that tasks are appropriately prioritized as well as resources fairly allocated. We thus introduce a notion of cost (typically relative per customer or contract initiator) which can be discussed and negotiated between the contract initiator and the contractor, in order to make sure that the contract receives the adequate resources relative to the other contracts initiated by the contract initiator. The contractors can also negotiate other aspects of the contracts, for example in terms of specification and deliverables (cf. also section below on feedback).

能够处理越来越复杂的任务，并让客户能够依赖并信任承包方的结果，将为公司确保真正的价值。即便如此，我们仍需要相对优先级这一概念，以确保任务得到恰当的优先排序，资源也得到公平分配。因此我们引入成本这一概念（通常是相对于每个客户或每个合约发起方而言），它可以在合约发起方与承包方之间讨论和协商，以确保该合约相对于合约发起方所发起的其他合约，获得与之相称的资源。承包方也可以协商合约的其他方面，例如规格和交付物（另见下文关于反馈的小节）。

---

## Contract Feedback

合约反馈

Contracts give a vehicle to provide feedback and in particular resolve ambiguities. As tasks become more and more complex, it is critical to be able to raise ambiguities or other issues related to the tasks specifications as early as possible. Contractors can give feedback on the contract just after having received the contract (initial contract assessment), and then at a frequency predefined in the contract.

合约提供了一种载体，用来给出反馈，尤其是用来消解歧义。随着任务越来越复杂，必须尽早提出与任务规格相关的歧义或其他问题。承包方可以在刚收到合约之后就对合约给出反馈（初始合约评估），此后再按合约中预先规定的频率进行。

This feedback will contain clarification requests, or other types of feedback about the underspecification or misspecification of tasks (inconsistencies, conflicting specs, clarification, etc.).

这类反馈会包含澄清请求，或其他关于任务欠指定或误指定的反馈（不一致、规格冲突、澄清等）。

---

## Subcontracts

子合约

Although not part of the contract definition and specification directly, the ability to decompose a task into subtasks by generating subcontracts is a core concept that will be used to power the contractors' engine.

尽管并不直接属于合约的定义和规格，通过生成子合约把任务分解为子任务的能力，是用来驱动承包方引擎的一个核心概念。

When a task is considered too complex to be tackled directly, contractors can decide to decompose the task into smaller and easier tasks, which will be added to the execution queue for solving. This is made possible only through the contract formalization described above, which makes it possible for the contractors to generate, process and manipulate other contracts in a uniform and standardized way.

当一项任务被认为过于复杂、无法直接处理时，承包方可以决定把任务分解为更小、更容易的任务，并加入执行队列以待求解。这之所以可能，完全是因为上文所述的合约形式化：它使承包方能够以统一、标准化的方式生成、处理并操作其他合约。

---

## Google's Co-Scientist: A Case Study in Multi-Agent Intelligence

Google 的 Co-Scientist：多智能体智能的一个案例

Google's AI co-scientist is a prime example of a multi-agent LLM system applied to scientific research. This system utilizes a team of specialized agents, each with its own role and expertise, to accelerate the pace of scientific discovery. These agents collaborate to generate, evaluate, and refine hypotheses, mirroring the iterative process of scientific inquiry.

Google 的 AI co-scientist 是把多智能体大语言模型系统用于科学研究的一个典型例子。该系统使用一组专门化的智能体，每个智能体有自己的角色和专长，以加快科学发现的步伐。这些智能体协作生成、评估并提炼假说，映照科学探究的迭代过程。

The co-scientist system employs a "generate, debate, and evolve" approach, drawing inspiration from the scientific method. This approach involves generating diverse hypotheses, critically evaluating their potential, and refining them through ongoing feedback and analysis. The system leverages the strengths of different LLMs, each specializing in a particular aspect of the research process, to achieve a more comprehensive and robust outcome.

co-scientist 系统采用「生成、辩论和演化」方法，灵感来自科学方法。这一方法包括生成多样的假说，批判性地评估它们的潜力，并通过持续的反馈和分析加以提炼。系统借助不同大语言模型的长处，每一种都专攻研究过程的某一特定方面，从而得到更全面、更稳健的结果。

For instance, in a study on liver fibrosis treatments, the co-scientist not only identified existing drugs but also proposed new mechanisms and promising drug candidates, demonstrating its potential to generate novel insights. Some of its major components are:

例如，在一项关于肝纤维化治疗的研究中，co-scientist 不仅识别出已有药物，还提出了新的机制和有前景的候选药物，显示了它产生新洞见的潜力。它的一些主要组成部分是：

- Data Processing Agents: aggregate and structure large volumes of experimental data.

- 数据处理智能体：汇聚并结构化大量实验数据。

- Hypothesis Generators: propose potential explanations based on existing research and new findings.

- 假说生成器：基于已有研究和新发现，提出可能的解释。

- Validation Agents: run simulations and verify results before presenting them to researchers.

- 验证智能体：运行模拟，并在呈现给研究人员之前核实结果。

- Collaboration Agents: communicate findings across different research teams, enhancing interdisciplinary cooperation.

- 协作智能体：在不同研究团队之间传达研究发现，加强跨学科合作。

![A process diagram of the AI co-scientist system](image_017_page_53.png)

[图 14：AI co-scientist 系统的过程图<sup>31</sup>。标题为 AI co-scientist 的系统设计。最左侧是科学家：以自然语言指定研究目标，也可提出自己的想法与提案、提供反馈和评审，并通过聊天界面引导系统。向右是科学家输入：研究目标（连同偏好、实验约束和其他属性），以及添加想法、评审想法、讨论研究；其下是研究提案与概览，把排名靠前的研究假说和提案汇总成研究概览，分享给科学家，并有箭头回到科学家。中间大框是 AI co-scientist 多智能体系统：研究计划配置指向生成智能体（文献探索、模拟科学辩论）；排序智能体锦标赛对研究假说进行比较和排序，把局限性与顶尖胜负模式汇总后反馈给其他智能体，形成自我改进回路，并以蓝色回路箭头连向反思智能体、演化智能体和邻近检查智能体；反思智能体包含结合网页搜索的全文评审、模拟评审、锦标赛评审和深度核实；演化智能体包含从其他想法获得灵感、简化和研究扩展；邻近检查智能体连接元评审智能体，由后者拟定研究概览，向左返回研究提案与概览，并向右连接记忆。最右侧是 AI co-scientist，持续生成、评审、辩论并改进研究假说和提案，朝着科学家给出的研究目标推进；其下是工具使用（搜索、其他工具）。]

This approach exemplifies how multi-agent architectures move beyond static AI interactions, instead fostering dynamic, evolving intelligence capable of handling sophisticated tasks in research, enterprise automation, and knowledge management.

这一方法例证了多智能体架构如何超越静态的 AI 交互，进而培育出动态的、不断演化的智能，使之能够处理研究、企业自动化和知识管理中的复杂任务。

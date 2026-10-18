# 3. Why did Agent Skills become so popular, so fast?

<mark>3. 智能体技能为什么这么快就流行起来？</mark>

Imagine it's early 2025. You are asked to build a system that offload repetitive back office work: generating slide decks from briefs while adhering to the company style, parsing structured invoicing PDFs, drafting HR onboarding guides, summarising weekly compliance reports, and tackling a long tail of similar tasks that will inevitably grow as the team finds new things to automate.

<mark>设想现在是 2025 年初。你被要求做一个系统，把重复的后台工作卸下来：按公司风格把简报生成幻灯片，解析结构化的发票 PDF，起草人力资源入职指南，汇总每周合规报告，还要对付一长串同类任务。团队不断找到新的自动化对象，这条长尾只会更长。</mark>

Most likely, you would have defaulted to a multi-agent architecture. A router agent at the top dispatching to a handful of specialist sub-agents beneath it. You would then spend agonizing hours on CI/CD pipelines, orchestration logic, and ensuring that a deployment for the new HR sub-agent didn't break the invoice sub-agent.

<mark>你多半会默认做成多智能体架构。顶上一个路由智能体 (Agent)，把活派给下面若干专家子智能体。然后你会在 CI/CD 流水线、编排 (Orchestration) 逻辑上耗掉痛苦的好几个小时，还要保证新的人力资源子智能体一部署，不会把发票子智能体弄坏。</mark>

With the release of Agent Skills, this workflow becomes vastly simpler. This friction is exactly how the Skill format was first created by Anthropic, with the first skills for reading PDFs and creating slides<sup>6</sup>, which represents a much lighter version to accomplish this. Instead of a router dispatching subagents, you have one agent with a library of skills. Skills can run commands, call MCP servers, and bundle Python scripts. The agent decides which to load when. You maintain skills, not agents, and the operational surface can shrink.

<mark>智能体技能 (Agent Skill) 发布之后，这条工作流简单了很多。正是这种摩擦，让 Anthropic 最初做出了技能格式。最早的技能用来读 PDF 和做幻灯片<sup>6</sup>，以轻得多的方式完成同一件事。不再是路由器去派发子智能体，而是一个智能体加上一个技能库。技能可以跑命令、调用 MCP 服务器、打包 Python 脚本。智能体决定何时加载哪一个。你维护的是技能，不是智能体，运维面可以缩小。</mark>

> To be very clear: Agent Skills do not kill multi-agent architectures.

<mark>需要说清楚：智能体技能并不会淘汰多智能体架构。</mark>

Multi-agent remains the absolute right answer when you have genuine parallelism, real capability boundaries (different access, different security postures, different external systems), hierarchical decomposition where the abstraction layers actually differ, adversarial or check-and-balance setups, sub-agent intercommunication, or heterogeneous models. This list isn't exhaustive.

<mark>当你真的需要并行、真的存在能力边界（不同的访问权限、不同的安全姿态、不同的外部系统）、抽象层次确实不同的层次分解、对抗或制衡设置、子智能体之间的通信，或异构模型 (Model) 时，多智能体仍然是完全正确的答案。这份清单并不穷尽。</mark>

What Skills did was introduce a missing architectural primitive. Many systems that were built multi-agent by default can now be elegantly simplified to single-agent-with-skills by design.

<mark>技能所做的，是补上一个缺失的架构原语。许多默认做成多智能体的系统，现在可以按设计优雅地简化成「单智能体加技能」。</mark>

---

## Skills for chatbots, for coding agents, or for multi-agent enterprise use cases?

<mark>技能是给聊天机器人、编码智能体，还是给企业级多智能体场景用的？</mark>

The first publicly visible skills were AI chatbot-shaped. The coding-agent narrative arrived within days or weeks. And once it did, skills exploded. They landed straight into the vibe-coding fever and turned out to be the format developers had been wanting.

<mark>最早公开可见的技能，形状像 AI 聊天机器人。编码智能体的叙事在几天到几周内到来。它一到，技能就爆发了。它们直接掉进了 vibe coding（氛围编程）的热潮，而且正好是开发者一直想要的格式。</mark>

In some multi-agentic architectures, by definition, each sub-agent is already a specialist. A research agent might not need a research skill. Skills are more useful in scenarios when one general-purpose agent has the flexibility to become a specialist across different things, by design. However, there might be cases where multi-agent and skills do compose well, for example, if there is a need for each specialized agent to have its own scoped skill library.

<mark>在某些多智能体架构里，按定义，每个子智能体已经是专家。一个研究智能体也许不需要一个研究技能。技能更有用的场景，是一个通用智能体按设计就有灵活性，在不同事情上变成专家。不过，多智能体和技能也可以组合得很好。例如，每个专职智能体都需要自己范围内的技能库。</mark>

Now consider a logistics company with 100 process variants depending on product type, tools, route constraints, customer SLAs, regulatory zones, etc. How could this be solved elegantly and lightweight:

<mark>再考虑一家物流公司。流程变体有 100 种，取决于产品类型、工具 (Tools)、路线约束、客户 SLA、监管区域等等。怎样才能既优雅又轻量地解决：</mark>

- One agent, one giant context window. Causes immediate context rot and exorbitant token costs.

<mark>一个智能体，一扇巨大的上下文窗口。会立刻造成上下文腐烂 (Context Rot)，token 成本也高得离谱。</mark>

- RAG over the runbooks. Probably the right answer two years ago. But you're now running a vector DB, an embedding model, and a chunking strategy whose quality has nothing to do with the actual procedures.

<mark>在运维手册上做检索增强生成 (RAG)。两年前这大概是正确答案。但你现在要运维一个向量数据库、一个嵌入模型，以及一套分块策略，而这套策略的质量跟真正的流程毫无关系。</mark>

- Multi-agent, one subagent per process. 100 subagents, each with a process-specific system prompt. An operational nightmare of 100 deployments, 100 evaluation surfaces, and complex routing layers.

<mark>多智能体，每个流程一个子智能体。100 个子智能体，各自带着流程专用的系统提示词。运维噩梦：100 次部署、100 个评估面，外加复杂的路由层。</mark>

- One agent, 100 skills. This fits the skills format as there are many variants for the same job. The progressive disclosure of skills means 100 skills cost ~100 × 50 tokens = ~5,000 tokens of always-loaded metadata. Logistics requests carry strong activation cues: SKU, origin, weight, hazmat flag, SLA, which makes skill descriptions sharp and selection reliable. Procedures live in version control. Adding the 101st variant is a new folder, not a new deployment. Easier to maintain and to scale.

<mark>一个智能体，100 个技能。同一份工作有很多变体，正好契合技能格式。技能的渐进式披露 (Progressive Disclosure) 意味着，100 个技能的常驻成本大约是 100 × 50 token = 约 5,000 token 的始终加载元数据。物流请求带着很强的激活线索：SKU、始发地、重量、危化品标记、SLA。这让技能描述很锋利，选择也很可靠。流程住在版本控制里。加上第 101 个变体，是一个新文件夹，不是一次新部署。更好维护，也更好扩展。</mark>

However, the most important part is to always have a strict evaluation process and compare different performances to make the final decision (Section 4 covers what that evaluation work actually looks like in practice).

<mark>不过，最重要的是始终要有严格的评估过程，并比较不同方案的表现，再做最终决定（第 4 节会讲这套评估工作在实践中到底长什么样）。</mark>

As a mental note, adoption follows the path of least resistance. Anyone who can write documentation can write a skill. That lowers the barrier and the latent procedural knowledge sitting in wikis, runbooks, and engineers' heads finally has somewhere structured to flow.

<mark>记一笔：采用总是沿着阻力最小的路径走。会写文档的人就会写技能。门槛因此降低，藏在 wiki、运维手册和工程师脑子里的潜在程序性记忆 (Procedural Memory)，终于有了一个结构化的去处。</mark>

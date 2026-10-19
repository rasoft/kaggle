# Where to start

<mark>从哪里开始</mark>

The shift from syntax to intent is not a future state. It is the work in front of us today. Whether reading this as an individual builder or as a leader thinking about how a team or organisation adopts these tools, the same underlying principle holds: AI amplifies the engineering culture it lands in. The practices below translate that principle into action.

<mark>从语法到意图的转变不是未来状态。它是今天摆在面前的工作。无论你是作为个人构建者来读，还是作为思考团队或组织如何采用这些工具的负责人来读，底下的原则都一样：AI 放大它落进去的那套工程文化。下面的实践把这条原则变成行动。</mark>

---

## For individual developers

<mark>给个人开发者</mark>

1. Set up an AGENTS.md (or equivalent) for the project. Pick the convention that matches the coding agent of choice. Start with ten lines: stack, conventions, hard rules, workflow. Add a rule every time the agent does something it should not do again.

<mark>1. 为项目建立一份 AGENTS.md（或等价物）。选择与你所用编码智能体 (coding agent) 匹配的约定。从十行开始：技术栈、约定、硬规则、工作流。每当智能体 (Agent) 做了不该再做的事，就加一条规则。</mark>

2. Install a set of skills for your coding agents (like Agents CLI) to build, evaluate, deploy and optimize agents.

<mark>2. 为编码智能体安装一组技能 (Skill)（例如 Agents CLI），用来构建、评估 (evaluate)、部署和优化智能体。</mark>

3. Pick one repetitive workflow and make it the first agent. A research workflow, a code review process, a recurring report, a piece of content produced regularly. Use a coding agent for the prototype, and graduate it to a production agent through Agents CLI when it earns its keep. Building one agent end to end teaches more than reading about a hundred.

<mark>3. 挑一个重复的工作流，把它做成第一个智能体。一套研究流程、一个代码评审过程、一份定期报告、一块定期产出的内容。用编码智能体做原型，等它证明自己值得留下，再通过 Agents CLI 把它毕业成生产智能体。从头到尾构建一个智能体，比读一百个更有收获。</mark>

4. Write the tests and evals before generating the code. Together they are the contract with the AI. A well-written test and eval suite communicates intent more precisely than any natural-language prompt, and turns AI-assisted development from vibe coding into agentic engineering.

<mark>4. 在生成代码之前写下测试和评估 (eval)。它们合在一起，就是与 AI 的契约。一套写得好的测试和评估套件，比任何自然语言提示都更精确地传达意图，并把 AI 辅助开发从氛围编码 (vibe coding) 变成智能体工程 (agentic engineering)。</mark>

5. Review every line the agent produces that is going to ship. Be skeptical of anything that looks clever. Check imports for real packages. Verify that error handling covers realistic failure modes. Code that the team does not understand becomes debugging cost the team cannot afford.

<mark>5. 评审智能体产出的、将要发布的每一行。对任何看起来巧妙的东西保持怀疑。检查导入的是不是真实的包。验证错误处理覆盖了现实的失败模式。团队看不懂的代码，会变成团队负担不起的调试成本。</mark>

6. Maintain your developer skills. AI handles the routine so the developer can focus on the challenging. That arrangement only works if the foundational skills, debugging, system design, intuition for performance and correctness, stay sharp. Treat AI as a way to apply expertise at a greater scale, not as a substitute for it. Regular practice with complex debugging, code review of AI output, and architecture discussions stay essential to growing as an engineer.

<mark>6. 维持你的开发者技能。AI 处理常规事务，好让开发者专注于难的部分。这种安排只有在基础技能保持锋利时才成立：调试、系统设计、对性能和正确性的直觉。把 AI 当成在更大尺度上运用专长的方式，而不是专长的替代品。定期练习复杂调试、评审 AI 输出，以及架构讨论，对作为工程师成长仍然必要。</mark>

---

## For engineering leaders

<mark>给工程负责人</mark>

1. Make context engineering a first-class engineering practice on the team. Treat AGENTS.md, system prompts, eval suites, and skill libraries as code: reviewed in pull requests, versioned with the project, owned by named engineers. Without this discipline, the harness drifts and agent behaviour becomes irreproducible across the team.

<mark>1. 把上下文工程 (context engineering) 变成团队里的一等工程实践。把 AGENTS.md、系统提示、评估套件和技能库当成代码：在拉取请求 (pull request) 里评审，随项目版本化，由指名的工程师拥有。没有这套纪律，驾驭层 (Harness) 会漂移，智能体行为在团队之间变得不可复现。</mark>

2. Set the bar at the eval, not the demo. A working demo proves an agent can succeed once. A passing eval suite proves it succeeds reliably. But an eval without a clear rubric measures nothing. Define what you are scoring: task success, tool use quality, trajectory compliance, hallucination, and response quality. Require eval coverage with explicit rubrics as a precondition for any agent shipping into a shared workflow, the same way test coverage gates a service deployment.

<mark>2. 把门槛设在评估上，而不是演示上。一个能跑的演示证明智能体能成功一次。一套通过的评估套件证明它能可靠地成功。但没有清楚量规的评估什么也测不到。定义你在打分的东西：任务成功、工具使用 (tool use) 质量、轨迹 (trajectory) 符合度、幻觉和响应质量。把带明确量规的评估覆盖，作为任何智能体进入共享工作流的前提，就像测试覆盖是服务部署的门禁一样。</mark>

3. Re-shape code review for AI-generated code. AI-generated code requires the same or greater scrutiny than human-written code, with extra attention to hallucinated dependencies, inadequate error handling, and subtle correctness gaps that look right at a glance. Train reviewers on the failure modes of generated code, and tune review checklists accordingly.

<mark>3. 为 AI 生成的代码重塑代码评审。AI 生成的代码需要与人工编写的代码相同、或更严的审视，并额外注意幻觉出来的依赖、不充分的错误处理，以及一眼看去是对的、微妙的正确性缺口。就生成代码的失败模式训练评审者，并据此调整评审清单。</mark>

4. Distinguish prototyping work from production work in team norms. Vibe coding is the right speed for exploration. Agentic engineering is the right discipline for production. Make the boundary explicit: which projects, which branches, which environments warrant which mode of working. Teams that keep this distinction blurry produce prototypes that ship by accident.

<mark>4. 在团队规范里区分原型工作和生产工作。氛围编码是探索的合适速度。智能体工程是生产的合适纪律。把边界写明确：哪些项目、哪些分支、哪些环境配哪种工作模式。把这个区分保持模糊的团队，会让原型意外地发布出去。</mark>

5. Invest in the harness components as a shared team asset. Reusable system prompts, skill libraries, MCP server connections, and evaluation harnesses compound across projects. Treat them as infrastructure: documented, maintained, and improved deliberately. The teams that compound the most value from AI-assisted development are the ones that build their harness once and refine it many times.

<mark>5. 把驾驭层组件当成团队共享资产来投入。可复用的系统提示、技能库、模型上下文协议 (Model Context Protocol, MCP) 服务器连接和评估驾驭层，会跨项目复利。把它们当成基础设施：有文档、有人维护、被刻意改进。从 AI 辅助开发里复利出最多价值的团队，是那些把驾驭层建一次、再打磨许多次的团队。</mark>

---

## For organizations

<mark>给组织</mark>

1. Treat AI-assisted development as an engineering investment, not a productivity feature. The teams seeing the largest gains pair AI tooling with eval coverage, observability, and clear architectural standards. Rolling out a coding agent without that scaffolding produces speed without quality, which compounds into technical debt faster than any team can pay it down.

<mark>1. 把 AI 辅助开发当成工程投入，而不是一项生产力功能。看到最大收益的团队，把 AI 工具与评估覆盖、可观测性和清楚的架构标准配在一起。没有那层脚手架就铺开编码智能体，产出的是没有质量的速度，它复利成技术债的速度，比任何团队偿还的速度都快。</mark>

2. Invest in the production substrate before scale. A vibe-coded prototype on a laptop is not a production system. What graduates one to the other is the operations discipline around it: trajectory and final-response evals run in CI, traces of every agent run, scoped permissions per agent, and security review tuned to the failure modes of generated code. Build this substrate before the first production agent ships, not after.

<mark>2. 在放量之前投入生产基底。笔记本上一个氛围编码出来的原型不是生产系统。把一个毕业成另一个的，是周围的运维纪律：在 CI 里运行的轨迹评估和最终响应评估，每一次智能体运行的追踪，每个智能体划定范围的权限，以及针对生成代码失败模式调过的安全评审。在第一个生产智能体发布之前建好这层基底，而不是之后。</mark>

3. Adopt open standards for tools and inter-agent communication. Model Context Protocol (MCP) for tool access and Agent2Agent (A2A) for cross-agent delegation are converging into the connective tissue of multi-agent systems. Choosing them now keeps the option to mix vendors and frameworks open, and avoids re-platforming later.

<mark>3. 为工具和智能体间通信采用开放标准。用于工具访问的模型上下文协议 (MCP)，和用于跨智能体委派的智能体对智能体 (Agent2Agent, A2A)，正在汇成多智能体系统的结缔组织。现在就选择它们，保留混合厂商和框架的选项，并避免以后重新换平台。</mark>

4. Plan for hybrid teams of humans and agents, not human-only or agent-only workflows. The strongest production results in the past year come from architectures where humans set direction, agents do the implementation, and clear handoff protocols govern the boundary. Code review processes, on-call rotations, and team structures all need to evolve to reflect that agents are now participants, not just tools.

<mark>4. 为人和智能体的混合团队做规划，而不是只为人、或只为智能体的工作流。过去一年里最强的生产结果，来自这样的架构：人设定方向，智能体做实现，清楚的交接协议管辖这条边界。代码评审流程、值班轮转和团队结构都需要演进，以反映智能体现在是参与者，不只是工具。</mark>

5. Reframe hiring and skill development around judgment, not just implementation. As implementation becomes faster and more automated, the bottleneck shifts to specification, evaluation, architectural judgment, and review. Hire and develop for those skills deliberately. The most valuable engineers in the next several years will be the ones who can direct agents well, not the ones who can write the most code.

<mark>5. 把招聘和技能发展重新框定在判断上，而不只是实现上。随着实现变得更快、更自动化，瓶颈转向规格、评估、架构判断和评审。有意识地为这些技能招聘和培养。未来几年最有价值的工程师，将是那些能把智能体指挥好的人，而不是那些能写出最多代码的人。</mark>

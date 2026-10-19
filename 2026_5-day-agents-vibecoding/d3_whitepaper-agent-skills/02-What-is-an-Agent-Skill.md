# 2. What is an Agent Skill (and How to Build Your First One)

<mark>2. 什么是智能体技能 (Agent Skill)，以及如何构建第一个</mark>

Agent Skills are a primitive for giving a general-purpose agent on-demand specialist competence. Yes, a Skill can be as simple as a single markdown file, but it doesn’t have to stop there, and the paradigm behind it is quite innovative.

<mark>智能体技能 (Agent Skill) 是一种原语，用来给通用智能体 (Agent) 按需补上专家能力。是的，一个技能 (Skill) 可以简单到只有一个 Markdown 文件，但它不必停在那里，背后的范式相当有新意。</mark>

Today we are seeing Agent Skills emerge through two distinct patterns:

<mark>今天，智能体技能沿着两条不同的路径出现：</mark>

The first path is driven by subject matter experts, who already have institutional knowledge written down somewhere. Think of a compliance officer with a 30-page runbook, or an HR manager with onboarding guides for new hires. None of them need to learn to code to write and start using a Skill. They already have the content; the only job left is to translate it into a format the agent can use smartly.

<mark>第一条路径由主题专家推动。他们的机构知识已经写在某处。比如合规官手里有一份 30 页的运维手册 (runbook)，或者人力资源经理手里有新员工入职指南。他们不必学编程才能写出并开始使用技能。内容已经有了，剩下的工作只是把它翻译成智能体能聪明地使用的格式。</mark>

The second path involves developers wrapping agentic or coded workflows into Skills. If an agent successfully executes a non-trivial, repetitive task, you don't want it to have to figure out the process from scratch next time. Instead, you want the agent to create a Skill out of this successful run. In short, we are observing an emerging pattern: anything that is a good, reusable workflow becomes a Skill, and you don't have to write it yourself, the agent does, you review. This is already meta-skills territory, which we introduce gently here before going deep on it in Section 6.

<mark>第二条路径是开发者把智能体工作流或已编码的工作流包成技能。如果智能体成功执行了一个不简单、又会重复的任务，你不会希望它下次再从头摸索过程。你希望智能体把这次成功运行做成一个技能。简而言之，我们看到一个正在成形的模式：凡是好的、可复用的工作流，都会变成技能；你不必自己写，智能体来写，你来审。这已经是元技能 (Meta-skill) 的领地。这里先轻轻介绍，第 6 节再深入。</mark>

Both groups produce the same artifact, a Skill folder anchored by the SKILL.md primitive, but the journey to get there is different.

<mark>两组人产出的是同一种制品：一个以 SKILL.md 原语为锚点的技能文件夹。到达那里的旅程不同。</mark>

---

## Skill Anatomy & Progressive Disclosure

<mark>技能解剖与渐进式披露 (Progressive Disclosure)</mark>

Before going into the different paths, let’s review the Skill anatomy. Every skill lives in its own directory and must contain a SKILL.md. To see the full canonical structure, as defined by the open standard at agentskills.io, let's look at a practical example.

<mark>在进入不同路径之前，先看技能的解剖。每个技能住在自己的目录里，而且必须包含 SKILL.md。完整的规范结构由 agentskills.io 上的开放标准定义。我们看一个实际例子。</mark>

Below is an illustrative folder for a Skill designed to conduct daily cafe preparation. (Remember, the only mandatory file is SKILL.md. The rest is optional):

<mark>下面是一个示意性文件夹，对应一个负责每日咖啡馆备料的技能。（记住，唯一的必需文件是 SKILL.md。其余都是可选的。）</mark>

```text
cafe-preparation/
├── SKILL.md                      # Required: metadata + instructions
├── scripts/                      # Optional: executable code (any language)
│   ├── calc_quantities.py        # Estimates lattes, croissants, etc.
│   └── convert_to_ingredients.py # Converts drinks and pastries into..
├── references/                   # Optional: supplementary context
│   ├── menu_and_recipes.md       # Matcha latte: 3g powder, 200ml...
│   └── minimums.md               # Always prep for at least 40 lattes...
└── assets/                       # Optional: templates, configs, schemas
    ├── prep_sheet_template.md    # The final layout for the kitchen staff
    └── shopping_list_template.md # The layout for vendor ordering
```

Snippet 1: Directory tree structure showing the standard layout and progressive disclosure design for the cafe-preparation skill.

<mark>代码片段 1：目录树展示 cafe-preparation 技能的标准布局和渐进式披露设计。</mark>

<mark>注释：SKILL.md 为必需，包含元数据与指令。scripts/ 为可选的可执行代码（任意语言）。calc_quantities.py 估算拿铁、可颂等数量。convert_to_ingredients.py 把饮品和糕点换算成原料。references/ 为可选的补充上下文。menu_and_recipes.md 记录配方，例如抹茶拿铁：3 克粉、200 毫升……。minimums.md 规定至少准备 40 杯拿铁……。assets/ 为可选的模板、配置和 schema。prep_sheet_template.md 是给后厨的最终备料表版式。shopping_list_template.md 是向供应商订货的版式。</mark>

The innovative piece is the progressive disclosure. Skills load in three levels:

<mark>真正有新意的部分是渐进式披露。技能分三层加载：</mark>

1. Metadata (name + description) is always in the agent's context.

<mark>1. 元数据（name + description）始终在智能体的上下文里。</mark>

2. SKILL.md body is loaded only when the skill triggers.

<mark>2. SKILL.md 正文只在技能触发 (Trigger) 时加载。</mark>

3. Bundled resources are loaded strictly as needed (and scripts execute without ever polluting the token window).

<mark>3. 打包的资源严格按需加载（脚本执行时，永远不会污染 token 窗口）。</mark>

This means you can have a hundred installed skills but only pay the tiny token cost for their metadata on every turn. Let's get practical and look at how to build one.

<mark>这意味着你可以装上 100 个技能，但每一轮只为它们的元数据支付很小的 token 成本。下面进入实操，看怎么做一个。</mark>

---

## Path A: Translating what you already know

<mark>路径 A：翻译你已经知道的东西</mark>

A minimal SKILL.md template lives in Appendix A. You can copy it directly. The piece worth focusing on first is the YAML frontmatter, because it's the activation trigger:

<mark>附录 A 里有一份最小的 SKILL.md 模板，可以直接复制。最先值得盯紧的是 YAML 前置元数据 (frontmatter)，因为它就是激活触发器：</mark>

```yaml
---
name: cafe-preparation
description: |
  Calculates daily ingredient needs and generates prep sheets for cafe operations.
  Use when the user asks to estimate daily quantities, convert drinks to
  ingredients, or generate shopping lists.
  Do NOT use for employee shift scheduling or financial accounting.
---
```

Snippet 2: YAML frontmatter configuration for the cafe-preparation skill.

<mark>代码片段 2：cafe-preparation 技能的 YAML frontmatter 配置。</mark>

<mark>description 的意思是：计算每日原料需求，并为咖啡馆运营生成备料表。当用户要求估算每日数量、把饮品换算成原料，或生成采购清单时使用。不要用于员工排班或财务记账。</mark>

There are two things worth getting right from the start: naming and the description field.

<mark>有两件事从一开始就值得做对：命名，以及 description 字段。</mark>

Naming. When naming, be obvious and boring: use snake_case for directories (e.g., bigquery_ingestion), kebab-case for skill names (e.g., pdf-processing), and prefer the gerund form like managing-databases. Avoid generic names such as utils or tools and omit any internal jargon.

<mark>命名。命名时要直白、甚至乏味：目录用 snake_case（例如 bigquery_ingestion），技能名用 kebab-case（例如 pdf-processing），并优先用动名词形式，如 managing-databases。避开 utils、tools 这类泛名，也不要夹带内部黑话。</mark>

Description. This is your routing algorithm. It is the only thing the model sees to decide whether to load the Agent Skill. State what it does, front-load trigger keywords, be pushy if the model under-triggers, and explicitly state what it is not for.

<mark>Description。这就是你的路由算法。模型 (Model) 决定要不要加载这个智能体技能时，唯一能看到的就是它。写清它做什么，把触发关键词放在前面；如果模型触发不足，就把语气写得更主动；并明确写出它不用于什么。</mark>

---

Once the SKILL.md is drafted, you build out the rest of the folder. This is where progressive disclosure starts paying off. Anything that doesn't need to be in the SKILL.md body goes somewhere else:

<mark>SKILL.md 起草之后，再把文件夹的其余部分补上。渐进式披露从这里开始兑现。凡是不必放进 SKILL.md 正文的东西，都放到别处：</mark>

- Scripts. Deterministic work (parsing exports, math, formatting) lives in scripts/. The model decides what to do; the script does the heavy lifting.

<mark>脚本。确定性工作（解析导出文件、数学计算、格式化）放在 scripts/。模型决定做什么；脚本承担重活。</mark>

- References. Knowledge that is only relevant once the skill is running (domain principles, definitions, edge case handling) lives in references/ and loads on demand.

<mark>参考资料。只有技能已经在跑时才相关的知识（领域原则、定义、边界情况处理）放在 references/，按需加载。</mark>

- Assets. Templates and schemas live in assets/.

<mark>资源。模板和 schema 放在 assets/。</mark>

Rule of thumb: if the SKILL.md is starting to get long, the next paragraph probably belongs in references/ and not in the body.

<mark>经验法则：如果 SKILL.md 开始变长，下一段大概该进 references/，而不是留在正文里。</mark>

(Impatient? Appendix A offers a printable operational cheat sheet with curated Do’s and Don’ts to guide your initial Skill development).<sup>1</sup>

<mark>（等不及了？附录 A 有一份可打印的操作速查表，整理了该做与不该做，用来引导你最初的技能开发。）<sup>1</sup></mark>

---

## Path B: Crystallizing what the agent just did

<mark>路径 B：把智能体刚刚做成的事结晶下来</mark>

The second path starts from the other end. Instead of translating something you already have, you're crystallizing something the agent just did.

<mark>第二条路径从另一头开始。你不是在翻译已有的东西，而是把智能体刚刚做成的事结晶下来。</mark>

The agent completed a task successfully. You noticed the workflow was reusable. You want the next instance of that kind of task to benefit from what was just learned.

<mark>智能体成功完成了一个任务。你注意到这个工作流可以复用。你希望下一次同类任务能用上刚刚学到的东西。</mark>

This is the meta-skills territory: Skills whose job is to capture or improve other Skills. Tools like Anthropic's skill-creator<sup>2</sup>, Nous Research's Hermes Agent<sup>3</sup>, and the self-improving-agent-skills pattern from awesome-llm-apps<sup>4</sup> all support this workflow. The agent watches a successful trajectory and proposes a SKILL.md draft. You review, instead of authoring.

<mark>这就是元技能的领地：职责是捕获或改进其他技能的技能。Anthropic 的 skill-creator<sup>2</sup>、Nous Research 的 Hermes Agent<sup>3</sup>，以及 awesome-llm-apps 里的 self-improving-agent-skills 模式<sup>4</sup>，都支持这种工作流。智能体观察一条成功轨迹，并提议一份 SKILL.md 草稿。你负责审阅，而不是从零撰写。</mark>

The same quality bar applies. A reviewed, iterated, agent-drafted Skill can be excellent. An un-reviewed agent-drafted Skill is often worse than no Skill at all. We come back to this whole topic with much more depth in Section 6, where we cover meta-skills.

<mark>质量门槛是一样的。经过审阅和迭代的、由智能体起草的技能可以非常好。未经审阅的、由智能体起草的技能，常常比没有技能更糟。第 6 节会把整个主题讲得深得多，那里专门谈元技能。</mark>

---

## Trying it out & How to install Skills today

<mark>试一试，以及今天如何安装技能</mark>

Once the folder is ready (whether you wrote it or an agent drafted it for you), it is time to try it out. Drop it in the right place for your tool, restart the agent, and test it with a natural prompt. Watch the trace to confirm the skill actually triggered. Then try a prompt where it should NOT trigger and confirm it stays quiet.

<mark>文件夹就绪之后（无论是你写的，还是智能体替你起草的），就该试一试。把它放到你所用工具的正确位置，重启智能体，用一句自然语言提示来测试。看轨迹，确认技能真的触发了。然后再试一条它不该触发的提示，确认它保持沉默。</mark>

But where exactly is the "right place"?

<mark>但「正确位置」到底在哪？</mark>

This is where things get a bit nuanced, and it's one of the downsides of the exploding popularity of Skills. Every agent or coding tool has converged on the format, but they each look in a slightly different place for it. Broadly, there are three paradigms for how you will interact with and install Skills today:

<mark>这里开始有些细微差别，也是技能爆红的一个副作用。每个智能体或编码工具都收敛到了同一种格式，但它们各自去略有不同的地方找它。大体上，今天与技能交互和安装技能有三种范式：</mark>

1. The File Drop (Coding Agents & CLIs): For local environments, the pattern is file-based, you drop or install the skill folder into a specific hidden directory and the agent picks it up. While a highly welcome cross-tool convention is emerging around a shared .agents/skills/ folder at your project root, many tools still protect their own bespoke paths. (Pro tip: If you bounce between multiple CLI tools and IDEs, community managers like skillport or openskills will automatically symlink your central skills library to every tool's expected location).

<mark>1. 文件投放（编码智能体与 CLI）：本地环境走的是基于文件的模式。你把技能文件夹丢进或安装到某个特定的隐藏目录，智能体就会捡起来。一个很受欢迎的跨工具约定正在形成：项目根目录下共享的 .agents/skills/ 文件夹。不过很多工具仍然守着自己的专用路径。（实用提示：如果你在多个 CLI 工具和 IDE 之间来回切换，skillport 或 openskills 这类社区管理器会自动把你的中央技能库符号链接到每个工具期望的位置。）</mark>

2. The UI Install (Web & Enterprise Workspaces): If you are using web-based collaborative platforms or consumer AI chatbots, you rarely touch a terminal or a hidden folder. These platforms allow you to install, upload, or manage your Skill folders directly through a visual UI registry with just a few clicks, handling the routing behind the scenes for your whole team.

<mark>2. 界面安装（Web 与企业工作区）：如果你用的是基于网页的协作平台或消费级 AI 聊天机器人，你很少会碰终端或隐藏文件夹。这些平台让你点几下，就能通过可视化的 UI 注册表直接安装、上传或管理技能文件夹，并在幕后为整个团队处理路由。</mark>

3. The Programmatic Route (Custom Frameworks): If you are building bespoke, non-coding agents from scratch (for example, using the Google Agent Development Kit), you load skills programmatically. You point your code to the folder path—such as registering it through a SkillToolset class<sup>5</sup>, which seamlessly auto-generates the necessary load_skill routing tools for the model under the hood.

<mark>3. 编程路径（自定义框架）：如果你从零构建定制的、非编码类智能体（例如使用 Google Agent Development Kit），就以编程方式加载技能。你把代码指向文件夹路径，比如通过 SkillToolset 类注册它<sup>5</sup>。它会在底层无缝地为模型自动生成所需的 load_skill 路由工具 (Tools)。</mark>

The overall pattern is the same everywhere: drop the skill folder into the right directory, restart the agent, and it picks it up. The "right directory" is what changes depending on the tool.

<mark>总体模式到处都一样：把技能文件夹放进正确的目录，重启智能体，它就会捡起来。会变的是「正确的目录」，它取决于工具。</mark>

A piece of advice: check the documentation of your specific coding agent or AI chatbot before assuming. The format is shared, but the install path, the activation rules, and the per-tool details (allowed-tools whitelisting, security gates, plugin bundling) are not.

<mark>一条建议：先查你所用编码智能体或 AI 聊天机器人的文档，再做假设。格式是共享的，但安装路径、激活规则，以及每个工具自己的细节（allowed-tools 白名单、安全门禁、插件打包）并不是。</mark>

---

## Wait but how does a Skill differ from MCP and AGENTS.md?

<mark>等一下，技能和 MCP、AGENTS.md 有什么不同？</mark>

To establish the architectural fit of Agent Skills, it helps to map these primitives.

<mark>要摆正智能体技能在架构里的位置，最好先把这些原语对上号。</mark>

Skill vs. MCP. These do not compete, they compose. Model Context Protocol is about reach: an MCP server connects the agent to an external system (Drive, Salesforce, BigQuery, or an internal API). A Skill is about know-how: it teaches the agent how to think about a particular kind of work. When a Skill needs data, it tells the agent to call a tool, typically one provided by an MCP server.

<mark>技能对比 MCP。它们不竞争，它们组合。模型上下文协议 (Model Context Protocol, MCP) 管的是触达：一个 MCP 服务器把智能体接到外部系统（Drive、Salesforce、BigQuery，或内部 API）。技能管的是诀窍：它教智能体如何思考某一类工作。技能需要数据时，会让智能体调用一个工具，通常就是 MCP 服务器提供的那个工具。</mark>

Skill vs. AGENTS.md. From one side AGENTS.md is always loaded within the project; Skills load on demand. The cleanest setups use both. Keep AGENTS.md tight (project conventions, stack, build commands, etc.) and if needed use it also as a router into the Skills library, with a short catalog at the bottom that tells the agent what’s available.

<mark>技能对比 AGENTS.md。一方面，AGENTS.md 在项目里始终加载；技能则按需加载。最干净的做法是两者都用。把 AGENTS.md 写紧（项目约定、技术栈、构建命令等），需要时也用它做技能库的路由器，在底部放一份短目录，告诉智能体有哪些技能可用。</mark>

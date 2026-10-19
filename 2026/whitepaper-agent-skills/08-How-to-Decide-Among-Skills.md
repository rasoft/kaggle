# 8. How to Decide Among the Hundreds of Skills That Exist

<mark>8. 面对成百上千个技能，如何做选择</mark>

By early 2026, public skill marketplaces had crossed 40,000 listings, with the leading platform reporting tens of thousands of new skills published in the first weeks of January alone. At Google Cloud Next 2026, Google launched its official Agent Skills repository at github.com/google/skills, with skills installable via `npx skills install github.com/google/skills` for use across Antigravity CLI, and any other coding agent that supports the Skills standard. The Anthropic skills repository, the Google ADK skill library, the Google official skills repository, and community marketplaces such as awesome-llm-apps now host more skills than any practitioner could review individually. The selection problem is real and growing.

<mark>到 2026 年初，公开的技能市场已经超过 40,000 条上架，领先平台报告仅 1 月的头几周就发布了数以万计的新技能 (Skill)。在 Google Cloud Next 2026 上，Google 发布了官方的智能体技能 (Agent Skill) 仓库 github.com/google/skills。技能可以通过 `npx skills install github.com/google/skills` 安装，用于 Antigravity CLI，以及任何其他支持技能标准的编码智能体 (Agent)。Anthropic 技能仓库、Google ADK 技能库、Google 官方技能仓库，以及 awesome-llm-apps 这类社区市场，现在托管的技能多到任何实践者都无法逐个审阅。选择问题是真实的，而且在变大。</mark>

Three heuristics help.

<mark>三条启发式有帮助。</mark>

1. First, prefer first-party skills for vendor-specific tools. Google's BigQuery skill, the official Stripe skill, anything written by the people who built the underlying system. They will be more correct and more maintained than community alternatives.

<mark>1. 第一，厂商专用工具优先用第一方技能。Google 的 BigQuery 技能、Stripe 的官方技能，以及任何由底层系统建造者写的东西。它们会比社区替代品更正确，也更有人维护。</mark>

2. Second, pin everything you depend on. Community skills evolve, and an unpinned dependency that worked yesterday can fail tomorrow.

<mark>2. 第二，把你依赖的一切都钉住版本。社区技能会演化，一个昨天能用、却没有钉版本的依赖，明天就可能失败。</mark>

3. Third, audit before adopting. A skill is code that runs in your context. Treat it like any other dependency, with the same supply-chain hygiene.

<mark>3. 第三，采用之前先审计。技能是跑在你上下文里的代码。把它当成任何其他依赖，用同样的供应链卫生来对待。</mark>

Not all sources are equal. Three categories of skill source exist in early 2026, and the right operational stance is different for each:

<mark>来源并不平等。2026 年初存在三类技能来源，对每一类，正确的操作姿态都不同：</mark>

| Source | Trust default | Examples | Who maintains it |
| --- | --- | --- | --- |
| First-party vendor skills | Trust by default; pin a version | google/agents-cli<sup>28</sup>, google/skills<sup>29</sup>, google-gemini/gemini-skills<sup>30</sup>, anthropics/skills<sup>31</sup>, stripe/ai<sup>32</sup>, microsoft/skills<sup>33</sup> | The team that built the underlying product |
| Organization-curated skills | Trust within the org; review on adoption | your-org/retail-skills, your-org/finance-skills (private, internally maintained) | Your own domain teams, with PR review |
| Community skills | Audit before adopting; pin aggressively | VoltAgent/awesome-agent-skills<sup>34</sup>, SkillsMP marketplace<sup>35</sup>, addyosmani/agent-skills<sup>36</sup>, individual GitHub repos | Volunteer authors, varying maintenance commitment |

<mark>表 4：智能体技能来源概览，按默认信任、官方示例和维护所有权分类。</mark>

| <mark>来源</mark> | <mark>默认信任</mark> | <mark>示例</mark> | <mark>谁维护</mark> |
| --- | --- | --- | --- |
| <mark>第一方厂商技能</mark> | <mark>默认信任；钉住一个版本</mark> | google/agents-cli<sup>28</sup>, google/skills<sup>29</sup>, google-gemini/gemini-skills<sup>30</sup>, anthropics/skills<sup>31</sup>, stripe/ai<sup>32</sup>, microsoft/skills<sup>33</sup> | <mark>构建底层产品的那个团队</mark> |
| <mark>组织策展的技能</mark> | <mark>组织内部信任；采用时审阅</mark> | your-org/retail-skills, your-org/finance-skills <mark>（私有，内部维护）</mark> | <mark>你自己的领域团队，经 PR 审阅</mark> |
| <mark>社区技能</mark> | <mark>采用前审计；积极钉版本</mark> | VoltAgent/awesome-agent-skills<sup>34</sup>, SkillsMP marketplace<sup>35</sup>, addyosmani/agent-skills<sup>36</sup>, <mark>以及单独的 GitHub 仓库</mark> | <mark>志愿作者，维护投入参差不齐</mark> |

Table 4: Overview of Agent Skill sources categorized by trust defaults, official examples, and maintenance ownership.

<mark>表 4：按默认信任、官方示例和维护所有权，对智能体技能来源的概览。</mark>

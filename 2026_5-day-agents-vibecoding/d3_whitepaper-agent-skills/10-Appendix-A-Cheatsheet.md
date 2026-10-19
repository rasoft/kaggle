# Appendix A – The Practical Cheatsheet

<mark>附录 A — 实用速查表</mark>

This section is designed to be printable and standalone. It compresses the rest of the whitepaper into the decisions a team will face.

<mark>这一节设计成可以单独打印。它把白皮书的其余部分压缩成一个团队会面对的决定。</mark>

---

## The minimal SKILL.md

<mark>最小的 SKILL.md</mark>

Copy-paste this. Adjust the placeholders. Done.

<mark>复制粘贴。改掉占位符。完成。</mark>

```markdown
---
name: skill-name
description: |
  [What it does in one verb-led sentence.] Use this skill when the user
  [trigger phrase 1], [trigger phrase 2], or [trigger phrase 3].
  Do NOT use for [anti-trigger 1] or [anti-trigger 2].
version: 1.0.0
license: MIT
allowed-tools: [Optional] Read Bash Write
metadata:
  author: [Optional] your-handle
---

# Skill Name

## When to use
- [Concrete scenario]
- [Concrete scenario]

## When NOT to use
- [Out-of-scope scenario]

## Workflow
1. [Step]
2. [Step]
3. See `references/advanced.md` for [edge case].

## Examples
- Input: "..." → Output: "..."

## Output format
- Use `assets/template.md` etc.

## Anti-patterns to avoid
- Don't [...]
```

<mark>占位符含义：用一个以动词开头的句子写它做什么。当用户说出触发短语 1、2 或 3 时使用这个技能 (Skill)。不要用于反触发 1 或反触发 2。version 为 1.0.0。license 为 MIT。allowed-tools 可选，例如 Read、Bash、Write。metadata.author 可选，填你的账号。正文依次是：何时使用、何时不要使用、工作流、示例、输出格式、要避开的反模式。</mark>

---

## The folder structure.

<mark>文件夹结构。</mark>

```text
skill_name/
├── SKILL.md          # Required: YAML frontmatter + markdown instructions
├── scripts/          # Optional: executable helper scripts (Python, Bash)
├── references/       # Optional: supplementary context loaded as needed
├── assets/           # Optional: files used in output (templates, resources)
└── ...               # Any additional files or directories
```

<mark>注释：SKILL.md 为必需，包含 YAML 前置元数据 (frontmatter) 和 Markdown 指令。scripts/ 为可选的可执行辅助脚本（Python、Bash）。references/ 为可选的补充上下文，按需加载。assets/ 为可选的、用在输出里的文件（模板、资源）。其余为任何额外的文件或目录。</mark>

---

## Naming

<mark>命名</mark>

- Directory name: snake_case

<mark>目录名：snake_case</mark>

- Skill name: kebab-case

<mark>技能名：kebab-case</mark>

- Prefer gerund form: processing-pdfs, not pdf-processor

<mark>优先用动名词形式：processing-pdfs，而不是 pdf-processor</mark>

- Avoid generic names: helper, utils, tools, data

<mark>避开泛名：helper、utils、tools、data</mark>

- Avoid vendor prefixes: claude-*, gemini-*, anthropic-*

<mark>避开厂商前缀：claude-*、gemini-*、anthropic-*</mark>

- Avoid internal jargon outsiders won't recognize

<mark>避开外人认不出的内部黑话</mark>

---

## The description field

<mark>description 字段</mark>

The description is the routing algorithm. Spend more time here than anywhere else.

<mark>description 就是路由算法。花在这里的时间要比花在别处更多。</mark>

- State what it does AND when to use it

<mark>写清它做什么，以及何时使用</mark>

- Front-load trigger keywords ("Generate a commit message…", not "This skill helps with…")

<mark>把触发关键词放在前面（「Generate a commit message…」，而不是「This skill helps with…」）</mark>

- Include when NOT to use to prevent over-triggering

<mark>写上何时不要使用，以防止过度触发 (Trigger)</mark>

- Be pushy when the model under-triggers

<mark>模型 (Model) 触发不足时，把语气写得更主动</mark>

- ≤200 chars for API; ≤1024 chars in YAML. Most authors aim for ~50 words

<mark>API 不超过 200 个字符；YAML 不超过 1024 个字符。大多数作者瞄准大约 50 个词</mark>

---

## The five rules

<mark>五条规则</mark>

1. One skill, one job. If you cannot describe what the skill does in one sentence, it is two skills. Decompose before writing.

<mark>1. 一个技能，一份工作。如果你不能用一句话描述这个技能做什么，那它就是两个技能。先拆开，再写。</mark>

2. Descriptions are an interface. The agent picks skills by reading descriptions. A vague description means an unused skill.

<mark>2. 描述是接口。智能体 (Agent) 靠读描述来挑选技能。含糊的描述意味着一个用不上的技能。</mark>

3. Skills are dependencies. Treat them like libraries. Version them, pin them, review them in PRs. A skill without a test is a hope, not a capability.

<mark>3. 技能是依赖。把它们当库。给它们版本，钉住版本，在 PR 里审阅。没有测试的技能只是一种希望，不是一种能力。</mark>

4. The right team owns the right skill. Domain experts own domain skills. Do not let the AI team become a bottleneck for the organization's domain knowledge.

<mark>4. 对的团队拥有对的技能。领域专家拥有领域技能。不要让 AI 团队变成组织领域知识的瓶颈。</mark>

5. The agent runtime is interchangeable. Do not tie skills to one runtime. Portability is part of the value.

<mark>5. 智能体运行时 (runtime) 是可替换的。不要把技能绑死在一个运行时上。可移植性是价值的一部分。</mark>

---

## The quality principles

<mark>质量原则</mark>

1. Run the task yourself first. Real failure produces signal. Speculation produces noise.

<mark>1. 先自己把任务跑一遍。真实的失败产生信号。推测产生噪声。</mark>

2. Give the reason, not just the rule. Models generalize wonderfully to edge cases when they understand why an instruction exists. If you find yourself typing "ALWAYS" or "NEVER" in caps, pause and try explaining the rationale instead.

<mark>2. 给出理由，而不只是规矩。模型理解一条指令为什么存在时，对边界情况的泛化会好得出奇。如果你发现自己在打全大写的「ALWAYS」或「NEVER」，停一下，试着改成解释理由。</mark>

3. Every line should earn its place. Keep gotchas, exact commands, business logic, anti-patterns. Cut boilerplate the model already knows such as "always validate output".

<mark>3. 每一行都该挣到自己的位置。留下易错点、精确命令、业务逻辑、反模式。砍掉模型已经知道的套话，例如「always validate output」。</mark>

4. One skill, one job. If the description needs "and" between unrelated capabilities, split it.

<mark>4. 一个技能，一份工作。如果 description 需要在互不相关的能力之间加一个「and」，就把它拆开。</mark>

5. Make instructions verifiable. If the agent can't tell whether it followed the rule, the rule is too vague.

<mark>5. 让指令可验证。如果智能体无法判断自己有没有遵守这条规则，规则就太含糊了。</mark>

6. Bundle what repeats. Helper code the agent keeps re-deriving belongs in scripts/.

<mark>6. 把重复的东西打包。智能体一再重新推导的辅助代码，属于 scripts/。</mark>

---

## Do's and Don'ts

<mark>该做与不该做</mark>

Do:

<mark>该做：</mark>

- Start small and concrete

<mark>从小处、从具体处开始</mark>

- Spend disproportionate time on the description field. It is the routing algorithm. Always include what it does, when to use, and when not to use

<mark>在 description 字段上花不成比例的时间。它就是路由算法。始终写上它做什么、何时使用、何时不要使用</mark>

- Trust progressive disclosure

<mark>信任渐进式披露 (Progressive Disclosure)</mark>

- Bundle deterministic work in scripts/, not as instructions

<mark>把确定性工作打包进 scripts/，不要写成指令</mark>

- Treat Skills as code

<mark>把技能当代码</mark>

- Remember: Skills + MCPs, not Skills vs. MCPs

<mark>记住：技能加 MCP，而不是技能对打 MCP</mark>

- Have test cases and controlled, programmatic evaluation (see Section 4 for how to actually do this)

<mark>要有测试用例，以及受控的、可编程的评估 (Evaluation)（具体做法见第 4 节）</mark>

Don't:

<mark>不该做：</mark>

- Write vague descriptions like "helps with documents". Use specific verbs, trigger phrases, and a when-not-to-use clause

<mark>不要写「helps with documents」这种含糊描述。用具体动词、触发短语，以及一条「何时不要使用」</mark>

- Write SKILL.md bodies over 5,000 words. Move detail to references/

<mark>不要把 SKILL.md 正文写过 5,000 词。把细节移到 references/</mark>

- Hard-code paths or secrets

<mark>不要硬编码路径或密钥</mark>

- Embed "always do X" rules that are more appropriate for AGENTS.md

<mark>不要把更适合放进 AGENTS.md 的「always do X」规则嵌进来</mark>

- Install untrusted third-party libraries or Skills without scanning

<mark>不要在不扫描的情况下安装不可信的第三方库或技能</mark>

- Reinvent MCP as scripts

<mark>不要用脚本把 MCP 重做一遍</mark>

---

## Skill smells (revise if you see these)

<mark>技能异味（看到就要改）</mark>

- Over 5,000 words. Probably two skills, or reference material that should live in references/

<mark>超过 5,000 词。大概是两个技能，或者本该住在 references/ 里的参考材料</mark>

- Two domain teams could plausibly own it. Not yet decomposed. Split along team boundaries

<mark>两个领域团队都说得通地可以拥有它。还没拆开。沿着团队边界拆</mark>

- You can't write three test cases for it. Description is too vague; skill does too many things

<mark>你写不出三个测试用例。描述太含糊；技能做的事太多</mark>

- It does not reference any other resource. Might just be a long instruction that belongs in the system prompt

<mark>它不引用任何其他资源。也许只是一条很长的指令，属于系统提示词</mark>

- You keep adding "edge cases" sections. Each edge case probably wants its own skill

<mark>你不停地加「边界情况」小节。每个边界情况大概都想要自己的技能</mark>

- Its description starts with "a helpful skill for…". Rewrite. The description should name the trigger, the inputs, and the output

<mark>它的 description 以「a helpful skill for…」开头。重写。description 应该点名触发、输入和输出</mark>

---

## Eval coverage checklist

<mark>评估覆盖清单</mark>

A skill is "evaluated" only when all four are satisfied:

<mark>一个技能只有在下面四项都满足时，才算「已评估」：</mark>

- ☐ Trigger. Positive AND negative test cases. Target 90% trigger accuracy

<mark>☐ 触发。正向和负向测试用例都要有。目标是 90% 的触发准确率</mark>

- ☐ Execution. Correct outputs across a representative range of inputs

<mark>☐ 执行。在有代表性的输入范围内输出正确</mark>

- ☐ Regression. Adding this skill causes zero drops in the existing library suite

<mark>☐ 回归 (Regression)。加入这个技能后，现有技能库套件零下降</mark>

- ☐ Token budget. Co-loaded with 5 to 15 frequently-active skills, does not degrade unrelated turns

<mark>☐ Token 预算。与 5 到 15 个频繁活跃的技能共同加载 (co-load) 时，不拉低无关轮次</mark>

Any failure holds the skill at the draft tier, regardless of happy-path performance.

<mark>任何一项失败，都把技能留在草稿层，不管顺利路径上的表现如何。</mark>

---

## Deployment checklist

<mark>部署清单</mark>

- ☐ Frontmatter validates (lint passes)

<mark>☐ 前置元数据校验通过（lint 通过）</mark>

- ☐ Description includes what + when + when-not

<mark>☐ Description 包含做什么、何时使用、何时不要使用</mark>

- ☐ Scripts have unit tests passing in CI

<mark>☐ 脚本的单元测试在 CI 中通过</mark>

- ☐ Eval suite passes in CI with min-pass threshold

<mark>☐ 评估套件在 CI 中通过，并达到最低通过阈值</mark>

- ☐ Security scan clean (no secrets, no untrusted deps)

<mark>☐ 安全扫描干净（没有密钥，没有不可信依赖）</mark>

- ☐ Description reviewed by someone other than the author

<mark>☐ Description 由作者以外的人审阅过</mark>

- ☐ Cross-tool install paths tested if shipping publicly

<mark>☐ 如果公开交付，跨工具的安装路径已测试</mark>

- ☐ Org-level admin provisioning updated (if applicable)

<mark>☐ 组织级管理员配置已更新（如适用）</mark>

---

## One-line mental model

<mark>一句话心智模型</mark>

System prompt = instinct. AGENTS.md = project README. Tools / MCP = hands. RAG = library. Skills = the runbook the experienced colleague hands you on day one, and that the AI never forgets.

<mark>系统提示词 = 本能。AGENTS.md = 项目 README。工具 (Tools) / 模型上下文协议 (Model Context Protocol, MCP) = 手。检索增强生成 (RAG) = 图书馆。技能 = 有经验的同事在第一天递给你的运维手册 (runbook)，而且 AI 永远不会忘记。</mark>

---

## Where to start tomorrow

<mark>明天从哪里开始</mark>

1. Take your most experienced practitioner aside for an hour. Ask them to narrate three workflows they do regularly. Record it.

<mark>1. 把团队里最有经验的实践者单独约出来一个小时。请他们口述三件经常做的工作流。录下来。</mark>

2. Pick the most repeated workflow. Run the prompts yourself, without any skill loaded. Note where the agent fails. Or let an agent similar to ().

<mark>2. 挑出重复最多的工作流。你自己跑这些提示，不加载任何技能。记下智能体在哪里失败。或者让一个类似（）的智能体来做。</mark>

3. Draft a SKILL.md from the transcript. Write three eval cases (two positive, one negative) before drafting the body.

<mark>3. 根据转录起草一份 SKILL.md。在起草正文之前，先写三个评估用例（两个正向，一个负向）。</mark>

4. Ship to a read-only tier. Test in production-like conditions. Iterate the description until trigger accuracy clears 90%.

<mark>4. 交付到只读 (Read-Only) 层。在接近生产的条件下测试。迭代 description，直到触发准确率超过 90%。</mark>

Repeat. Build the library one workflow at a time. Resist the urge to let an LLM generate fifty skills on day one.

<mark>重复。一次一个工作流地建技能库。忍住第一天就让大语言模型生成 50 个技能的冲动。</mark>

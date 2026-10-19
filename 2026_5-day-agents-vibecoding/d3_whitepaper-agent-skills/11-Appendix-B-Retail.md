# Appendix B – Case Study: Domain Expertise as Code (Vertical Skills in Retail)

<mark>附录 B — 案例研究：把领域专长写成代码（零售业的垂直技能）</mark>

This section is the worked example of the whitepaper. It walks through how a large retailer would structure a skills library to capture the institutional knowledge that differentiates the brand from its competitors, and why that library, rather than any specific custom agent, is the durable strategic asset. Several major retailers have publicly described AI assistants with capabilities that match the architecture below. We describe the pattern, not the implementation of any single vendor.

<mark>这一节是白皮书的演算示例。它走一遍大型零售商会如何组织一个技能库 (Skill)，去捕获那些把品牌和竞争对手区分开的机构知识，以及为什么耐久的战略资产是这个技能库，而不是任何一个具体的定制智能体 (Agent)。几家大型零售商已经公开描述过能力与下面这套架构相符的 AI 助手。我们描述的是模式，不是任何单一厂商的实现。</mark>

---

## Why retail is the canonical case for skills

<mark>为什么零售是技能的典型场景</mark>

Two retailers running on the same agent runtime, accessing similar data through similar APIs, will produce wildly different shopping experiences. Retail expertise is the kind of knowledge that has historically been stuck in three places that AI systems have struggled to reach: in the heads of senior buyers, merchandisers, and category managers; in thirty-page operational runbooks that no one reads; and in Slack channels where the answer to "should we recommend this product with that one?" lives in a thread from 2023.

<mark>两家零售商跑在同一个智能体运行时 (runtime) 上，通过相似的 API 访问相似的数据，却会给出截然不同的购物体验。零售专长是一种知识，历史上卡在 AI 系统一直够不着的三个地方：资深买手、商品策划和品类经理的脑子里；没人读的三十页操作运维手册 (runbook) 里；以及 Slack 频道里——「该不该把这个产品和那个一起推荐？」的答案，住在 2023 年的一条帖子里。</mark>

Skills capture this knowledge in a form that the company's customer-facing systems will actually use.

<mark>技能把这种知识捕获成公司面向客户的系统真的会用的形式。</mark>

---

## What the architecture looks like

<mark>架构长什么样</mark>

![A skills-first retail architecture](image_011_page_54.png)

<mark>[图片_011：技能优先的零售架构 - 第 54 页]</mark>

Figure 11. A skills-first retail architecture (illustrative). Customer surfaces (web chat, mobile app, in-store kiosk, voice agent) sit above an agent runtime that loads skills carrying merchandising, category, and compliance knowledge. The tools below are accessed via MCP and managed search integrations.

<mark>图 11. 一套技能优先的零售架构（示意）。客户触点（网页聊天、移动应用、店内自助机、语音智能体）位于智能体运行时之上，运行时加载携带商品、品类和合规知识的技能。下面的工具 (Tools) 通过模型上下文协议 (Model Context Protocol, MCP) 和托管搜索集成来访问。</mark>

The architecture has three layers. The top layer is the customer surface: chat on the website, the mobile app, an in-store kiosk, a voice agent in the call center. Each surface is thin. It forwards user input to the runtime and renders the response.

<mark>架构有三层。顶层是客户触点：网站上的聊天、移动应用、店内自助机、呼叫中心里的语音智能体。每个触点都很薄。它把用户输入转给运行时，并渲染响应。</mark>

The middle layer is the agent runtime and the orchestrator that maintains the conversation, loads skills, calls tools, and assembles the reply.

<mark>中间层是智能体运行时和编排器 (Orchestration)。它维持对话，加载技能，调用工具，并组装回复。</mark>

The bottom layer is the data and tools plane: the product catalog (often millions of SKUs), live inventory with store-level location data, customer profile and order history, the project knowledge base, and vector search over reviews, manuals, and specification sheets.

<mark>底层是数据和工具平面：产品目录（常常是数百万 SKU）、带门店级位置数据的实时库存、客户档案和订单历史、项目知识库，以及对评论、手册和规格表的向量搜索。</mark>

What matters for this whitepaper is the middle layer. The runtime itself is generic: Google's Agent Development Kit, Anthropic's Claude Agent SDK, or any of the other runtimes that support the open Skills standard. The skills loaded into that runtime are specific to the retailer's domain, and they are what carry the brand's expertise to the customer.

<mark>对这份白皮书重要的是中间层。运行时本身是通用的：Google 的 Agent Development Kit、Anthropic 的 Claude Agent SDK，或其他任何支持开放技能标准的运行时。装进那个运行时的技能是零售商领域专用的，它们才是把品牌专长送到客户面前的东西。</mark>

---

## An illustrative skills library

<mark>一个示意性的技能库</mark>

What does that library actually look like? Below is a representative set of skills a major home-improvement retailer would plausibly maintain. Each is one folder. Each has a single owner. Each has its own eval suite (using the patterns from Section 4). Together, they constitute the company's working memory of how it serves customers.

<mark>那个技能库实际上长什么样？下面是一家大型家居建材零售商大概会维护的一组有代表性的技能。每一个都是一个文件夹。每一个都有单一所有者。每一个都有自己的评估套件（用第 4 节的模式）。合在一起，它们构成公司服务客户方式的工作记忆 (Memory)。</mark>

- project-guidance. Encodes the trades' knowledge that turns a vague query ("how do I tile a shower?") into a step-by-step plan. Includes structural dependencies (substrate must be waterproofed before tiling), ordering logic (cuts before installation), and common-mistake callouts. Owned by the trades knowledge team. Read-only tier.

<mark>project-guidance。编码工种知识，把一句含糊的查询（「how do I tile a shower?」）变成逐步计划。包括结构依赖（贴砖之前基层必须做好防水）、顺序逻辑（先切割再安装），以及常见错误提示。由工种知识团队拥有。只读 (Read-Only) 层。</mark>

- materials-list. Takes a project description (voice, text, or partial list) and produces a grouped bill-of-materials, including items the contractor is likely to forget. Owned by Pro merchandising. Draft-only tier: the customer reviews before purchasing.

<mark>materials-list。接收项目描述（语音、文本，或部分清单），产出分组的物料清单，包括承包商很可能忘掉的物品。由专业客户商品团队拥有。仅草稿 (Draft-Only) 层：客户先审阅，再购买。</mark>

- review-summarize. Condenses long product reviews into pros, cons, and common use cases. Triggered when the customer asks about real-world experience with a product. Owned by personalization. Read-only tier.

<mark>review-summarize。把很长的产品评论压缩成优点、缺点和常见用法。当客户询问某件产品的真实使用体验时触发 (Trigger)。由个性化团队拥有。只读层。</mark>

- delivery-window. Computes last-mile delivery options and ETAs given the customer's location, the store's availability, and the company's freight network. Owned by fulfillment. Read-only tier.

<mark>delivery-window。根据客户位置、门店可供情况和公司货运网络，计算最后一公里的配送选项和预计到达时间。由履约团队拥有。只读层。</mark>

- return-policy. Encodes the company's return rules, including the dozens of exceptions for special-order items, hazardous materials, custom cuts, and contract pricing. Owned by customer service. Read-only tier. Promotion to action-allowed (e.g. issuing a refund) requires a second skill with much tighter review.

<mark>return-policy。编码公司的退货规则，包括特殊订购商品、危险品、定制切割和合同价的几十条例外。由客户服务拥有。只读层。若要晋级到允许执行 (Action-Allowed)（例如开出退款），需要第二个技能，审阅要紧得多。</mark>

Each one is small enough to be reviewed, tested, and shipped independently.

<mark>每一个都小到可以独立审阅、测试和交付。</mark>

---

## How does the same query route through the library

<mark>同一个查询如何在技能库中路由</mark>

Consider what happens when a customer asks: "I want to remodel my kids' bathroom, what do I need?"

<mark>考虑客户问这句话时会发生什么：「I want to remodel my kids' bathroom, what do I need?」</mark>

The runtime loads the L1 descriptions of all skills at session start (~30 to 80 tokens each, ~2KB total). It identifies that project-guidance matches and loads its body, which produces an outline of the renovation steps. If the customer follows up about delivery, the delivery-window skill loads. If they ask about returns on a specific item, return-policy loads. The previous skills can stay in context or be released as the conversation moves.

<mark>运行时在会话开始时加载所有技能的 L1 描述（每个约 30 到 80 token，合计约 2KB）。它识别出 project-guidance 匹配，并加载其正文，正文产出翻新步骤的大纲。如果客户接着问配送，就加载 delivery-window 技能。如果他们问某件具体商品的退货，就加载 return-policy。先前的技能可以留在上下文里，也可以随着对话推进被释放。</mark>

Notice what does not happen. There is no monolithic "remodeling assistant" agent that has been trained on every possible remodeling scenario. Each piece of expertise is loaded into context only when the conversation reaches it. The active context stays small. The available capability is effectively unbounded.

<mark>注意什么没有发生。没有一个单体的「翻新助手」智能体，被训练来覆盖每一种可能的翻新场景。每一块专长只在对话走到它时才加载进上下文。活跃上下文保持很小。可用能力实际上不受限。</mark>

---

## Ownership: who writes which skill

<mark>所有权：谁来写哪一个技能</mark>

The single most important governance decision a retailer makes about its skills library is who owns each skill. The principle is to distribute ownership to the teams that already own the underlying expertise:

<mark>零售商对技能库做出的最重要的治理决定，是谁拥有每一个技能。原则是把所有权分给已经拥有底层专长的团队：</mark>

| Skill family | Owner team | Why |
| --- | --- | --- |
| project-guidance, product-fit | Trades knowledge / category mgmt. | These teams hold the merchandising and trade rules; they edit them weekly anyway |
| materials-list | Pro merchandising | The Pro segment's specific BOM logic is owned by the Pro team |
| delivery-window | Store operations / fulfillment | Real-time inventory and freight rules change constantly; the team that handles them owns the skill |
| review-summarize | Personalization / data science | Closest to the underlying NLP and customer feedback signals |

<mark>表 5：分布式所有权模型，把零售技能族映射到负责其底层业务逻辑的领域团队。</mark>

| <mark>技能族</mark> | <mark>所有者团队</mark> | <mark>原因</mark> |
| --- | --- | --- |
| project-guidance, product-fit | <mark>工种知识 / 品类管理</mark> | <mark>这些团队掌握商品和工种规则；他们本来每周都在改这些规则</mark> |
| materials-list | <mark>专业客户商品</mark> | <mark>专业客群特有的物料清单逻辑由专业客户团队拥有</mark> |
| delivery-window | <mark>门店运营 / 履约</mark> | <mark>实时库存和货运规则不断变化；处理它们的团队拥有这个技能</mark> |
| review-summarize | <mark>个性化 / 数据科学</mark> | <mark>离底层自然语言处理和客户反馈信号最近</mark> |

Table 5: Distributed ownership model mapping retail skill families to the domain teams responsible for their underlying business logic.

<mark>表 5：分布式所有权模型，把零售技能族映射到负责其底层业务逻辑的领域团队。</mark>

---

## The read / draft / act ladder

<mark>只读 / 草稿 / 执行阶梯</mark>

The second governance decision is what each skill is allowed to do. This is the same tier model from Section 4, applied with retail-specific examples:

<mark>第二个治理决定是每个技能被允许做什么。这就是第 4 节的层级模型，配上零售专用的例子：</mark>

| Tier | Capability | Review | Examples |
| --- | --- | --- | --- |
| Read-Only | May fetch, query, or describe data; cannot mutate state | Domain team approval | review-summarize, store-locator, project-guidance |
| Draft-Only | May produce content for human review; cannot send or commit | Domain team + format owner | draft-customer-email, materials-list |
| Action-Allowed | May execute irreversible operations on real systems | Domain team + security/compliance + executive sign-off | issue-refund, send-customer-message, reserve-inventory |

<mark>表 6：只读 / 草稿 / 执行的治理阶梯，分类技能能力、审阅要求和操作示例。</mark>

| <mark>层级</mark> | <mark>能力</mark> | <mark>审阅</mark> | <mark>示例</mark> |
| --- | --- | --- | --- |
| <mark>只读 (Read-Only)</mark> | <mark>可以获取、查询或描述数据；不能改变状态</mark> | <mark>领域团队批准</mark> | review-summarize, store-locator, project-guidance |
| <mark>仅草稿 (Draft-Only)</mark> | <mark>可以产出供人审阅的内容；不能发送或提交</mark> | <mark>领域团队 + 格式所有者</mark> | draft-customer-email, materials-list |
| <mark>允许执行 (Action-Allowed)</mark> | <mark>可以在真实系统上执行不可逆操作</mark> | <mark>领域团队 + 安全 / 合规 + 高管签批</mark> | issue-refund, send-customer-message, reserve-inventory |

Table 6: The read/draft/act governance ladder classifying skill capabilities, review requirements, and operational examples.

<mark>表 6：只读 / 草稿 / 执行治理阶梯，对技能能力、审阅要求和操作示例进行分类。</mark>

This is far more defensible to a security team, and to the regulator who eventually shows up, than the alternative: a black-box agent that does whatever its training plus its system prompt produce.

<mark>对安全团队，以及对最终会出现的监管者，这比另一种做法好辩护得多。另一种做法是一个黑盒智能体，训练加上系统提示词产出什么，它就做什么。</mark>

---

## Why is this harder to compete with than a custom agent

<mark>为什么这比定制智能体更难被追上</mark>

If the competitor and our retailer are both running on the same generic agent runtime (and they are, because the runtime has commoditized), then matching the runtime is trivial. The skills library encodes the company's accumulated patterns. This is the central strategic point of the whitepaper.

<mark>如果竞争对手和我们这家零售商都跑在同一个通用智能体运行时上（他们确实如此，因为运行时已经商品化），那么对齐运行时是微不足道的。技能库编码的是公司积累下来的模式。这是白皮书的核心战略论点。</mark>

A retailer that invests heavily in custom agents but neglects its skills library is investing in the part of the stack that competitors will reach for free. A retailer that invests in skills, even on a generic runtime, is building a durable asset that captures what the company actually knows.

<mark>一家在定制智能体上重金投入、却忽视技能库的零售商，投的是竞争对手会免费拿到的那一层。一家投资技能的零售商，即便跑在通用运行时上，也是在建一块耐久资产，捕获公司真正知道的东西。</mark>

---

## Cold start: where to actually begin

<mark>冷启动：到底从哪里开始</mark>

A useful exercise: take the team's most experienced practitioner aside for an hour, ask them to narrate three workflows they do regularly, and record the conversation. The transcript is, almost literally, the first draft of three skills. This is the kind of work that, before skills, had no obvious home. It now has one.

<mark>一个有用的练习：把团队里最有经验的实践者单独约出来一个小时，请他们口述三件经常做的工作流，并把对话录下来。转录几乎就是三个技能的第一稿。这类工作在技能出现之前没有明显的家。现在有了。</mark>

Ling, G., Zhong, S., & Huang, R. (2026). Agent Skills: A Data-Driven Analysis of Claude Skills for Extending Large Language Model Functionality. arXiv:2602.08004. Analysis of 40,285 publicly listed skills from a major marketplace.

<mark>Ling, G., Zhong, S., & Huang, R. (2026). Agent Skills: A Data-Driven Analysis of Claude Skills for Extending Large Language Model Functionality. arXiv:2602.08004. 对一个主要市场上 40,285 个公开上架技能的分析。</mark>

Google Cloud Blog. (2026, April). Level Up Your Agents: Announcing Google's Official Skills Repository. https://cloud.google.com/blog/topics/developers-practitioners/level-up-your-agents-announcing-googles-official-skills-repository. Repository: https://github.com/google/skills. Installable via `npx skills install github.com/google/skills` for Antigravity, and any compliant coding agent.

<mark>Google Cloud Blog. (2026, April). Level Up Your Agents: Announcing Google's Official Skills Repository. https://cloud.google.com/blog/topics/developers-practitioners/level-up-your-agents-announcing-googles-official-skills-repository. 仓库：https://github.com/google/skills. 可通过 `npx skills install github.com/google/skills` 安装，用于 Antigravity 以及任何兼容的编码智能体。</mark>

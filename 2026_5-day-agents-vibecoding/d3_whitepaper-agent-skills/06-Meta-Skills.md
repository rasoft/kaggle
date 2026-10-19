# 6. On Meta-Skills and Self-Improving Skills

<mark>6. 论元技能 (Meta-skill) 与自我改进技能</mark>

So far, every skill in this document has been written by a human. A domain expert sits down, drafts a SKILL.md, tests it, ships it. That's the right place to start. But once you have a working library, the natural next question is: can the agent help write, evaluate, and improve skills too?

<mark>到目前为止，本文里的每个技能 (Skill) 都是人写的。领域专家坐下来，起草一份 SKILL.md，测试它，交付它。这是正确的起点。但一旦你有了一个能用的技能库，下一个自然的问题是：智能体 (Agent) 能不能也帮忙写、评估和改进技能？</mark>

This is the meta-skills territory. Skills whose job is to author, evaluate, or improve other skills. In practice, these "meta-skills" fall into four buckets:

<mark>这就是元技能的领地。职责是撰写、评估或改进其他技能的技能。实践中，这些「元技能」落进四类：</mark>

1. Authoring. Skills that take a description of a workflow and produce a draft SKILL.md. Google's ADK<sup>21</sup> has a "skill factory" pattern that does this through its SkillToolset. Anthropic ships a skill-creator Skill<sup>22</sup> that walks you through creation, evaluation, and tuning.

<mark>1. 撰写。这类技能接收一份工作流描述，产出一份 SKILL.md 草稿。Google 的 ADK<sup>21</sup> 有一种「技能工厂」模式，通过 SkillToolset 来做这件事。Anthropic 提供一个 skill-creator 技能<sup>22</sup>，带你走完创建、评估 (Evaluation) 和调优。</mark>

2. Assisted authoring from traces. Instead of asking a human to describe a workflow, watch the agent do it successfully a few times, then turn that trace into a skill. The skill-creator workflow supports this directly through trace-based harvesting. The human's job shifts from writing the skill to confirming that the harvested version captures the right steps.

<mark>2. 从轨迹辅助撰写。不要请人描述工作流，而是看智能体成功做几次，再把那条轨迹变成技能。skill-creator 工作流通过基于轨迹的收获直接支持这一点。人的工作从写技能，变成确认收获来的版本抓住了正确的步骤。</mark>

![Trace-to-skill authoring loop](image_009_page_36.png)

<mark>[图片_009：从轨迹到技能的撰写循环 - 第 36 页]</mark>

Figure 9: The step-by-step loop demonstrates how real, successful production histories are transformed into reliable procedural memories without manual human drafting.

<mark>图 9：这个逐步循环展示了真实、成功的生产历史如何被转成可靠的程序性记忆 (Procedural Memory)，而不必由人手动起草。</mark>

3. Improvement. Skills that take an existing skill plus a set of failing evaluation cases and propose edits. Saboo's SkillOptimizer<sup>24</sup> and Anthropic's description-optimization loop are both examples. Another is Karpathy's autoresearch pattern<sup>25</sup>, where an agent proposes a change to a target file, runs a bounded experiment, and keeps the change only if a metric improves.

<mark>3. 改进。这类技能拿一个已有技能加上一组失败的评估用例，并提议修改。Saboo 的 SkillOptimizer<sup>24</sup> 和 Anthropic 的描述优化循环都是例子。另一个是 Karpathy 的 autoresearch 模式<sup>25</sup>：智能体对目标文件提议一处修改，跑一个有界实验，只有指标变好才保留修改。</mark>

![Evaluation gating before a skill change is committed](image_010_page_37.png)

<mark>[图片_010：技能修改提交前的评估门禁 - 第 37 页]</mark>

Figure 10: Notice the evaluation gating. The agent can suggest changes to descriptions or instructions, but it cannot commit them to the library unless the unit tests pass.

<mark>图 10：注意评估门禁。智能体可以建议修改描述或指令，但单元测试不通过，就不能把它们提交进技能库。</mark>

4. Library evolution. Skills that grow the library over time, the way Voyager grew its own Minecraft skill library<sup>26</sup>. The agent finishes a task it had no skill for, notices that it just solved a recurring problem, and proposes adding a new skill to cover it. Schmid's self-learning-skill<sup>27</sup> is a community reference implementation of this pattern.

<mark>4. 技能库演化。这类技能随时间让技能库长大，就像 Voyager 长出自己的 Minecraft 技能库<sup>26</sup>。智能体完成了一个它没有技能可依的任务，注意到自己刚刚解决了一个会反复出现的问题，并提议加一个新技能来覆盖它。Schmid 的 self-learning-skill<sup>27</sup> 是这个模式的一个社区参考实现。</mark>

---

## Where this falls apart

<mark>它在哪里会垮掉</mark>

Meta-skills only work if your evaluation suite is good. An agent that's allowed to edit its own skills will happily optimize for whatever metric you point it at, including metrics that are easy to game. The Section 4 evaluation work is what keeps this honest. Without solid trigger accuracy tests, regression tests, and human spot-checks, an autonomous improvement loop will quietly make your library worse while reporting that it's getting better.

<mark>元技能只有在评估套件足够好时才成立。一个被允许修改自己技能的智能体，会开心地优化你指向的任何指标，包括那些容易被刷的指标。第 4 节的评估工作就是让这件事保持诚实的东西。没有扎实的触发准确率测试、回归测试和人工抽查，自主改进循环会一边报告自己在变好，一边悄悄把技能库弄差。</mark>

A few habits that have held up:

<mark>几条已经经住检验的习惯：</mark>

- Anything an agent writes enters the library at the draft tier, regardless of how confident the meta-skill is. It graduates through the same Read / Draft / Act ladder from Section 4 as any human-written skill.

<mark>智能体写的任何东西，都以草稿层进入技能库，不管元技能自己有多自信。它和任何人手写的技能一样，沿着第 4 节的只读 / 草稿 / 执行阶梯晋级。</mark>

- Keep a human in the loop for the first few edits. Even when the metric clearly improves, scan the diff. The kind of mistake an agent makes (overfitting the description to a few test cases, breaking a downstream skill it didn't know existed) is exactly the kind a human catches in 30 seconds.

<mark>前几次修改要让人留在回路里。即便指标明显变好，也扫一眼 diff。智能体会犯的那种错（把 description 过拟合到少数测试用例上，弄坏一个它不知道存在的下游技能），正好是人在 30 秒里能抓住的那种。</mark>

- Don't start with meta-skills. Get the manual authoring loop working first. The fastest way to get a bad library is to point an agent at an empty folder and ask it to generate fifty skills.

<mark>不要从元技能开始。先让手工撰写的循环跑起来。得到一个糟糕技能库的最快办法，就是把智能体指向一个空文件夹，让它生成 50 个技能。</mark>

---

## Where this is going

<mark>它要走向哪里</mark>

The pattern is settling into something like: humans write the first version of every skill, meta-skills handle the repetitive part of maintenance (tuning descriptions, adding test cases, surfacing regressions), and a small subset of teams experiment with full self-extension. The interesting frontier is the third category, where the agent proposes new skills based on what it sees in production traffic. It's promising. It's also where things go wrong fastest if the evaluation gates aren't tight.

<mark>这个模式正在落成这样：每个技能的第一版由人来写，元技能处理维护里重复的部分（调 description、补测试用例、把回归浮出来），一小部分团队则试验完全的自我扩展。有意思的前沿是第三类：智能体根据它在生产流量里看到的东西，提议新技能。这很有希望。评估门禁如果不紧，这也是出事最快的地方。</mark>

The practical version of this is in Appendix A where the cheatsheet covers what to do (and not do) when you're tempted to let the agent write its own skills.

<mark>这件事的实践版本在附录 A。速查表写了：当你想让智能体给自己写技能时，该做什么，不该做什么。</mark>

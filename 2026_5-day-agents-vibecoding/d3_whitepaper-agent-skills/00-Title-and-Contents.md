# Agent Skills

智能体技能 (Agent Skills)

Authors: Tanvi Singhal, Gabriela Hernandez Larios, Debanshu Dus, Lavi Nigam, and Smitha Kolan

作者：Tanvi Singhal、Gabriela Hernandez Larios、Debanshu Dus、Lavi Nigam、Smitha Kolan

May 2026

2026 年 5 月

---

## Acknowledgements

致谢

Curators and editors

策划与编辑

Shubham Saboo

Designer

设计师

Michael Lanning

---

## Table of contents

目录

1. Introduction — 4

1. 引言 — 4

2. What is an Agent Skill (and How to Build Your First One) — 6

2. 什么是智能体技能 (Agent Skill)，以及如何构建第一个 — 6

Skill Anatomy & Progressive Disclosure — 7

技能解剖与渐进式披露 (Progressive Disclosure) — 7

Path A: Translating what you already know — 8

路径 A：翻译你已经知道的东西 — 8

Path B: Crystallizing what the agent just did — 9

路径 B：把智能体刚刚做成的事结晶下来 — 9

Trying it out & How to install Skills today — 10

试一试，以及今天如何安装技能 — 10

Wait but how does a Skill differ from MCP and AGENTS.md? — 11

等一下，技能和 MCP、AGENTS.md 有什么不同？ — 11

3. Why did Agent Skills become so popular, so fast? — 12

3. 智能体技能为什么这么快就流行起来？ — 12

Skills for chatbots, for coding agents, or for multi-agent enterprise use cases? — 13

技能是给聊天机器人、编码智能体，还是给企业级多智能体场景用的？ — 13

4. Evaluating Skills — 15

4. 评估技能 — 15

The Evaluation Toolkit — 17

评估工具箱 — 17

The trigger is the first gate — 18

触发是第一道门 — 18

Output quality and tool trajectory — 19

输出质量与工具轨迹 (tool trajectory) — 19

System vs. Skill: The Evaluation Illusion — 21

系统与技能：评估错觉 — 21

Token budget: isolation is a trap — 22

Token 预算：孤立评估是个陷阱 — 22

What "eval coverage" means — 24

「评估覆盖」是什么意思 — 24

5. From Prototype to Production — 25

5. 从原型到生产 — 25

What's actually inside an agent runtime — 27

智能体运行时里实际有什么 — 27

Why skills are the unit of improvement — 28

为什么技能是改进的单位 — 28

The failure mode that breaks demos: context overflow — 29

让演示翻车的失败模式：上下文溢出 (Context Overflow) — 29

What this means for the token budget — 31

这对 token 预算意味着什么 — 31

6. On Meta-Skills and Self-Improving Skills — 32

6. 论元技能 (Meta-skill) 与自我改进技能 — 32

Where this falls apart — 34

它在哪里会垮掉 — 34

Where this is going — 35

它要走向哪里 — 35

7. Composing and Packaging Skills — 36

7. 组合与打包技能 — 36

Execution Routing: DAG Orchestration — 36

执行路由：有向无环图编排 (DAG Orchestration) — 36

Environment Packaging: Capability Profiles — 37

环境打包：能力画像 (Capability Profile) — 37

Populating the Graph: The Canonical Skill Taxonomy — 37

填充图：规范的技能分类 — 37

Context Debt and Shifting Intelligence Left — 38

上下文债务 (Context Debt) 与智能左移 (Shift Intelligence Left) — 38

Architectural Tradeoffs — 38

架构权衡 — 38

Actionable Best Practices — 39

可执行的最佳实践 — 39

8. How to Decide Among the Hundreds of Skills That Exist — 39

8. 面对成百上千个技能，如何做选择 — 39

9. Conclusion — 41

9. 结论 — 41

Appendix A – The Practical Cheatsheet — 43

附录 A — 实用速查表 — 43

The minimal SKILL.md — 43

最小的 SKILL.md — 43

The folder structure. — 44

文件夹结构 — 44

Naming — 44

命名 — 44

The description field — 45

description 字段 — 45

The five rules — 45

五条规则 — 45

The quality principles — 46

质量原则 — 46

Do's and Don'ts — 46

该做与不该做 — 46

Skill smells (revise if you see these) — 47

技能异味（看到就要改） — 47

Eval coverage checklist — 48

评估覆盖清单 — 48

Deployment checklist — 48

部署清单 — 48

One-line mental model — 49

一句话心智模型 — 49

Where to start tomorrow — 49

明天从哪里开始 — 49

Appendix B – Case Study: Domain Expertise as Code (Vertical Skills in Retail) — 50

附录 B — 案例研究：把领域专长写成代码（零售业的垂直技能） — 50

Why retail is the canonical case for skills — 50

为什么零售是技能的典型场景 — 50

What the architecture looks like — 51

架构长什么样 — 51

An illustrative skills library — 52

一个示意性的技能库 — 52

How does the same query route through the library — 53

同一个查询如何在技能库中路由 — 53

Ownership: who writes which skill — 54

所有权：谁来写哪一个技能 — 54

The read / draft / act ladder — 55

只读 / 草稿 / 执行阶梯 — 55

Why is this harder to compete with than a custom agent — 55

为什么这比定制智能体更难被追上 — 55

Cold start: where to actually begin — 56

冷启动：到底从哪里开始 — 56

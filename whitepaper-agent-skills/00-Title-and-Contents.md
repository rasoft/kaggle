# Agent Skills

<mark>智能体技能 (Agent Skills)</mark>

Authors: Tanvi Singhal, Gabriela Hernandez Larios, Debanshu Dus, Lavi Nigam, and Smitha Kolan

<mark>作者：Tanvi Singhal、Gabriela Hernandez Larios、Debanshu Dus、Lavi Nigam、Smitha Kolan</mark>

May 2026

<mark>2026 年 5 月</mark>

---

## Acknowledgements

<mark>致谢</mark>

Curators and editors

<mark>策划与编辑</mark>

Shubham Saboo

Designer

<mark>设计师</mark>

Michael Lanning

---

## Table of contents

<mark>目录</mark>

1. Introduction — 4

<mark>1. 引言 — 4</mark>

2. What is an Agent Skill (and How to Build Your First One) — 6

<mark>2. 什么是智能体技能 (Agent Skill)，以及如何构建第一个 — 6</mark>

Skill Anatomy & Progressive Disclosure — 7

<mark>技能解剖与渐进式披露 (Progressive Disclosure) — 7</mark>

Path A: Translating what you already know — 8

<mark>路径 A：翻译你已经知道的东西 — 8</mark>

Path B: Crystallizing what the agent just did — 9

<mark>路径 B：把智能体刚刚做成的事结晶下来 — 9</mark>

Trying it out & How to install Skills today — 10

<mark>试一试，以及今天如何安装技能 — 10</mark>

Wait but how does a Skill differ from MCP and AGENTS.md? — 11

<mark>等一下，技能和 MCP、AGENTS.md 有什么不同？ — 11</mark>

3. Why did Agent Skills become so popular, so fast? — 12

<mark>3. 智能体技能为什么这么快就流行起来？ — 12</mark>

Skills for chatbots, for coding agents, or for multi-agent enterprise use cases? — 13

<mark>技能是给聊天机器人、编码智能体，还是给企业级多智能体场景用的？ — 13</mark>

4. Evaluating Skills — 15

<mark>4. 评估技能 — 15</mark>

The Evaluation Toolkit — 17

<mark>评估工具箱 — 17</mark>

The trigger is the first gate — 18

<mark>触发是第一道门 — 18</mark>

Output quality and tool trajectory — 19

<mark>输出质量与工具轨迹 (tool trajectory) — 19</mark>

System vs. Skill: The Evaluation Illusion — 21

<mark>系统与技能：评估错觉 — 21</mark>

Token budget: isolation is a trap — 22

<mark>Token 预算：孤立评估是个陷阱 — 22</mark>

What "eval coverage" means — 24

<mark>「评估覆盖」是什么意思 — 24</mark>

5. From Prototype to Production — 25

<mark>5. 从原型到生产 — 25</mark>

What's actually inside an agent runtime — 27

<mark>智能体运行时里实际有什么 — 27</mark>

Why skills are the unit of improvement — 28

<mark>为什么技能是改进的单位 — 28</mark>

The failure mode that breaks demos: context overflow — 29

<mark>让演示翻车的失败模式：上下文溢出 (Context Overflow) — 29</mark>

What this means for the token budget — 31

<mark>这对 token 预算意味着什么 — 31</mark>

6. On Meta-Skills and Self-Improving Skills — 32

<mark>6. 论元技能 (Meta-skill) 与自我改进技能 — 32</mark>

Where this falls apart — 34

<mark>它在哪里会垮掉 — 34</mark>

Where this is going — 35

<mark>它要走向哪里 — 35</mark>

7. Composing and Packaging Skills — 36

<mark>7. 组合与打包技能 — 36</mark>

Execution Routing: DAG Orchestration — 36

<mark>执行路由：有向无环图编排 (DAG Orchestration) — 36</mark>

Environment Packaging: Capability Profiles — 37

<mark>环境打包：能力画像 (Capability Profile) — 37</mark>

Populating the Graph: The Canonical Skill Taxonomy — 37

<mark>填充图：规范的技能分类 — 37</mark>

Context Debt and Shifting Intelligence Left — 38

<mark>上下文债务 (Context Debt) 与智能左移 (Shift Intelligence Left) — 38</mark>

Architectural Tradeoffs — 38

<mark>架构权衡 — 38</mark>

Actionable Best Practices — 39

<mark>可执行的最佳实践 — 39</mark>

8. How to Decide Among the Hundreds of Skills That Exist — 39

<mark>8. 面对成百上千个技能，如何做选择 — 39</mark>

9. Conclusion — 41

<mark>9. 结论 — 41</mark>

Appendix A – The Practical Cheatsheet — 43

<mark>附录 A — 实用速查表 — 43</mark>

The minimal SKILL.md — 43

<mark>最小的 SKILL.md — 43</mark>

The folder structure. — 44

<mark>文件夹结构 — 44</mark>

Naming — 44

<mark>命名 — 44</mark>

The description field — 45

<mark>description 字段 — 45</mark>

The five rules — 45

<mark>五条规则 — 45</mark>

The quality principles — 46

<mark>质量原则 — 46</mark>

Do's and Don'ts — 46

<mark>该做与不该做 — 46</mark>

Skill smells (revise if you see these) — 47

<mark>技能异味（看到就要改） — 47</mark>

Eval coverage checklist — 48

<mark>评估覆盖清单 — 48</mark>

Deployment checklist — 48

<mark>部署清单 — 48</mark>

One-line mental model — 49

<mark>一句话心智模型 — 49</mark>

Where to start tomorrow — 49

<mark>明天从哪里开始 — 49</mark>

Appendix B – Case Study: Domain Expertise as Code (Vertical Skills in Retail) — 50

<mark>附录 B — 案例研究：把领域专长写成代码（零售业的垂直技能） — 50</mark>

Why retail is the canonical case for skills — 50

<mark>为什么零售是技能的典型场景 — 50</mark>

What the architecture looks like — 51

<mark>架构长什么样 — 51</mark>

An illustrative skills library — 52

<mark>一个示意性的技能库 — 52</mark>

How does the same query route through the library — 53

<mark>同一个查询如何在技能库中路由 — 53</mark>

Ownership: who writes which skill — 54

<mark>所有权：谁来写哪一个技能 — 54</mark>

The read / draft / act ladder — 55

<mark>只读 / 草稿 / 执行阶梯 — 55</mark>

Why is this harder to compete with than a custom agent — 55

<mark>为什么这比定制智能体更难被追上 — 55</mark>

Cold start: where to actually begin — 56

<mark>冷启动：到底从哪里开始 — 56</mark>

# 1. Introduction

<mark>1. 引言</mark>

Agent Skills are a way to equip your agent with knowledge and company context. An Agent Skill is a folder containing a SKILL.md file, with scripts/, references/, and assets/ directories. Section 2 covers the anatomy in detail.

<mark>智能体技能 (Agent Skill) 是一种为智能体 (Agent) 配备知识和公司上下文的方式。一个智能体技能是一个文件夹，其中包含 SKILL.md 文件，以及 scripts/、references/ 和 assets/ 目录。第 2 节会详细讲它的解剖结构。</mark>

Agent Skills are becoming the standard for cross-platform portability. But why the sudden adoption velocity? We believe Agent Skills tackle four main friction points in AI agent development:

<mark>智能体技能正在成为跨平台可移植性的标准。但为什么采用速度会突然这么快？我们认为，智能体技能打中了 AI 智能体开发里的四个主要摩擦点：</mark>

1. Too many instructions, worse results. Dumping every instruction you can think of into a single system prompt inevitably degrades Large Language Model (LLM) performance, a problem known as context rot. Skills solve this by loading exclusively on demand. Section 5 unpacks the research behind this.

<mark>1. 指令太多，效果更差。把能想到的每条指令都倒进同一个系统提示词，必然拉低大语言模型 (LLM) 的表现。这个问题叫上下文腐烂 (Context Rot)。技能的解法是只按需加载。第 5 节会展开背后的研究。</mark>

> Agent Skills turn any general-purpose agent into a specialist on demand. No context bloat. Portable and lightweight.

<mark>智能体技能按需把任何通用智能体变成专家。没有上下文臃肿。可移植，而且轻量。</mark>

2. Knowing how, not just knowing what. LLMs already have reasonable analogs for remembering what happened (episodic memory) and remembering facts (semantic memory). What they've lacked is a way to remember how to do things step by step, which is called procedural memory. Agent Skills can be seen as the first credible procedural memory primitive for LLM Agents.

<mark>2. 要知道怎么做，而不只是知道是什么。大语言模型已经有了还算可用的类比：记住发生过什么（情景记忆，episodic memory），以及记住事实（语义记忆，semantic memory）。它们缺的是一种逐步记住「怎么做」的方式，这叫程序性记忆 (Procedural Memory)。智能体技能可以看作大语言模型智能体第一个站得住的程序性记忆原语。</mark>

3. Multi-agent overload. The ecosystem was flooded with complex multi-agent systems that are notoriously hard to build and maintain. While still necessary for certain tasks, Skills allow a single general-purpose agent to seamlessly flex into many specialist roles. Section 3 develops this argument in depth, with a worked example.

<mark>3. 多智能体过载。生态里涌进了大量复杂的多智能体系统，它们出了名地难建、难维护。某些任务仍然需要多智能体，但技能让单个通用智能体可以顺滑地切换成许多专家角色。第 3 节会把这个论点展开，并给出一个算例。</mark>

4. Portability. A folder with a markdown file is a remarkably lightweight primitive. Any agent with filesystem access can use them, making them perfectly portable across a multi-vendor AI landscape.

<mark>4. 可移植性。一个装着 Markdown 文件的文件夹，是轻得惊人的原语。任何能访问文件系统的智能体都能使用它们，因此它们可以在多厂商的 AI 版图里自由迁移。</mark>

In this whitepaper, we cater to two personas: Builders (those using Skills) and Developers (those creating, versioning, and managing them). We’ll gently walk through what a Skill is and how to use it (Sections 2 to 3), before diving into complex Developer topics like evaluation, production readiness, meta-skills, and composition (Sections 4 to 8).

<mark>这份白皮书面向两种人：构建者 (Builder)，也就是使用技能的人；以及开发者 (Developer)，也就是创建、版本化并管理技能的人。我们会先把技能是什么、怎么用讲清楚（第 2 节到第 3 节），再进入更复杂的开发者主题：评估 (Evaluation)、生产就绪、元技能 (Meta-skill) 和组合（第 4 节到第 8 节）。</mark>

(Impatient? Appendix A offers a printable operational cheat sheet, and Appendix B walks through a retail case study).

<mark>（等不及了？附录 A 是一份可打印的操作速查表，附录 B 走一遍零售案例。）</mark>

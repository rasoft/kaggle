# Agent Tools & Interoperability

<mark>智能体工具与互操作性 (Agent Tools & Interoperability)</mark>

Authors: Kanchana Patlolla, Łukasz Olejniczak, and Pier Paolo Ippolito

<mark>作者：Kanchana Patlolla、Łukasz Olejniczak、Pier Paolo Ippolito</mark>

May 2026

<mark>2026 年 5 月</mark>

---

## Acknowledgements

<mark>致谢</mark>

Content contributors

<mark>内容贡献者</mark>

Alan Blount

Mike Smith

Anant Nawalgaria

Lukas Geiger

Curators and editors

<mark>策划与编辑</mark>

Anant Nawalgaria

Designer

<mark>设计师</mark>

Michael Lanning

---

## Table of contents

<mark>目录</mark>

Introduction — 6

<mark>引言 — 6</mark>

Why this paper, why now — 8

<mark>为什么是这篇，为什么是现在 — 8</mark>

Who this paper is for — 9

<mark>这篇写给谁 — 9</mark>

The Vibe Coder’s View of MCP: Discovery, Configuration, & Connection — 10

<mark>氛围编码者眼中的 MCP：发现、配置与连接 — 10</mark>

Discovery — 11

<mark>发现 — 11</mark>

Configuration — 12

<mark>配置 — 12</mark>

Connection — 12

<mark>连接 — 12</mark>

Bypassing the NxM Prototyping Problem — 13

<mark>绕开 N×M 原型问题 — 13</mark>

Why is this important? — 14

<mark>这件事为什么重要？ — 14</mark>

Debugging Issues with MCP Servers — 15

<mark>调试 MCP 服务器的问题 — 15</mark>

Vibe Coder Toolkit: Best Practices for MCP Consumption — 15

<mark>氛围编码者工具箱：消费 MCP 的最佳实践 — 15</mark>

Agent-to-Agent (A2A) Interoperability — 17

<mark>智能体对智能体 (A2A) 互操作性 — 17</mark>

The Evolution of Agentic Architectures — 17

<mark>智能体架构的演化 — 17</mark>

Bounded vs. Unbounded Domains — 23

<mark>有界领域与无界领域 — 23</mark>

The GOTO Problem in Agentic Architecture — 24

<mark>智能体架构里的 GOTO 问题 — 24</mark>

Building the Virtual Workforce — 24

<mark>组建虚拟劳动力 — 24</mark>

The Agent Card — 25

<mark>智能体名片 — 25</mark>

Registries: From Public Marketplaces to Private Enterprises — 25

<mark>注册表：从公开市场到企业内部 — 25</mark>

Implementing A2A Protocols — 26

<mark>实现 A2A 协议 — 26</mark>

Exposing A2A Agent — 26

<mark>把智能体暴露为 A2A 智能体 — 26</mark>

Connecting Remote A2A Agents — 27

<mark>连接远程 A2A 智能体 — 27</mark>

The Extensibility Layer: A2A as the Foundation for UI and Commerce — 28

<mark>扩展层：A2A 作为界面与商务的基础 — 28</mark>

Monetizing A2A Agents — 29

<mark>让 A2A 智能体变现 — 29</mark>

The Extensibility Layer: A2A as the Foundation for UI and Commerce — 31

<mark>扩展层：A2A 作为界面与商务的基础 — 31</mark>

Agent-to-UI (A2UI) Interoperability — 32

<mark>智能体到界面 (A2UI) 互操作性 — 32</mark>

The Communication Gap — 32

<mark>沟通缺口 — 32</mark>

Generative UI & A2UI — 32

<mark>生成式界面与 A2UI — 32</mark>

What is Generative UI? — 32

<mark>什么是生成式界面？ — 32</mark>

A2UI: A Secure Implementation — 33

<mark>A2UI：一种安全的实现 — 33</mark>

The Basic Catalog (and Bringing Your Own) — 34

<mark>基础组件目录（以及自带目录） — 34</mark>

Generating A2UI: Two Patterns — 35

<mark>生成 A2UI 的两种模式 — 35</mark>

When to Use Each Pattern — 37

<mark>何时用哪一种 — 37</mark>

Interactive Artifacts & The Canvas — 38

<mark>交互式工件与画布 — 38</mark>

Canvas + A2UI — 39

<mark>画布 + A2UI — 39</mark>

Best Practices — 40

<mark>最佳实践 — 40</mark>

Let LLMs Generate A2UI — 40

<mark>让大语言模型生成 A2UI — 40</mark>

Hybrid Output for Flexibility — 42

<mark>混合输出，换取灵活 — 42</mark>

Summary — 43

<mark>小结 — 43</mark>

Agents and Commerce (AP2 and UCP) — 43

<mark>智能体与商务（AP2 与 UCP） — 43</mark>

Autonomous Procurement with a workflow example — 43

<mark>用一个工作流例子看自主采购 — 43</mark>

Key characteristics and benefits of Protocols — 43

<mark>协议的关键特征与好处 — 43</mark>

What is AP2 and UCP? — 44

<mark>AP2 和 UCP 是什么？ — 44</mark>

UCP (Universal Commerce Protocol): The Ultimate Food Delivery App — 45

<mark>UCP（通用商务协议）：终极外卖应用 — 45</mark>

AP2 (Agent Payments Protocol): The Parent's Credit Card with Strict Rules — 46

<mark>AP2（智能体支付协议）：带着严格规则的家长信用卡 — 46</mark>

Conclusion — 47

<mark>结论 — 47</mark>

Endnotes — 48

<mark>尾注 — 48</mark>

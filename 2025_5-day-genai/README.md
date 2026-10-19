# 5-Day Gen AI Intensive Course with Google

<mark>与 Google 一起的 5 日生成式 AI 强化课程</mark>

Source: [https://www.kaggle.com/learn-guide/5-day-genai](https://www.kaggle.com/learn-guide/5-day-genai)

<mark>原文：[https://www.kaggle.com/learn-guide/5-day-genai](https://www.kaggle.com/learn-guide/5-day-genai)</mark>

Each English paragraph is followed by its Chinese translation.

<mark>英文段落后紧跟中文。</mark>

---

5-Day Gen AI Intensive Course with Google — Originally held live from March 31 to April 4, 2025, this program is now available as a self-paced learning guide for anyone interested in exploring the fundamental technologies and techniques behind Generative AI.

<mark>与 Google 一起的 5 日生成式 AI 强化课程最初于 2025 年 3 月 31 日至 4 月 4 日以直播形式举办。它现在作为自定进度的学习指南开放，供任何有兴趣探索生成式 AI (Generative AI) 背后基础技术与方法的人学习。</mark>

---

## What's covered?

<mark>课程涵盖什么？</mark>

- **Day 1: Foundational Models & Prompt Engineering** — Explore the evolution of Large Language Models (LLMs), from transformers to techniques like fine-tuning, inference acceleration, and reasoning models. Get trained with the art of prompt engineering for optimal LLM interaction.

  **第 1 天：基础模型与提示工程 (Foundational Models & Prompt Engineering)**。探索大语言模型 (Large Language Model, LLM) 的演进：从 Transformer 到微调 (Fine-tuning)、推理加速 (Inference Acceleration) 和推理模型 (Reasoning Model) 等技术。学习提示工程 (Prompt Engineering) 这门手艺，以便与大语言模型进行最优交互。

- **Day 2: Embeddings and Vector Stores/Databases** — Learn about the conceptual underpinning of embeddings and vector databases, including embedding methods, vector search algorithms, and real-world applications with LLMs, as well as their tradeoffs.

  **第 2 天：嵌入与向量存储 / 数据库 (Embeddings and Vector Stores/Databases)**。了解嵌入 (Embeddings) 和向量数据库 (Vector Database) 的概念基础，包括嵌入方法、向量搜索 (Vector Search) 算法、与大语言模型结合的实际应用，以及其中的权衡。

- **Day 3: Generative AI Agents** — Learn to build sophisticated AI agents by understanding their core components and the iterative development process, including recent agentspace development.

  **第 3 天：生成式 AI 智能体 (Generative AI Agents)**。通过理解核心组件和迭代式开发过程，学习构建精密的 AI 智能体，内容也包括近期 Agentspace 的发展。

- **Day 4: Domain-Specific LLMs** — Delve into the creation and application of specialized LLMs like SecLM and Med-PaLM, with insights from the researchers who built them.

  **第 4 天：领域专用大语言模型 (Domain-Specific LLMs)**。深入了解 SecLM、Med-PaLM 这类专用大语言模型的构建与应用，并听取构建它们的研究人员的见解。

- **Day 5: MLOps for Generative AI** — Discover how to adapt MLOps practices for Generative AI and leverage Vertex AI's tools for foundation models and generative AI applications.

  **第 5 天：面向生成式 AI 的机器学习运维 (MLOps for Generative AI)**。了解如何把机器学习运维 (Machine Learning Operations, MLOps) 实践改造用于生成式 AI，并利用 Vertex AI 面向基础模型 (Foundation Model) 和生成式 AI 应用的工具。

- Capstone Project goes live — See Details in the FAQ.

  <mark>综合实践项目 (Capstone Project) 已上线——详见常见问题 (FAQ)。</mark>

---

## Setup Instructions

<mark>环境准备</mark>

To ensure you are ready for the course, please complete these essential setup steps:

<mark>为确保你已准备好上课，请完成这些必要的准备步骤：</mark>

- [Kaggle](https://www.kaggle.com/) account: Sign up for a Kaggle account and [learn how Notebooks work](https://www.youtube.com/watch?v=BPQDZLPtgDc). Make sure to [phone verify](https://www.kaggle.com/settings) your account, it’s necessary for the course’s codelabs.

  <mark>[Kaggle](https://www.kaggle.com/) 账号：注册一个 Kaggle 账号，并[了解 Notebook 如何工作](https://www.youtube.com/watch?v=BPQDZLPtgDc)。请务必对账号做[手机验证](https://www.kaggle.com/settings)，课程的代码实验 (codelab) 需要这一步。</mark>

- [AI Studio](https://aistudio.google.com) account: Sign up for an AI Studio account and ensure you can generate an [API key](https://aistudio.google.com/app/apikey).

  <mark>[AI Studio](https://aistudio.google.com) 账号：注册一个 AI Studio 账号，并确认你能生成 [API 密钥](https://aistudio.google.com/app/apikey)。</mark>

- [Kaggle Discord](http://discord.gg/kaggle): Sign up for a Discord account and join us on the Kaggle Discord server to connect and collaborate with fellow learners in this course.

  <mark>[Kaggle Discord](http://discord.gg/kaggle)：注册一个 Discord 账号，并加入 Kaggle Discord 服务器，与本课程的其他学习者联系、协作。</mark>

---

## Day 1 (Foundational Large Language Models & Prompt Engineering)

<mark>第 1 天（基础大语言模型与提示工程）</mark>

Welcome to Day 1.

<mark>欢迎来到第 1 天。</mark>

Today you’ll explore the evolution of LLMs, from transformers to techniques like fine-tuning and inference acceleration. You’ll also get trained in the art of prompt engineering for optimal LLM interaction and evaluating LLMs.

<mark>今天你将探索大语言模型的演进，从 Transformer 到微调和推理加速等技术。你还将学习提示工程，以便与大语言模型进行最优交互，并学会评估大语言模型。</mark>

The first codelab will walk you through getting started with the Gemini 2.0 API and cover several prompt techniques including how different parameters impact the prompts. In the second codelab, you will also learn how to evaluate the response of LLMs using autoraters and structured output.

<mark>第一个代码实验会带你上手 Gemini 2.0 API，并介绍若干提示技巧，包括不同参数如何影响提示。在第二个代码实验里，你还将学习如何用自动评分器 (Autorater) 和结构化输出 (Structured Output) 来评估大语言模型的回答。</mark>

### Day 1 Assignments

<mark>第 1 天作业</mark>

1. Complete the Intro Unit – “Foundational Large Language Models & Text Generation”:

   <mark>完成导论单元——「基础大语言模型与文本生成」：</mark>

   - Listen to the [summary podcast episode](https://www.youtube.com/watch?v=Na3O4Pkbp-U&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE) for this unit.

     <mark>收听本单元的[摘要播客](https://www.youtube.com/watch?v=Na3O4Pkbp-U&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE)。</mark>

   - To complement the podcast, read the [“Foundational Large Language Models & Text Generation” whitepaper](https://www.kaggle.com/whitepaper-foundational-llm-and-text-generation).

     <mark>作为播客的补充，阅读白皮书「[基础大语言模型与文本生成](https://www.kaggle.com/whitepaper-foundational-llm-and-text-generation)」。</mark>

2. Complete Unit 1 – “Prompt Engineering”:

   <mark>完成单元 1——「提示工程」：</mark>

   - Listen to the [summary podcast episode](https://www.youtube.com/watch?v=CFtX0ZyLSAY&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=2) for this unit.

     <mark>收听本单元的[摘要播客](https://www.youtube.com/watch?v=CFtX0ZyLSAY&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=2)。</mark>

   - To complement the podcast, read the [“Prompt Engineering” whitepaper](https://www.kaggle.com/whitepaper-prompt-engineering).

     <mark>作为播客的补充，阅读白皮书「[提示工程](https://www.kaggle.com/whitepaper-prompt-engineering)」。</mark>

   - Complete these codelabs on Kaggle:

     <mark>在 Kaggle 上完成这些代码实验：</mark>

     - [Prompting fundamentals](https://www.kaggle.com/code/markishere/day-1-prompting)

       <mark>[提示基础](https://www.kaggle.com/code/markishere/day-1-prompting)</mark>

     - [Evaluation and structured data](https://www.kaggle.com/code/markishere/day-1-evaluation-and-structured-output)

       <mark>[评估与结构化数据](https://www.kaggle.com/code/markishere/day-1-evaluation-and-structured-output)</mark>

   - Make sure you [phone verify](https://www.kaggle.com/settings) your account before starting, it's necessary for the codelabs.

     <mark>开始之前请务必对账号做[手机验证](https://www.kaggle.com/settings)，代码实验需要这一步。</mark>

   - Want to have an [interactive conversation](https://support.google.com/notebooklm/answer/15731776?hl=en&ref_topic=14272601&sjid=16012842710481496794-EU)? Try adding the whitepapers to [NotebookLM](https://notebooklm.google/).

     <mark>想进行一场[互动对话](https://support.google.com/notebooklm/answer/15731776?hl=en&ref_topic=14272601&sjid=16012842710481496794-EU)吗？试试把白皮书加到 [NotebookLM](https://notebooklm.google/)。</mark>

   - [Optional] [Read a case study](https://cloud.google.com/blog/products/ai-machine-learning/how-commerzbank-is-transforming-financial-advisory-workflows-with-gen-ai?e=48754805) to learn how a leading bank leveraged advanced prompt engineering and other contents discussed in assignments of day 1 to automate their financial advisory workflows, achieving significant productivity gains.

     <mark>［可选］[阅读一篇案例研究](https://cloud.google.com/blog/products/ai-machine-learning/how-commerzbank-is-transforming-financial-advisory-workflows-with-gen-ai?e=48754805)，了解一家领先的银行如何运用高级提示工程，以及第 1 天作业里讨论的其他内容，把金融顾问工作流自动化，并显著提升生产力。</mark>

   - [Optional] Watch the [YouTube livestream recording](https://www.youtube.com/watch?v=WpIfAeCIFc0&list=PLqFaTIg4myu-lbBTrUpoQQIzZZxvrOaP5&index=1). Paige Bailey will be joined by expert speakers from Google — Warren Barkley, Logan Kilpatrick, Kieran Milan, Anant Nawalgaria, Irina Sigler and Mat Velloso to discuss today's readings and code labs.

     <mark>［可选］观看 [YouTube 直播录像](https://www.youtube.com/watch?v=WpIfAeCIFc0&list=PLqFaTIg4myu-lbBTrUpoQQIzZZxvrOaP5&index=1)。Paige Bailey 将与来自 Google 的专家讲者 Warren Barkley、Logan Kilpatrick、Kieran Milan、Anant Nawalgaria、Irina Sigler 和 Mat Velloso 一起，讨论今天的阅读材料和代码实验。</mark>

---

## Day 2 (Embeddings and Vector Stores/Databases)

<mark>第 2 天（嵌入与向量存储 / 数据库）</mark>

Welcome to Day 2.

<mark>欢迎来到第 2 天。</mark>

Today you will learn about the conceptual underpinning of embeddings and vector databases and how they can be used to bring live or specialist data into your LLM application. You’ll also explore their geometrical powers for classifying and comparing textual data as well as how to evaluate embeddings.

<mark>今天你将学习嵌入和向量数据库的概念基础，以及如何用它们把实时数据或专业数据带进大语言模型应用。你还将探索它们在分类和比较文本数据上的几何能力，以及如何评估嵌入。</mark>

### Day 2 Assignments

<mark>第 2 天作业</mark>

Complete Unit 2: “Embeddings and Vector Stores/Databases”:

<mark>完成单元 2：「嵌入与向量存储 / 数据库」：</mark>

- Listen to the [summary podcast episode](https://www.youtube.com/watch?v=xCAVsst6WJ8&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=3) for this unit.

  <mark>收听本单元的[摘要播客](https://www.youtube.com/watch?v=xCAVsst6WJ8&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=3)。</mark>

- To complement the podcast, read the [“Embeddings and Vector Stores/Databases” whitepaper](https://kaggle.com/whitepaper-embeddings-and-vector-stores).

  <mark>作为播客的补充，阅读白皮书「[嵌入与向量存储 / 数据库](https://kaggle.com/whitepaper-embeddings-and-vector-stores)」。</mark>

- Complete these code labs on Kaggle:

  <mark>在 Kaggle 上完成这些代码实验：</mark>

  - [Build a RAG question-answering system over custom documents](https://www.kaggle.com/code/markishere/day-2-document-q-a-with-rag)

    <mark>[基于自定义文档构建检索增强生成 (Retrieval-Augmented Generation, RAG) 问答系统](https://www.kaggle.com/code/markishere/day-2-document-q-a-with-rag)</mark>

  - [Explore text similarity with embeddings](https://www.kaggle.com/code/markishere/day-2-embeddings-and-similarity-scores)

    <mark>[用嵌入探索文本相似度](https://www.kaggle.com/code/markishere/day-2-embeddings-and-similarity-scores)</mark>

  - [Build a neural classification network with Keras using embeddings](https://www.kaggle.com/code/markishere/day-2-classifying-embeddings-with-keras)

    <mark>[用嵌入和 Keras 构建神经网络分类器](https://www.kaggle.com/code/markishere/day-2-classifying-embeddings-with-keras)</mark>

- Want to have an [interactive conversation](https://support.google.com/notebooklm/answer/15731776?hl=en&ref_topic=14272601&sjid=16012842710481496794-EU)? Try adding the whitepapers to [NotebookLM](https://notebooklm.google/).

  <mark>想进行一场[互动对话](https://support.google.com/notebooklm/answer/15731776?hl=en&ref_topic=14272601&sjid=16012842710481496794-EU)吗？试试把白皮书加到 [NotebookLM](https://notebooklm.google/)。</mark>

- [Optional] Watch the [YouTube livestream recording](https://www.youtube.com/watch?v=AjpjCHdIINU&list=PLqFaTIg4myu-lbBTrUpoQQIzZZxvrOaP5&index=2). Paige Bailey will be joined by expert speakers from Google — Andre Araujo, Patricia Florissi, Alan Li, Anant Nawalgaria, Xiaoqi Ren, Chuck Sugnet, and Howard Zhou to discuss embeddings and vector stores/databases.

  <mark>［可选］观看 [YouTube 直播录像](https://www.youtube.com/watch?v=AjpjCHdIINU&list=PLqFaTIg4myu-lbBTrUpoQQIzZZxvrOaP5&index=2)。Paige Bailey 将与来自 Google 的专家讲者 Andre Araujo、Patricia Florissi、Alan Li、Anant Nawalgaria、Xiaoqi Ren、Chuck Sugnet 和 Howard Zhou 一起，讨论嵌入与向量存储 / 数据库。</mark>

---

## Day 3 (Generative Agents)

<mark>第 3 天（生成式智能体）</mark>

Welcome to Day 3.

<mark>欢迎来到第 3 天。</mark>

Today you’ll learn to build sophisticated AI agents by understanding their core components and the iterative development process. You'll also learn more about advanced agentic architectures and approaches such as multi-agent systems, agent evaluation and more.

<mark>今天你将通过理解核心组件和迭代式开发过程，学习构建精密的 AI 智能体。你还将进一步了解高级的智能体式架构与方法，例如多智能体系统 (Multi-agent System)、智能体评估 (Agent Evaluation) 等。</mark>

The codelabs cover how to connect LLMs to existing systems and to the real world. Learn about function calling by giving SQL tools to a chatbot (including an example using Gemini 2.0’s [Live API](https://ai.google.dev/gemini-api/docs/live)), and learn how to build a LangGraph agent that takes orders in a café.

<mark>这些代码实验讲的是如何把大语言模型接到现有系统和真实世界。你将通过给聊天机器人配备 SQL 工具来学习函数调用 (Function Calling)，其中包含一个使用 Gemini 2.0 [Live API](https://ai.google.dev/gemini-api/docs/live) 的例子；你还将学习如何用 LangGraph 构建一个在咖啡馆接受点单的智能体。</mark>

### Day 3 Assignments

<mark>第 3 天作业</mark>

Complete Unit 3a — “Generative AI Agents”:

<mark>完成单元 3a——「生成式 AI 智能体」：</mark>

- Listen to the [summary podcast episode](https://www.youtube.com/watch?v=D3Kaqz7VW28&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=4) for this unit.

  <mark>收听本单元的[摘要播客](https://www.youtube.com/watch?v=D3Kaqz7VW28&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=4)。</mark>

- To complement the podcast, read the [“Generative AI Agents” whitepaper](https://www.kaggle.com/whitepaper-agents).

  <mark>作为播客的补充，阅读白皮书「[生成式 AI 智能体](https://www.kaggle.com/whitepaper-agents)」。</mark>

- Complete these code labs on Kaggle:

  <mark>在 Kaggle 上完成这些代码实验：</mark>

  - [Talk to a database with function calling](https://www.kaggle.com/code/markishere/day-3-function-calling-with-the-gemini-api)

    <mark>[用函数调用与数据库对话](https://www.kaggle.com/code/markishere/day-3-function-calling-with-the-gemini-api)</mark>

  - [Build an agentic ordering system in LangGraph](https://www.kaggle.com/code/markishere/day-3-building-an-agent-with-langgraph/)

    <mark>[用 LangGraph 构建智能体点单系统](https://www.kaggle.com/code/markishere/day-3-building-an-agent-with-langgraph/)</mark>

[Optional] Advanced 3b — “Agents Companion”:

<mark>［可选］进阶 3b——「智能体伴读 (Agents Companion)」：</mark>

- Listen to the [summary podcast episode](https://www.youtube.com/watch?v=7rbSwt-7odQ&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=5) for this unit.

  <mark>收听本单元的[摘要播客](https://www.youtube.com/watch?v=7rbSwt-7odQ&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=5)。</mark>

- Read the advanced [“Agents Companion” whitepaper](https://www.kaggle.com/whitepaper-agent-companion).

  <mark>阅读进阶白皮书「[智能体伴读](https://www.kaggle.com/whitepaper-agent-companion)」。</mark>

- Want to have an [interactive conversation](https://support.google.com/notebooklm/answer/15731776?hl=en&ref_topic=14272601&sjid=16012842710481496794-EU)? Try adding the whitepapers to [NotebookLM](https://notebooklm.google/).

  <mark>想进行一场[互动对话](https://support.google.com/notebooklm/answer/15731776?hl=en&ref_topic=14272601&sjid=16012842710481496794-EU)吗？试试把白皮书加到 [NotebookLM](https://notebooklm.google/)。</mark>

- [Optional] [Read a case study](https://cloud.google.com/blog/products/ai-machine-learning/regnology-automates-ticket-to-code-with-genai-on-vertex-ai?e=48754805) which talks about how a leading technology regulatory reporting solutions provider used an agentic generative AI system to automate ticket-to-code creation in software development, achieving a 2.5x productivity boost.

  <mark>［可选］[阅读一篇案例研究](https://cloud.google.com/blog/products/ai-machine-learning/regnology-automates-ticket-to-code-with-genai-on-vertex-ai?e=48754805)。文中介绍一家领先的科技监管报告解决方案提供商，如何用智能体式生成式 AI 系统，把软件开发里的「从工单到代码 (ticket-to-code)」自动化，并使生产力提升 2.5 倍。</mark>

- [Optional] Watch the [YouTube livestream recording](https://www.youtube.com/watch?v=g6MVIEzFTjY&list=PLqFaTIg4myu-lbBTrUpoQQIzZZxvrOaP5&index=3). Paige Bailey will be joined by expert speakers from Google — Alan Blount, Antonio Gulli, Steven Johnson, Jaclyn Konzelmann, Patrick Marlow, Anant Nawalgaria and Julia Wiesinger to discuss generative AI agents.

  <mark>［可选］观看 [YouTube 直播录像](https://www.youtube.com/watch?v=g6MVIEzFTjY&list=PLqFaTIg4myu-lbBTrUpoQQIzZZxvrOaP5&index=3)。Paige Bailey 将与来自 Google 的专家讲者 Alan Blount、Antonio Gulli、Steven Johnson、Jaclyn Konzelmann、Patrick Marlow、Anant Nawalgaria 和 Julia Wiesinger 一起，讨论生成式 AI 智能体。</mark>

---

## Day 4 (Domain-Specific LLMs)

<mark>第 4 天（领域专用大语言模型）</mark>

Welcome to Day 4.

<mark>欢迎来到第 4 天。</mark>

In today’s reading, you’ll delve into the creation and application of specialized LLMs like SecLM and MedLM/Med-PaLM, with insights from the researchers who built them.

<mark>在今天的阅读里，你将深入了解 SecLM、MedLM / Med-PaLM 这类专用大语言模型的构建与应用，并听取构建它们的研究人员的见解。</mark>

In the codelabs, you'll learn how to add real-world data to a model using Google Search and then visualize it with plotting tools via the Live API. You will also learn how to fine-tune a custom Gemini model using your own labeled data to solve custom tasks.

<mark>在代码实验里，你将学习如何用 Google 搜索为模型补充真实世界的数据，再通过 Live API 用绘图工具把它可视化。你还将学习如何用自己的标注数据，微调一个定制的 Gemini 模型，以解决自定义任务。</mark>

### Day 4 Assignments

<mark>第 4 天作业</mark>

Complete Unit 4 — “Domain-Specific LLMs”:

<mark>完成单元 4——「领域专用大语言模型」：</mark>

- Listen to the [summary podcast episode](https://www.youtube.com/watch?v=MWqspvVvNzA&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=6) for this unit.

  <mark>收听本单元的[摘要播客](https://www.youtube.com/watch?v=MWqspvVvNzA&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=6)。</mark>

- To complement the podcast, read the [“Solving Domain-Specific Problems Using LLMs” whitepaper](https://www.kaggle.com/whitepaper-solving-domains-specific-problems-using-llms).

  <mark>作为播客的补充，阅读白皮书「[用大语言模型解决领域专用问题](https://www.kaggle.com/whitepaper-solving-domains-specific-problems-using-llms)」。</mark>

- Complete these codelabs on Kaggle:

  <mark>在 Kaggle 上完成这些代码实验：</mark>

  - [Tune a Gemini model for a custom task](https://www.kaggle.com/code/markishere/day-4-fine-tuning-a-custom-model)

    <mark>[为自定义任务调优 Gemini 模型](https://www.kaggle.com/code/markishere/day-4-fine-tuning-a-custom-model)</mark>

  - [Use Google Search data in generation](https://www.kaggle.com/code/markishere/day-4-google-search-grounding)

    <mark>[在生成中使用 Google 搜索数据](https://www.kaggle.com/code/markishere/day-4-google-search-grounding)</mark>

- Want to have an [interactive conversation](https://support.google.com/notebooklm/answer/15731776?hl=en&ref_topic=14272601&sjid=16012842710481496794-EU)? Try adding the whitepapers to [NotebookLM](https://notebooklm.google/).

  <mark>想进行一场[互动对话](https://support.google.com/notebooklm/answer/15731776?hl=en&ref_topic=14272601&sjid=16012842710481496794-EU)吗？试试把白皮书加到 [NotebookLM](https://notebooklm.google/)。</mark>

- [Optional] Watch the [YouTube livestream recording](https://www.youtube.com/watch?v=AN2tpHi26OE&list=PLqFaTIg4myu-lbBTrUpoQQIzZZxvrOaP5&index=4). Paige Bailey will be joined by expert speakers from Google — Donny Cheung, Scott Coull, Ewa Dominowska, Chris Grier, Anant Nawalgaria and Karthik Raman to discuss domain specific models.

  <mark>［可选］观看 [YouTube 直播录像](https://www.youtube.com/watch?v=AN2tpHi26OE&list=PLqFaTIg4myu-lbBTrUpoQQIzZZxvrOaP5&index=4)。Paige Bailey 将与来自 Google 的专家讲者 Donny Cheung、Scott Coull、Ewa Dominowska、Chris Grier、Anant Nawalgaria 和 Karthik Raman 一起，讨论领域专用模型。</mark>

---

## Day 5 (MLOps for Generative AI)

<mark>第 5 天（面向生成式 AI 的机器学习运维）</mark>

Welcome to Day 5.

<mark>欢迎来到第 5 天。</mark>

Discover how to adapt MLOps practices for Generative AI and leverage Vertex AI's tools for foundation models and generative AI applications such as AgentOps for agentic applications.

<mark>了解如何把机器学习运维实践改造用于生成式 AI，并利用 Vertex AI 面向基础模型和生成式 AI 应用的工具，例如面向智能体式应用的智能体运维 (AgentOps)。</mark>

### Day 5 Assignments

<mark>第 5 天作业</mark>

Complete Unit 5 — “MLOps for Generative AI”:

<mark>完成单元 5——「面向生成式 AI 的机器学习运维」：</mark>

- Listen to the [summary podcast episode](https://www.youtube.com/watch?v=Hbk8UXavHrk&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=7) for this unit.

  <mark>收听本单元的[摘要播客](https://www.youtube.com/watch?v=Hbk8UXavHrk&list=PLqFaTIg4myu_yKJpvF8WE2JfaG5kGuvoE&index=7)。</mark>

- To complement the podcast, read the [“MLOps for Generative AI” whitepaper](https://www.kaggle.com/whitepaper-operationalizing-generative-ai-on-vertex-ai-using-mlops).

  <mark>作为播客的补充，阅读白皮书「[面向生成式 AI 的机器学习运维](https://www.kaggle.com/whitepaper-operationalizing-generative-ai-on-vertex-ai-using-mlops)」。</mark>

- No codelab for today! During the livestream tomorrow, we will do a code walkthrough and live demo of [goo.gle/agent-starter-pack](https://goo.gle/e2e-gen-ai-app-starter-pack), a resource created for making MLOps for Gen AI easier and accelerating the path to production. Please go through the repository in advance.

  <mark>今天没有代码实验！在明天的直播里，我们会做代码走读，并现场演示 [goo.gle/agent-starter-pack](https://goo.gle/e2e-gen-ai-app-starter-pack)。这套资料是为了让面向生成式 AI 的机器学习运维更容易，并加快走向生产的路径。请提前浏览这个仓库。</mark>

- Want to have an [interactive conversation](https://support.google.com/notebooklm/answer/15731776?hl=en&ref_topic=14272601&sjid=16012842710481496794-EU)? Try adding the whitepapers to [NotebookLM](https://notebooklm.google/).

  <mark>想进行一场[互动对话](https://support.google.com/notebooklm/answer/15731776?hl=en&ref_topic=14272601&sjid=16012842710481496794-EU)吗？试试把白皮书加到 [NotebookLM](https://notebooklm.google/)。</mark>

- [Optional] Watch the [YouTube livestream recording](https://www.youtube.com/watch?v=eZ-8UQ_t4YM&list=PLqFaTIg4myu-lbBTrUpoQQIzZZxvrOaP5&index=5). Paige Bailey will be joined by expert speakers from Google — Sokratis Kartakis, Gabriela Hernandez Larios, Ivan Nardini, Anant Nawalgaria, Elia Secchi, Michael Styer and Saurabh Tiwary to discuss MLOps practices for generative AI.

  <mark>［可选］观看 [YouTube 直播录像](https://www.youtube.com/watch?v=eZ-8UQ_t4YM&list=PLqFaTIg4myu-lbBTrUpoQQIzZZxvrOaP5&index=5)。Paige Bailey 将与来自 Google 的专家讲者 Sokratis Kartakis、Gabriela Hernandez Larios、Ivan Nardini、Anant Nawalgaria、Elia Secchi、Michael Styer 和 Saurabh Tiwary 一起，讨论面向生成式 AI 的机器学习运维实践。</mark>

---

## Bonus Assignment

<mark>加分作业</mark>

Check out this [bonus assignment](https://www.kaggle.com/code/markishere/bonus-day-extra-api-features-to-try/): There’s more! This [bonus notebook](https://www.kaggle.com/code/markishere/bonus-day-extra-api-features-to-try/) walks you through a few more things you can do with the Gemini API that weren't covered during the course. This material doesn't pair with the whitepapers or podcast, but covers some extra capabilities you might find useful when building Gemini API powered apps.

<mark>看看这份[加分作业](https://www.kaggle.com/code/markishere/bonus-day-extra-api-features-to-try/)：还有更多内容！这份[加分 Notebook](https://www.kaggle.com/code/markishere/bonus-day-extra-api-features-to-try/)会带你试用课程里没讲到的若干 Gemini API 能力。这些材料不配白皮书或播客，但覆盖了一些额外能力，在构建由 Gemini API 驱动的应用时可能会用到。</mark>

---

## Congratulations on completing the GenAI Intensive Learn Guide!

<mark>恭喜你完成「生成式 AI 强化」学习指南！</mark>

Now that you’ve mastered the fundamentals, take the next step and dive into the [AI Agents Intensive Learn Guide](https://www.kaggle.com/learn-guide/5-day-agents) to develop a deeper, more hands-on understanding of AI agents.

<mark>现在你已经掌握了这些基础，下一步可以进入「[AI 智能体强化](https://www.kaggle.com/learn-guide/5-day-agents)」学习指南，对 AI 智能体建立更深入、更动手的理解。</mark>

## Happy Kaggling!

<mark>祝你在 Kaggle 上学习愉快！</mark>

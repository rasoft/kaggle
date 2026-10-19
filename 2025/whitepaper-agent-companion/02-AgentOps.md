# AgentOps

<mark>智能体运维 (AgentOps)</mark>

Over the past two years, the field of Generative AI (GenAI) has undergone significant changes, with enterprise customers focusing on how to operationalize related solutions. This has resulted in various terms describing the operationalization of GenAI, such as MLOps for GenAI, LLMOps, FMOps, and GenAIOps.

<mark>过去两年，生成式 AI (Generative AI, GenAI) 领域变化很大，企业客户关注的是如何把相关方案运维起来。于是出现了各种描述生成式 AI 运维化的说法，例如面向 GenAI 的 MLOps、LLMOps、FMOps 和 GenAIOps。</mark>

Agent and Operations (AgentOps) is a subcategory of GenAIOps that focuses on the efficient operationalization of Agents. Its main additional components include internal and external tool management, agent brain prompt (goal, profile, instructions) and orchestration, memory, and task decomposition.

<mark>智能体与运维 (Agent and Operations, AgentOps) 是 GenAIOps 的一个子类，专注于高效地把智能体运维起来。它额外的主要组件包括：内部与外部工具管理、智能体大脑提示（目标、画像、指令）与编排 (Orchestration)、记忆，以及任务分解。</mark>

![Relationship between DevOps, MLOps, and AgentOps](image_004_page_09.png)

<mark>[图 1：DevOps、MLOps 与 AgentOps 的关系<sup>13</sup>。DevOps 在顶层。模型开发一侧，MLOps 继承 DevOps，FMOps 再继承 MLOps；LLMOps 是 FMOps 的子类。应用开发一侧，GenAIOps 继承 DevOps，其下有 PromptOps、AgentOps、RAGOps 三个子类，PromptOps 是 AgentOps 与 RAGOps 的前提。生产者、微调者和消费者围绕中心节点：微调者创建并使用模型，消费者使用 GenAIOps。]</mark>

---

Each of these “Ops” requires capabilities like version control, automated deployments through CI/CD, testing, logging, security and (critically) metrics. Each system often implements some form of optimization based on metrics – measuring what your system is and isn’t doing, measuring the outcomes and business metrics, and automating the processes for more holistic metrics, and incrementally improving step by step. This practice might be called “A/B experimentation” or “ML Ops” or “Metrics Driven development", but they derive from the same general approach and we will rely on those principles for AgentOps as well.

<mark>这些「Ops」都需要版本控制、通过 CI/CD 自动部署、测试、日志、安全，以及（关键的）指标。每个系统通常都会基于指标做某种优化：度量系统在做什么、没做什么，度量结果和业务指标，把流程自动化以得到更完整的指标，再一步步改进。这种做法可能叫「A/B 实验」，或「ML Ops」，或「指标驱动开发」，但它们出自同一种一般方法。AgentOps 也会依靠这些原则。</mark>

Remember that new practices don't replace the old. DevOps and MLOps best practices are still necessary for AgentOps, as they are dependencies. For example, Agent tool use, where APIs are invoked based on agent orchestration, often uses the same APIs you would invoke with non-agentic software. Authentication and secret management, security, privacy, exception handling, throttling, quotas, and scalability are still critical and require careful API design in addition to Agent design.

<mark>要记住，新实践不会取代旧实践。DevOps 和 MLOps 的最佳实践对 AgentOps 仍然必要，因为它们是依赖项。例如，智能体的工具使用 (Tool Use) 是按智能体编排去调用 API，用的往往就是非智能体软件也会调用的那些 API。认证与密钥管理、安全、隐私、异常处理、限流、配额和可扩展性依然关键，除了智能体设计，还需要仔细的 API 设计。</mark>

Let’s go ahead and define these “ops” terms to help distinguish between them:

<mark>下面把这些「ops」术语定义清楚，便于区分：</mark>

- **Development and Operations (DevOps)** is the practice of efficiently productionizing deterministic software applications by integrating the elements of people, processes, and technology. DevOps serves as the foundation for all the following terms.

<mark>- **开发与运维 (Development and Operations, DevOps)** 是把人、流程和技术整合起来，高效地把确定性软件应用生产化的实践。DevOps 是下面所有术语的基础。</mark>

- **Machine Learning Operations (MLOps)** builds upon the capabilities of DevOps and concentrates on the efficient productionization of ML models. The primary distinction is that the output of an ML model is non-deterministic and relies on the input data (garbage in, garbage out).

<mark>- **机器学习运维 (Machine Learning Operations, MLOps)** 建立在 DevOps 的能力之上，专注于高效地把机器学习模型生产化。主要区别是：ML 模型的输出是非确定性的，并且依赖输入数据（垃圾进，垃圾出）。</mark>

- **Foundation Model Operations (FMOps)** expands upon the capabilities of MLOps and focuses on the efficient productionization of pre-trained (trained from scratch) or customized (fine-tuned) FMs.

<mark>- **基础模型运维 (Foundation Model Operations, FMOps)** 扩展了 MLOps 的能力，专注于高效地把预训练（从零训练）或定制（微调）的基础模型 (FM) 生产化。</mark>

- **Prompt and Operations (PromptOps)** is a subcategory of GenAIOps that focuses on operationalizing prompts effectively. Its main additional capabilities include prompt storage, lineage, metadata management (including evaluation scores), a centralized prompt template registry, and a prompt optimizer.

<mark>- **提示与运维 (Prompt and Operations, PromptOps)** 是 GenAIOps 的一个子类，专注于有效地把提示运维起来。它额外的主要能力包括：提示存储、血缘、元数据管理（含评估分数）、集中的提示模板注册表，以及提示优化器。</mark>

- **RAG and Operations (RAGOps)** is a subcategory of GenAIOps that centers on efficiently operationalizing RAG solutions. Its primary additional capabilities include the retrieval process through offline data preparation (encompassing cleaning, chunking, vectorization, similarity search, and re-ranking) and the generation process through prompt augmentation and grounding.

<mark>- **RAG 与运维 (RAG and Operations, RAGOps)** 是 GenAIOps 的一个子类，核心是高效地把检索增强生成 (RAG) 方案运维起来。它额外的主要能力包括：通过离线数据准备完成检索过程（涵盖清洗、分块、向量化、相似度搜索和重排序），以及通过提示增强和依据锚定 (grounding) 完成生成过程。</mark>

- **Agent and Operations (AgentOps)** is a subcategory of GenAIOps that focuses on the efficient operationalization of Agents. Its main additional components include internal and external tool management, agent brain prompt (goal, profile, instructions) and orchestration, memory, and task decomposition.

<mark>- **智能体与运维 (AgentOps)** 是 GenAIOps 的一个子类，专注于高效地把智能体运维起来。它额外的主要组件包括：内部与外部工具管理、智能体大脑提示（目标、画像、指令）与编排、记忆，以及任务分解。</mark>

![Each of these Ops is about technology, processes, and people](image_005_page_11.png)

<mark>[图 2：这些「Ops」都关乎技术、流程和人<sup>14</sup>。三圆相交：人 (People)、技术 (Technology)、流程 (Processes)。说明文字：Ops，即机器学习与运维，是人、流程与技术的组合，用来高效地把 ML 方案生产化。星标落在三者交汇处。]</mark>

---

All of these “Ops” are, in essence, the harmonious blend of people, processes, and technologies working together to efficiently deploy machine learning solutions into a live production environment. It’s crucial to recognize that Ops extends beyond mere technology; it’s not simply about constructing and delivering a ML pipeline. Successful Ops implementations delve deeper, considering the customer’s operational model, their existing business units, and their overall organizational structure. This holistic approach ensures that the technology is tailored to their specific needs, seamlessly integrating into the business and maximizing value.

<mark>所有这些「Ops」，本质上都是人、流程和技术和谐地合在一起，把机器学习方案高效地部署到真实生产环境。必须认识到，Ops 超出了单纯的技术：它不只是搭建并交付一条 ML 流水线。成功的 Ops 落地会看得更深，会考虑客户的运营模式、现有业务单元，以及整体组织结构。这种整体方法保证技术按他们的具体需要来裁剪，无缝融入业务，并尽量放大价值。</mark>

---

## Agent Success Metrics

<mark>智能体成功指标</mark>

The next section will cover Agent Evaluation in detail, which is a significant part of the story for AgentOps and automation to capture useful metrics. Before we go there, let’s start with a thought experiment; imagine setting up an A/B experiment in production for your new Agent. The treatment arm gets your new agent and the control arm does not. In that scenario, what metrics are you measuring to determine if the treatment arm is doing better? What metrics are you measuring to determine ROI for the project? Is it a goal being accomplished, or sales totals, or a set of critical steps in a user journey? Those metrics must be understood, instrumented and easily analyzed in addition to more detailed Agent Evaluation metrics.

<mark>下一节会详细讲智能体评估。对 AgentOps 和用来采集有用指标的自动化来说，这是故事里很重要的一部分。在那之前，先做一个思想实验：想象你为新智能体在生产环境里做一次 A/B 实验。实验组用上新智能体，对照组不用。在这个场景里，你用哪些指标判断实验组是否更好？你用哪些指标判断项目的投资回报 (ROI)？是目标达成了，还是销售总额，还是用户旅程里的一组关键步骤？这些指标必须被理解、被埋点，并且容易分析，这是在更细的智能体评估指标之外还要做的事。</mark>

Metrics are critical to building, monitoring, and comparing revisions of Agents. Business metrics, like revenue or user engagement, are probably outside of the scope of the agent itself but these should be the north star metric for your agents.

<mark>指标对构建、监控和比较智能体的各个修订版都至关重要。收入或用户参与度这类业务指标，大概不在智能体自身的范围内，但它们应当是智能体的北极星指标。</mark>

Most Agents are designed around accomplishing goals, so goal completion rate is a key metric to track. Similarly, a goal might be broken down into a few critical tasks or critical user interactions. Each of these critical tasks and interactions should be independently instrumented and measured.

<mark>大多数智能体是围绕达成目标来设计的，所以目标完成率是要跟踪的关键指标。同样，一个目标可以拆成若干关键任务或关键用户交互。这些关键任务和交互都应当单独埋点、单独度量。</mark>

So before we get into the details of the Agent itself, we already have several metrics identified which you should be able to easily track on a dashboard. Each business metric, goal, or critical interaction, will be aggregated in a familiar fashion: attempts, successes, rates, etc. Additionally, metrics you should be able to get from any application telemetry system are very important to track for agents as well, metrics like latency, errors, etc.

<mark>所以在进入智能体本身的细节之前，我们已经识别出若干指标，你应当能在仪表板上轻松跟踪。每项业务指标、目标或关键交互，都会按熟悉的方式汇总：尝试次数、成功次数、比率等。另外，任何应用遥测系统都能拿到的指标，对智能体同样非常重要，例如延迟、错误等。</mark>

None of these metrics are specific to Agents, you could track them for any software, but they are even more important for Agent builders. Deterministic code does only what you tell it to do, whereas an agent can do a lot more, relying on LLMs which are trained on huge amounts of data. Instrumentation of these high level metrics is an important part of observability. You can think of them as Key Performance Indicators (KPI) for the agent, and they allow for observability in the aggregate, a higher level perspective of your agents.

<mark>这些指标没有一个是智能体专有的，任何软件都可以跟踪，但对智能体构建者来说它们更加重要。确定性代码只做你让它做的事，而智能体可以做得多得多，它依赖在海量数据上训练的大语言模型 (LLM)。给这些高层指标埋点，是可观测性的重要部分。可以把它们看成智能体的关键绩效指标 (Key Performance Indicator, KPI)，它们提供汇总层面的可观测性，也就是对智能体更高一层的视角。</mark>

Human feedback is one of the more critical metrics to track as well. A simple 👍👎 or user feedback form, within the context of an agent or task can go a long way to understanding where your agent does well and where it needs improvement. This feedback can come from end users of a consumer system, but also employees, QA testers, and process or domain experts reviewing the agent.

<mark>人类反馈也是更关键、需要跟踪的指标之一。在某个智能体或某项任务的上下文里，一个简单的 👍👎 或用户反馈表，就很有助于弄清智能体哪里做得好、哪里需要改进。这类反馈可以来自消费级系统的最终用户，也可以来自员工、QA 测试人员，以及审阅智能体的流程专家或领域专家。</mark>

More detailed observability is also very important for agent building, being able to see and understand what the agent is doing and why it’s doing that. An agent can be instrumented with “trace” to log all of the inner workings of the agent, not only the critically important tasks and user interactions. You could conceptually measure every internal step as metrics, but that is rarely done. Instead these detailed traces are used to debug an agent when metrics or manual testing show a problem, you can dig into details and see what went wrong.

<mark>更细的可观测性对构建智能体同样非常重要：要能看见并理解智能体在做什么、为什么这样做。可以为智能体埋上「追踪 (trace)」，记录它全部的内部运作，而不只是那些至关重要的任务和用户交互。原则上可以把每一步内部步骤都当成指标来度量，但很少这样做。这些详细追踪是在指标或人工测试显示出问题时用来调试智能体的：你可以钻进细节，看看出了什么错。</mark>

![Cloud Observability traces for an agent with tools and LLM spans](image_006_page_14.png)

<mark>[图 3：Cloud Observability 中带工具和 LLM 的 OpenTelemetry 跨度的智能体追踪示例<sup>15</sup>。左侧是一段关于创建 SQLite 天气数据表的对话。右侧是一次追踪：chain invoke 之下有 GET、ALTER、CREATE、DROP 等工具调用，以及 gemini-1.5-flash 的 GenAI 跨度，并展示工具消息、模型选择和 token 计数。]</mark>

---

So far we’ve been talking about business metrics, goals, tasks, human feedback, and traces – those are all ways of understanding the actions and impact of your agents, in production. While developing an agent, in addition to manual testing, automated testing will be much more efficient in the long run and provide greater insights into the behavior of agents.

<mark>到目前为止，我们谈的是业务指标、目标、任务、人类反馈和追踪。它们都是在生产中理解智能体行动与影响的方式。在开发智能体时，除了人工测试，长期来看自动化测试会高效得多，也能对智能体行为提供更深的洞察。</mark>

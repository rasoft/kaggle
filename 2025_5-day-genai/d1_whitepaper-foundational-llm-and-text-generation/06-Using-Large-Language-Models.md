# Using large language models

使用大语言模型

Prompt engineering and sampling techniques have a strong influence on the performance of LLMs. Prompt engineering is the process of designing and refining the text inputs (prompts) that you feed into an LLM to achieve desired and relevant outputs. Sampling techniques determine the way in which output tokens are chosen and influence the correctness, creativity and diversity of the resulting output. We next discuss different variants of prompt engineering and sampling techniques as well as touch on some important parameters that can have a significant impact on LLM performance.

提示工程 (Prompt Engineering) 和采样 (Sampling) 技术对大语言模型 (LLM) 的性能有很强的影响。提示工程是设计和打磨你送入大语言模型的文本输入（提示，Prompt）的过程，以得到期望且相关的输出。采样技术决定输出词元 (token) 如何被选中，并影响所得输出的正确性、创造性和多样性。接下来我们讨论提示工程和采样技术的不同变体，并触及一些能显著影响大语言模型性能的重要参数。

---

## Prompt engineering

提示工程

LLMs are very powerful, but they still need guidance to unleash their full potential. Prompt engineering is a critical component in guiding an LLM to yield desired outputs. This might include grounding the model to yield factual responses or unleashing the creativity of the model to tell a story or write a song. Examples of prompt engineering include providing clear instructions to the LLM, giving examples, using keywords, and formatting to emphasize important information, providing additional background details etc.

大语言模型很强，但它们仍然需要引导，才能释放全部潜力。提示工程是引导大语言模型给出期望输出的关键组成部分。这可能包括把模型 (Model) 锚定到事实上以给出符合事实的回答，或释放模型的创造性来讲一个故事或写一首歌。提示工程的例子包括：给大语言模型清晰的指令、给出例子、用关键词和格式来强调重要信息、提供额外的背景细节等。

You will often hear the terms zero-shot, few-shot, and chain-of-thought prompting in the context of prompt engineering. We define these terms below:

在提示工程的语境里，你常会听到零样本、少样本和思维链提示这些术语。我们在下面定义它们：

- Few-shot prompting: This is when you provide the LLM with a task description, as well as a few (e.g. three to five) carefully chosen examples, that will help guide the LLM’s response. For example, you might provide the model with the name of a few countries and their capital cities, then ask it to generate the capital for a new country that isn’t in the examples.

- 少样本 (few-shot) 提示：这时你给大语言模型任务描述，以及几个（例如三到五个）仔细挑选的例子，用来引导大语言模型的回答。例如，你可以给模型几个国家的名字和它们的首都，然后请它为例子里没有的一个新国家生成首都。

- Zero-shot prompting: This is when you provide the LLM directly with a prompt with instructions. You usually give the LLM a task description and the LLM relies heavily on its existing knowledge to output the correct response. This requires no additional data or examples, hence the name ‘Zero-shot’ but can be less reliable than few-shot prompting.

- 零样本 (zero-shot) 提示：这时你直接给大语言模型一条带指令的提示。你通常给大语言模型任务描述，大语言模型在很大程度上依靠已有知识来输出正确回答。这不需要额外的数据或例子，因而得名「零样本」，但可能不如少样本提示可靠。

- Chain-of-thought prompting: This technique aims to improve performance on complex reasoning tasks. Rather than simply asking the LLM a question, you provide a prompt that demonstrates how to solve similar problems using step-by-step reasoning. The LLM then generates its own chain of thought for the new problem, breaking it down into smaller steps and explaining its reasoning. Finally, it provides an answer based on its reasoning process.

- 思维链 (chain-of-thought) 提示：这项技术旨在提高复杂推理 (Reasoning) 任务上的性能。你不是简单地问大语言模型一个问题，而是提供一条提示，演示如何用逐步推理来解决类似问题。大语言模型随后为新问题生成自己的思维链，把它拆成更小的步骤并解释自己的推理。最后，它根据自己的推理过程给出答案。

Prompt engineering is an active area of research.

提示工程是一个活跃的研究领域。

---

## Sampling Techniques and Parameters

采样技术与参数

A variety of sampling techniques can be employed to determine how the model chooses the next token in a sequence. They are essential for controlling the quality, creativity, and diversity of the LLM’s output. The following is a breakdown of different sampling techniques and their important parameters:

可以用多种采样技术来决定模型如何选择序列中的下一个词元。它们对控制大语言模型输出的质量、创造性和多样性至关重要。下面拆开不同的采样技术及其重要参数：

- Greedy search<sup>50</sup>: Selects the token with the highest probability at each step. This is the simplest option but it can lead to repetitive and predictable outputs.

- 贪心搜索<sup>50</sup>：每一步选择概率最高的词元。这是最简单的选项，但可能导致重复、可预测的输出。

- Random sampling:<sup>50</sup> Selects the next token according to the probability distribution, where each token is sampled proportionally to its predicted probability. This can produce more surprising and creative text, but also a higher chance of nonsensical output.

- 随机采样：<sup>50</sup> 按概率分布选择下一个词元，每个词元按其预测概率成比例地被采样。这可以产生更出人意料、更有创造性的文本，但出现无意义输出的机会也更高。

- Temperature sampling:<sup>50</sup> Adjusts the probability distribution by a temperature parameter. Higher temperatures promote diversity, lower temperatures favor high-probability tokens.

- 温度采样：<sup>50</sup> 用温度 (temperature) 参数调整概率分布。更高的温度促进多样性，更低的温度偏向高概率词元。

- Top-K sampling: Randomly samples from the top K most probable tokens. The value of K controls the degree of randomness.

- Top-K 采样：从概率最高的 K 个词元中随机采样。K 的值控制随机程度。

- Top-P sampling (nucleus sampling):<sup>51</sup> Samples from a dynamic subset of tokens whose cumulative probability adds up to P. This allows the model to adapt the number of potential candidates depending on its confidence, favoring more diversity when uncertain and focusing on a smaller set of highly probable words when confident.

- Top-P 采样（核采样）：<sup>51</sup> 从一个动态的词元子集中采样，这些词元的累积概率加起来达到 P。这使模型能按其置信度调整潜在候选的数量：不确定时偏向更多多样性，有信心时聚焦于一组更小的高概率词。

- Best-of-N sampling: Generates N separate responses and selects the one deemed best according to a predetermined metric (e.g., a reward model or a logical consistency check). This is particularly useful for short snippets or situations where logic and reasoning are key.

- Best-of-N 采样：生成 N 个分开的回答，并按预定指标（例如奖励模型或逻辑一致性检查）选出被认为最好的一个。这对短片段，或逻辑与推理是关键的情形，特别有用。

By combining prompt engineering with sampling techniques and correctly calibrated hyperparameters, you can greatly influence the LLM’s response, making it more relevant, creative, and consistent for your specific needs.

把提示工程与采样技术以及校准正确的超参数结合起来，你可以大大影响大语言模型的回答，使它更贴合你的具体需要，也更有创造性、更一致。

Until now, we have seen the various types of LLM architectures, their underlying technology, as well as the approaches used to train, tune, and adapt these models for various tasks. Let’s now look at some key research about how the decoding process in LLMs can be sped up considerably to generate faster responses.

到目前为止，我们看到了各种类型的大语言模型架构、它们背后的技术，以及用来训练、调优并使这些模型适应各种任务的方法。现在来看一些关键研究：大语言模型中的解码过程如何能大幅加速，以更快地生成回答。

---

## Task-based Evaluation

面向任务的评估

The emergence of LLMs has reduced the obstacles to building AI applications, but moving from MVP to production introduces challenges such as prompt engineering, model selection, and performance monitoring. A tailored evaluation framework is essential for navigating LLM application development by validating functionality and user experience, identifying potential issues, facilitating communication about capabilities, and establishing a roadmap for improvement. For building a tailored evaluation framework, application builders need to provide their own evaluation data, development context, a definition of good performance.

大语言模型的出现降低了构建 AI 应用的障碍，但从最小可行产品走向生产会带来提示工程、模型选择和性能监控等挑战。一套量身定做的评估 (Evaluation) 框架，对驾驭大语言模型应用开发至关重要：它验证功能与用户体验，识别潜在问题，促进关于能力的沟通，并建立改进路线图。要构建这样一套框架，应用构建者需要提供自己的评估数据、开发上下文，以及对「好的性能」的定义。

- Evaluation data: Public leaderboards that showcase LLM capabilities often fall short for application developers who require a more tailored approach. A dedicated evaluation dataset that mirrors the expected production traffic as closely as possible is needed. During prototyping this can be a manually curated dataset, one that is continuously enriched with real user interactions, production logs, and synthetically generated data to test specific scenarios.

- 评估数据：展示大语言模型能力的公开排行榜，对需要更贴合做法的应用开发者往往不够。需要一份专门的评估数据集，尽可能贴近预期的生产流量。原型阶段，这可以是一份人工整理的数据集，并持续用真实用户交互、生产日志和为测试特定场景而合成的数据来充实。

- Development Context: The evaluation should extend beyond just the model’s output to analyze the entire system, including components like data augmentation (e.g., Retrieval Augmented Generation or RAG) and agentic workflows. This approach ensures understanding of how all components interact and contribute to the application’s overall performance.

- 开发上下文：评估应当超出模型的输出本身，去分析整个系统，包括数据增强（例如检索增强生成，Retrieval Augmented Generation，即 RAG）和智能体式工作流等组件。这种做法确保理解所有组件如何交互，并如何贡献于应用的整体性能。

- Definition of “Good”: Traditional metrics that prioritize matching a single “correct” answer can unfairly penalize unexpected solutions. When working with LLMs, we can address this by moving beyond similarity to ground truth as a definition of good, but rather establish dataset level criteria that reflect desired business outcomes or even rubrics that capture the core elements of the desired outputs depending on the input user instructions.

- 「好」的定义：优先匹配单一「正确」答案的传统指标，可能不公平地惩罚出人意料的解。与大语言模型共事时，我们可以不把与真值的相似度当作「好」的定义，而是建立数据集层面的标准，反映期望的业务结果，甚至建立量规，按输入的用户指令捕捉期望输出的核心要素。

Application builders can evaluate LLM performance using three methods:

应用构建者可以用三种方法评估大语言模型的性能：

- Traditional Evaluation Methods: Similar to evaluating predictive models, these methods use quantitative metrics to compare model outputs to ideal responses, aiming to offer objective insights. However, they may penalize creative or unexpected outputs, limiting their effectiveness for generative tasks that have multiple possible solutions.

- 传统评估方法：与评估预测模型相似，这些方法用定量指标把模型输出与理想回答比较，旨在提供客观的洞察。然而，它们可能惩罚有创造性或出人意料的输出，从而限制了它们对有多种可能解的生成任务的有效性。

- Human Evaluation: Considered the gold standard, human judgment provides nuanced assessment of complex generative outputs.

- 人类评估：被认为是金标准。人的判断为复杂的生成输出提供细致的评估。

- LLM-Powered Autoraters: LLM-powered autoraters try to mimic human judgment, offering scalable and efficient evaluations. Unlike computation-based methods, they can operate with or without reference data. A basic setup involves providing the task, criteria, and candidate responses (with optional references), which the autorater uses to generate and parse LLM output for final evaluation results. In addition to the final outputs, autoraters can provide rationales to explain a given decision to the user. While generative models are common autoraters, reward and discriminative models are also used. Crucially, like any measurement tool, autoraters require calibration. Meta-evaluation, i.e. comparing autorater outputs to human judgments, ensures the autorater aligns with desired preferences. This calibration typically involves agreement in terms of model preference or correlation measures, tailored to the evaluation task. In this meta-evaluation, it is important to keep in mind potential limitations of autorater models.<sup>69</sup>

- 由大语言模型驱动的自动评分器：自动评分器 (autorater) 试图模仿人的判断，提供可扩展且高效的评估。与基于计算的方法不同，它们可以有参考数据，也可以没有。基本设置是提供任务、标准和候选回答（参考答案可选），自动评分器用这些来生成并解析大语言模型的输出，得到最终评估结果。除最终输出外，自动评分器还可以提供理由，向用户解释某一次决定。生成模型是常见的自动评分器，奖励模型和判别模型也会用到。关键的是，像任何测量工具一样，自动评分器需要校准。元评估，也就是把自动评分器的输出与人的判断比较，确保自动评分器与期望的偏好对齐。这种校准通常涉及模型偏好上的一致性或相关度量，并按评估任务来调整。在这种元评估里，记住自动评分器模型的潜在局限很重要。<sup>69</sup>

While the basic setup described above focuses on providing autoraters with fixed criteria that can be used to evaluate an entire dataset of examples, approaches are emerging to leverage rubrics and multi-step processes in order to obtain interpretable evaluation metrics. At a high level, an LLM breaks an example down into multiple evaluation subtasks and then evaluates each subtask to give an interpretable, detailed report for this example. As the task has been broken down, domain-specialized models can be leveraged for specific tasks to improve reliability if necessary. Results are then aggregated for a given example to yield an overall score, or across related subtasks to evaluate how well a model performs along a particular axis. This setup is especially useful in media generation, where different examples may require vastly different skills (e.g. object generation vs text generation) and a single score obfuscates how relative strengths and weaknesses of different models contribute to the final result.

上面描述的基本设置，重点是给自动评分器固定的标准，用来评估整个例子数据集。正在出现的做法则利用量规和多步过程，以得到可解释的评估指标。从高层看，一个大语言模型把一个例子拆成多个评估子任务，再评估每个子任务，为这个例子给出一份可解释的详细报告。任务拆开之后，如有必要，可以针对特定任务使用领域专用模型来提高可靠性。然后把结果按给定例子聚合，得到一个总分，或跨相关子任务聚合，以评估模型沿某一轴表现如何。这种设置在媒体生成中特别有用：不同例子可能需要差别很大的技能（例如物体生成对文本生成），单一分数会掩盖不同模型的相对长短如何贡献于最终结果。

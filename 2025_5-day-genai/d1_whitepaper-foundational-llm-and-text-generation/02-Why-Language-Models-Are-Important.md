# Why language models are important

语言模型为什么重要

LLMs achieve an impressive performance boost from the previous state of the art NLP models across a variety of different and complex tasks which require answering questions or complex reasoning, making feasible many new applications. These include language translation, code generation and completion, text generation, text classification, and question-answering, to name a few. Although foundational LLMs trained in a variety of tasks on large amounts of data perform very well out of the box and display emergent behaviors (e.g. the ability to perform tasks they have not been directly trained for) they can also be adapted to solve specific tasks where performance out of the box is not at the level desired through a process known as fine-tuning. This requires significantly less data and computational resources than training an LLM from scratch. LLMs can be further nudged and guided towards the desired behavior by the discipline of prompt engineering: the art and science of composing the prompt and the parameters of an LLM to get the desired response.

在需要回答问题或做复杂推理 (Reasoning) 的许多不同且困难的任务上，大语言模型 (LLM) 相对此前的自然语言处理（NLP）前沿模型有很明显的性能提升，从而让许多新应用成为可能。其中包括语言翻译、代码生成与补全、文本生成、文本分类和问答，这里只举几例。基础大语言模型在大量数据上、面向多种任务训练之后，开箱就能表现得很好，并显示出涌现行为（例如完成并未直接训练过的任务）。当开箱表现还达不到期望时，也可以通过称为微调 (fine-tuning) 的过程，把它们改造成解决特定任务。这比从零训练一个大语言模型所需的数据和计算资源少得多。还可以用提示工程 (Prompt Engineering) 进一步推动并引导它们走向期望的行为：这是一门编排提示 (Prompt) 和大语言模型参数、以得到期望回答的技艺与科学。

The big question is: how do these large language models work? The next section explores the core building blocks of LLMs, focusing on transformer architectures and their evolution from the original ‘Attention is all you need’ paper<sup>1</sup> to the latest models such as Gemini, Google’s most capable LLM. We also cover training and fine-tuning techniques, as well as methods to improve the speed of response generation. The whitepaper concludes with a few examples of how language models are used in practice.

大问题是：这些大语言模型如何工作？下一节探索它们的核心构件，重点是 Transformer 架构，以及从最初的论文《Attention is all you need》<sup>1</sup> 到最新模型 (Model)（例如 Google 能力最强的大语言模型 Gemini）的演进。我们也会讲训练与微调技术，以及提高回答生成速度的方法。白皮书最后用几个例子说明语言模型在实践中如何使用。

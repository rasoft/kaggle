# Prompt engineering

<mark>提示工程 (Prompt Engineering)</mark>

When you chat with the Gemini chatbot,1 you basically write prompts, however this whitepaper focuses on writing prompts for the Gemini model within Vertex AI or by using the API, because by prompting the model directly you will have access to the configuration such as temperature etc.

<mark>和 Gemini 聊天机器人对话时，1 你写的基本上就是提示 (Prompt)。不过这份白皮书关注的是在 Vertex AI 里、或通过 API，给 Gemini 模型 (Model) 写提示。直接向模型发提示，你才能用到温度 (temperature) 等配置。</mark>

This whitepaper discusses prompt engineering in detail. We will look into the various prompting techniques to help you getting started and share tips and best practices to become a prompting expert. We will also discuss some of the challenges you can face while crafting prompts.

<mark>这份白皮书详细讨论提示工程。我们会看各种提示技巧，帮你上手，并分享成为提示专家的窍门和最佳实践。我们也会讨论撰写提示时可能遇到的一些困难。</mark>

Remember how an LLM works; it’s a prediction engine. The model takes sequential text as an input and then predicts what the following token should be, based on the data it was trained on. The LLM is operationalized to do this over and over again, adding the previously predicted token to the end of the sequential text for predicting the following token. The next token prediction is based on the relationship between what’s in the previous tokens and what the LLM has seen during its training.

<mark>回想大语言模型 (LLM) 是怎么工作的：它是一台预测引擎。模型把一段顺序文本当作输入，再根据训练数据预测下一个词元 (token) 应该是什么。大语言模型被做成反复做这件事：把刚预测出的词元接到顺序文本末尾，再预测再下一个词元。下一个词元的预测，取决于前面那些词元里有什么，以及大语言模型在训练中见过什么。</mark>

When you write a prompt, you are attempting to set up the LLM to predict the right sequence of tokens. Prompt engineering is the process of designing high-quality prompts that guide LLMs to produce accurate outputs. This process involves tinkering to find the best prompt, optimizing prompt length, and evaluating a prompt’s writing style and structure in relation to the task. In the context of natural language processing and LLMs, a prompt is an input provided to the model to generate a response or prediction.

<mark>写提示，就是在设法把大语言模型摆到能预测出正确词元序列的位置上。提示工程是设计高质量提示的过程，用来引导大语言模型产生准确输出。这个过程包括反复试，找出最好的提示，优化提示长度，并按任务评估提示的写法与结构。在自然语言处理和大语言模型的语境里，提示是提供给模型、用来生成回答或预测的输入。</mark>

These prompts can be used to achieve various kinds of understanding and generation tasks such as text summarization, information extraction, question and answering, text classification, language or code translation, code generation, and code documentation or reasoning.

<mark>这些提示可以用来完成各种理解与生成任务，例如文本摘要、信息抽取、问答、文本分类、语言或代码翻译、代码生成，以及代码文档或推理 (Reasoning)。</mark>

Please feel free to refer to Google’s prompting guides2,3 with simple and effective prompting examples.

<mark>也可以参考 Google 的提示指南，2,3 里面有简单而有效的提示例子。</mark>

When prompt engineering, you will start by choosing a model. Prompts might need to be optimized for your specific model, regardless of whether you use Gemini language models in Vertex AI, GPT, Claude, or an open source model like Gemma or LLaMA.

<mark>做提示工程时，你要从选择模型开始。无论你用的是 Vertex AI 里的 Gemini 语言模型、GPT、Claude，还是 Gemma、LLaMA 这类开源模型，提示都可能需要针对你的具体模型来优化。</mark>

Besides the prompt, you will also need to tinker with the various configurations of a LLM.

<mark>除了提示，你还需要调试大语言模型的各种配置。</mark>

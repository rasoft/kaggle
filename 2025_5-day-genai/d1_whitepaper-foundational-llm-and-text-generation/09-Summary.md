# Summary

总结

In this whitepaper we have discussed the basics of transformers, upon which all modern-day LLMs are based. We detailed the evolution of the various LLM model architectures and their components. We’ve also seen the various methodologies you can use to train and fine-tune models efficiently and effectively. We briefly discussed prompt engineering and sampling techniques that greatly influence the output of an LLM, and also touched on possible applications of this technology. There are a number of key takeaways to keep in mind:

在本白皮书中，我们讨论了 Transformer 的基础，当今所有大语言模型 (LLM) 都建立在它之上。我们详述了各种大语言模型架构及其组件的演进。我们也看到了可以用来高效且有效地训练和微调 (fine-tune) 模型 (Model) 的各种方法。我们简要讨论了大大影响大语言模型输出的提示工程 (Prompt Engineering) 和采样 (Sampling) 技术，也触及了这项技术可能的应用。有若干要点需要记住：

- The transformer architecture is the basis for all modern-day LLMs. Across the various architectures mentioned in this whitepaper we see that it’s important not only to add more parameters to the model, but the composition of the dataset is equally important.

- Transformer 架构是当今所有大语言模型的基础。纵观本白皮书提到的各种架构，我们看到：不仅给模型增加更多参数很重要，数据集的构成同样重要。

- The order and strategies used for fine-tuning is important and may include multiple steps such as Instruction Tuning, Safety Tuning, etc. Supervised Fine Tuning (SFT) is important in capturing the essence of a task. RLHF, and potentially RLAIF, can be used to shift the distribution from the pretraining distribution to a more desired one through the power of the reward function, that can reward desirable behaviors and penalize undesirable ones.

- 微调所用的次序和策略很重要，可能包括指令微调、安全微调等多个步骤。监督微调 (Supervised Fine Tuning, SFT) 对抓住一项任务的要旨很重要。基于人类反馈的强化学习 (RLHF)，以及潜在的基于 AI 反馈的强化学习 (RLAIF)，可以借助奖励函数的力量，把分布从预训练 (pretraining) 分布移到一个更期望的分布上。奖励函数可以奖励可取的行为，并惩罚不可取的行为。

- Making inference from neural models efficient is an important problem and an active field of research. Many methods exist to reduce serving costs and latency with minimal impact to model performance, and some exact acceleration methods guarantee identical model outputs.

- 使神经网络模型的推断 (inference) 变得高效，是一个重要问题，也是一个活跃的研究领域。已有许多方法能在对模型性能影响很小的情况下降低服务成本和延迟，一些精确的加速方法则保证模型输出完全相同。

- Large language models can be used for a variety of tasks including summarization, translation, question answering, chat, code generation, and many more. You can create your own tasks using the Vertex and Makersuite text generation services which leverage Google’s latest language models. After the model has been trained and tuned, it is important to experiment with engineering prompts. You should use the technique most appropriate for the task-at-hand because LLMs can be sensitive to prompts k.

- 大语言模型可以用于多种任务，包括摘要、翻译、问答、聊天、代码生成等。你可以用 Vertex 和 Makersuite 的文本生成服务创建自己的任务，这些服务利用 Google 最新的语言模型。模型训练并调优之后，试验如何编排提示 (Prompt) 很重要。你应当使用最适合手头任务的技术，因为大语言模型对提示可能很敏感 k。

Furthermore, it is also possible to enhance task specific performance or creativity and diversity by tweaking the parameters corresponding to sampling techniques such as Top-K, Top-P, and Max decoding steps to find the optimum mix of correctness, diversity, and creativity required for the task at hand.

此外，也可以通过调整与采样技术对应的参数来增强任务专用的性能，或创造性与多样性，例如 Top-K、Top-P 和最大解码步数，从而为手头任务找到正确性、多样性和创造性所需的最优组合。

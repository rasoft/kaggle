# LLM output configuration

大语言模型输出配置

Once you choose your model you will need to figure out the model configuration. Most LLMs come with various configuration options that control the LLM’s output. Effective prompt engineering requires setting these configurations optimally for your task.

选定模型 (Model) 之后，就要弄清模型配置。大多数大语言模型 (LLM) 都带有多种配置项，用来控制大语言模型的输出。有效的提示工程 (Prompt Engineering) 要求按任务把这些配置设到合适的位置。

---

## Output length

输出长度

An important configuration setting is the number of tokens to generate in a response. Generating more tokens requires more computation from the LLM, leading to higher energy consumption, potentially slower response times, and higher costs.

一项重要配置是回答里要生成多少词元 (token)。生成更多词元需要大语言模型做更多计算，从而能耗更高，响应可能更慢，成本也更高。

Reducing the output length of the LLM doesn’t cause the LLM to become more stylistically or textually succinct in the output it creates, it just causes the LLM to stop predicting more tokens once the limit is reached. If your needs require a short output length, you’ll also possibly need to engineer your prompt to accommodate.

缩短大语言模型的输出长度，并不会让它写出的文字在风格或文笔上更简洁，只是让它在达到上限后停止继续预测词元。如果你需要较短的输出，多半还得把提示 (Prompt) 也设计成配合这一点。

Output length restriction is especially important for some LLM prompting techniques, like ReAct, where the LLM will keep emitting useless tokens after the response you want.

输出长度限制对某些大语言模型提示技巧尤其重要，例如推理与行动 (Reason and Act, ReAct)。用这些技巧时，大语言模型会在你想要的回答之后继续吐出无用词元。

Be aware, generating more tokens requires more computation from the LLM, leading to higher energy consumption and potentially slower response times, which leads to higher costs.

要注意：生成更多词元需要大语言模型做更多计算，从而能耗更高、响应可能更慢，最终成本更高。

---

## Sampling controls

采样控制

LLMs do not formally predict a single token. Rather, LLMs predict probabilities for what the next token could be, with each token in the LLM’s vocabulary getting a probability. Those token probabilities are then sampled to determine what the next produced token will be. Temperature, top-K, and top-P are the most common configuration settings that determine how predicted token probabilities are processed to choose a single output token.

大语言模型并不是直接预测出唯一一个词元。它预测的是下一个词元可能是什么的概率，词表里每个词元都有一个概率。然后再对这些概率做采样 (Sampling)，决定实际产生的下一个词元。温度 (temperature)、top-K 和 top-P 是最常见的配置，决定如何处理这些预测概率，从而选出一个输出词元。

### Temperature

温度 (temperature)

Temperature controls the degree of randomness in token selection. Lower temperatures are good for prompts that expect a more deterministic response, while higher temperatures can lead to more diverse or unexpected results. A temperature of 0 (greedy decoding) is deterministic: the highest probability token is always selected (though note that if two tokens have the same highest predicted probability, depending on how tiebreaking is implemented you may not always get the same output with temperature 0).

温度控制选词时的随机程度。较低的温度适合期望回答更确定的提示；较高的温度会带来更多样、更出乎意料的结果。温度为 0（贪心解码，greedy decoding）是确定的：总是选中概率最高的词元（不过要注意，如果两个词元的最高预测概率相同，取决于平局如何打破，温度取 0 时你也不一定每次都得到相同输出）。

Temperatures close to the max tend to create more random output. And as temperature gets higher and higher, all tokens become equally likely to be the next predicted token.

温度接近上限时，输出往往更随机。温度越来越高，所有词元成为下一个预测词元的可能性就趋于相等。

The Gemini temperature control can be understood in a similar way to the softmax function used in machine learning. A low temperature setting mirrors a low softmax temperature (T), emphasizing a single, preferred temperature with high certainty. A higher Gemini temperature setting is like a high softmax temperature, making a wider range of temperatures around the selected setting more acceptable. This increased uncertainty accommodates scenarios where a rigid, precise temperature may not be essential like for example when experimenting with creative outputs.

Gemini 的温度控制，可以类比机器学习里用的 softmax 函数来理解。低温度设置对应低的 softmax 温度 (T)，以很高的确定性强调某一个偏好温度。较高的 Gemini 温度设置就像高的 softmax 温度，让所选设置附近更宽的一段温度都变得可接受。这种增加的不确定性，适合并不必须卡死一个精确温度的场景，例如试验创造性输出的时候。

### Top-K and top-P

Top-K 与 top-P

Top-K and top-P (also known as nucleus sampling)4 are two sampling settings used in LLMs to restrict the predicted next token to come from tokens with the top predicted probabilities. Like temperature, these sampling settings control the randomness and diversity of generated text.

Top-K 和 top-P（也称核采样，nucleus sampling）4 是大语言模型里的两种采样设置，用来把预测的下一个词元限制在预测概率最高的那些词元之中。和温度一样，这些采样设置控制生成文本的随机性与多样性。

- Top-K sampling selects the top K most likely tokens from the model’s predicted distribution. The higher top-K, the more creative and varied the model’s output; the lower top-K, the more restive and factual the model’s output. A top-K of 1 is equivalent to greedy decoding.

Top-K 采样从模型预测分布里选出最可能的前 K 个词元。top-K 越高，模型输出越有创意、越多样；top-K 越低，输出越克制、越偏事实。top-K 为 1 等同于贪心解码。

- Top-P sampling selects the top tokens whose cumulative probability does not exceed a certain value (P). Values for P range from 0 (greedy decoding) to 1 (all tokens in the LLM’s vocabulary).

Top-P 采样选出累积概率不超过某个值 (P) 的那些最靠前的词元。P 的取值从 0（贪心解码）到 1（大语言模型词表中的全部词元）。

The best way to choose between top-K and top-P is to experiment with both methods (or both together) and see which one produces the results you are looking for.

在 top-K 和 top-P 之间做选择，最好的办法是两种都试（或一起试），看哪一种给出你想要的结果。

---

## Putting it all together

合在一起看

Choosing between top-K, top-P, temperature, and the number of tokens to generate, depends on the specific application and desired outcome, and the settings all impact one another. It’s also important to make sure you understand how your chosen model combines the different sampling settings together.

在 top-K、top-P、温度和要生成的词元数量之间如何取舍，取决于具体应用和想要的结果，而且这些设置会互相影响。同样重要的是弄清你所选的模型如何把不同的采样设置组合在一起。

If temperature, top-K, and top-P are all available (as in Vertex Studio), tokens that meet both the top-K and top-P criteria are candidates for the next predicted token, and then temperature is applied to sample from the tokens that passed the top-K and top-P criteria. If only top-K or top-P is available, the behavior is the same but only the one top-K or P setting is used.

如果温度、top-K 和 top-P 都可用（例如在 Vertex Studio 里），同时满足 top-K 和 top-P 标准的词元才是下一个预测词元的候选，然后再用温度从通过了 top-K 和 top-P 的词元里采样。如果只有 top-K 或只有 top-P 可用，行为相同，只是只用那一项 top-K 或 P 设置。

If temperature is not available, whatever tokens meet the top-K and/or top-P criteria are then randomly selected from to produce a single next predicted token.

如果没有温度这项，那么满足 top-K 和 / 或 top-P 标准的词元会被随机选出一个，作为下一个预测词元。

At extreme settings of one sampling configuration value, that one sampling setting either cancels out other configuration settings or becomes irrelevant.

某一项采样配置取到极端值时，这一项要么抵消其他配置，要么自己变得无关紧要。

- If you set temperature to 0, top-K and top-P become irrelevant–the most probable token becomes the next token predicted. If you set temperature extremely high (above 1–generally into the 10s), temperature becomes irrelevant and whatever tokens make it through the top-K and/or top-P criteria are then randomly sampled to choose a next predicted token.

如果把温度设为 0，top-K 和 top-P 就无关紧要了——概率最高的词元成为下一个预测词元。如果把温度设得极高（高于 1，一般到十几），温度就变得无关紧要，凡是通过 top-K 和 / 或 top-P 标准的词元都会被随机采样，从中选出下一个预测词元。

- If you set top-K to 1, temperature and top-P become irrelevant. Only one token passes the top-K criteria, and that token is the next predicted token. If you set top-K extremely high, like to the size of the LLM’s vocabulary, any token with a nonzero probability of being the next token will meet the top-K criteria and none are selected out.

如果把 top-K 设为 1，温度和 top-P 就无关紧要了。只有一个词元通过 top-K 标准，它就是下一个预测词元。如果把 top-K 设得极高，例如设成大语言模型的词表大小，任何成为下一个词元的概率不为零的词元都会满足 top-K 标准，没有词元被筛掉。

- If you set top-P to 0 (or a very small value), most LLM sampling implementations will then only consider the most probable token to meet the top-P criteria, making temperature and top-K irrelevant. If you set top-P to 1, any token with a nonzero probability of being the next token will meet the top-P criteria, and none are selected out.

如果把 top-P 设为 0（或一个很小的值），大多数大语言模型的采样实现就只会把概率最高的词元视为满足 top-P 标准，从而使温度和 top-K 无关紧要。如果把 top-P 设为 1，任何成为下一个词元的概率不为零的词元都会满足 top-P 标准，没有词元被筛掉。

As a general starting point, a temperature of .2, top-P of .95, and top-K of 30 will give you relatively coherent results that can be creative but not excessively so. If you want especially creative results, try starting with a temperature of .9, top-P of .99, and top-K of 40. And if you want less creative results, try starting with a temperature of .1, top-P of .9, and top-K of 20. Finally, if your task always has a single correct answer (e.g., answering a math problem), start with a temperature of 0.

作为一个一般的起点，温度 0.2、top-P 0.95、top-K 30，会给出相对连贯的结果，可以有创意，但不会过头。如果特别想要有创意的结果，可以先试温度 0.9、top-P 0.99、top-K 40。如果想要创意更少的结果，可以先试温度 0.1、top-P 0.9、top-K 20。最后，如果任务总是只有一个正确答案（例如解数学题），就从温度 0 开始。

NOTE: With more freedom (higher temperature, top-K, top-P, and output tokens), the LLM might generate text that is less relevant.

注意：自由度更大时（更高的温度、top-K、top-P，以及更多输出词元），大语言模型生成的文本可能更不切题。

WARNING: Have you ever seen a response ending with a large amount of filler words? This is also known as the "repetition loop bug", which is a common issue in Large Language Models where the model gets stuck in a cycle, repeatedly generating the same (filler) word, phrase, or sentence structure, often exacerbated by inappropriate temperature and top-k/top-p settings. This can occur at both low and high temperature settings, though for different reasons. At low temperatures, the model becomes overly deterministic, sticking rigidly to the highest probability path, which can lead to a loop if that path revisits previously generated text. Conversely, at high temperatures, the model's output becomes excessively random, increasing the probability that a randomly chosen word or phrase will, by chance, lead back to a prior state, creating a loop due to the vast number of available options. In both cases, the model's sampling process gets "stuck," resulting in monotonous and unhelpful output until the output window is filled. Solving this often requires careful tinkering with temperature and top-k/top-p values to find the optimal balance between determinism and randomness.

警告：你有没有见过回答末尾堆着大量填充词？这也叫「重复循环缺陷」（repetition loop bug），是大语言模型里的常见问题：模型陷进一个循环，反复生成同一个（填充）词、短语或句子结构，不合适的温度和 top-k / top-p 设置往往会让它更严重。低温和高温都可能发生，原因不同。低温时，模型变得过于确定，死死贴着概率最高的路径；如果这条路径又回到先前生成过的文本，就会形成循环。反过来，高温时，模型输出变得过度随机，随机选中的词或短语碰巧回到先前状态的概率上升，可选词太多，于是形成循环。两种情况下，模型的采样过程都「卡住了」，结果是单调、没用的输出，直到输出窗口被填满。解决它通常要仔细调试温度和 top-k / top-p，在确定性与随机性之间找到合适的平衡。

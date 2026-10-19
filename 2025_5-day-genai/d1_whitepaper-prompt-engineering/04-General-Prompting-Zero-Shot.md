# Prompting techniques

<mark>提示技巧</mark>

LLMs are tuned to follow instructions and are trained on large amounts of data so they can understand a prompt and generate an answer. But LLMs aren’t perfect; the clearer your prompt text, the better it is for the LLM to predict the next likely text. Additionally, specific techniques that take advantage of how LLMs are trained and how LLMs work will help you get the relevant results from LLMs.

<mark>大语言模型 (LLM) 被调校成会遵循指令，并在大量数据上训练，因此能理解提示 (Prompt) 并生成回答。但大语言模型并不完美；提示文本越清楚，大语言模型就越容易预测出接下来最可能的文本。此外，利用大语言模型如何训练、如何工作的特定技巧，能帮你从大语言模型得到切题的结果。</mark>

Now that we understand what prompt engineering is and what it takes, let’s dive into some examples of the most important prompting techniques.

<mark>现在我们已经理解提示工程 (Prompt Engineering) 是什么、需要什么，下面来看一些最重要的提示技巧的例子。</mark>

---

## General prompting / zero shot

<mark>一般提示 / 零样本 (zero-shot)</mark>

A zero-shot5 prompt is the simplest type of prompt. It only provides a description of a task and some text for the LLM to get started with. This input could be anything: a question, a start of a story, or instructions. The name zero-shot stands for ’no examples’.

<mark>零样本提示 5 是最简单的一类提示。它只提供任务描述，以及一段让大语言模型起步的文本。这段输入可以是任何东西：一个问题、一个故事的开头，或一组指令。零样本这个名字的意思是「没有示例」。</mark>

Let’s use Vertex AI Studio (for Language) in Vertex AI,6 which provides a playground to test prompts. In Table 1, you will see an example zero-shot prompt to classify movie reviews.

<mark>我们用 Vertex AI 里的 Vertex AI Studio（面向语言），6 它提供一个试验提示的试验场 (playground)。表 1 是一个给电影评论分类的零样本提示例子。</mark>

The table format as used below is a great way of documenting prompts. Your prompts will likely go through many iterations before they end up in a codebase, so it’s important to keep track of your prompt engineering work in a disciplined, structured way. More on this table format, the importance of tracking prompt engineering work, and the prompt development process is in the Best Practices section later in this chapter (“Document the various prompt attempts”).

<mark>下面这种表格是记录提示的好办法。提示在进入代码库之前往往会迭代很多次，所以要用有纪律、有结构的方式跟踪提示工程工作。关于这种表格、跟踪提示工程工作的重要性，以及提示开发过程，见本章后面的「最佳实践」（「记录各次提示尝试」）。</mark>

The model temperature should be set to a low number, since no creativity is needed, and we use the gemini-pro default top-K and top-P values, which effectively disable both settings (see ‘LLM Output Configuration’ above). Pay attention to the generated output. The words disturbing and masterpiece should make the prediction a little more complicated, as both words are used in the same sentence.

<mark>模型 (Model) 温度 (temperature) 应设得较低，因为这里不需要创意。我们使用 gemini-pro 默认的 top-K 和 top-P，这两项实际上都被关掉了（见上文「大语言模型输出配置」）。注意生成的输出。disturbing 和 masterpiece 这两个词会让预测稍难一些，因为它们出现在同一句话里。</mark>

| | |
| --- | --- |
| **Name** | 1_1_movie_classification |
| **Goal** | Classify movie reviews as positive, neutral or negative. |
| **Model** | gemini-pro |
| **Temperature** | 0.1 |
| **Token Limit** | 5 |
| **Top-K** | N/A |
| **Top-P** | 1 |

**Prompt**

```text
Classify movie reviews as POSITIVE, NEUTRAL or NEGATIVE.
Review: "Her" is a disturbing study revealing the direction
humanity is headed if AI is allowed to keep evolving,
unchecked. I wish there were more movies like this masterpiece.
Sentiment:
```

**Output**

```text
POSITIVE
```

**Table 1. An example of zero-shot prompting**

<mark>表 1：零样本提示的一个例子。</mark>

| | |
| --- | --- |
| **<mark>名称</mark>** | 1_1_movie_classification |
| **<mark>目标</mark>** | <mark>把电影评论分为正面、中性或负面。</mark> |
| **<mark>模型</mark>** | gemini-pro |
| **<mark>温度</mark>** | 0.1 |
| **<mark>词元上限</mark>** | 5 |
| **Top-K** | N/A |
| **Top-P** | 1 |

**<mark>提示</mark>**

<mark>把电影评论分为 POSITIVE、NEUTRAL 或 NEGATIVE。
评论："Her" 是一部令人不安的研究，揭示了如果允许 AI 不受约束地继续演化，人类将走向何方。我希望有更多像这部杰作一样的电影。
情感：</mark>

**<mark>输出</mark>**

```text
POSITIVE
```

When zero-shot doesn’t work, you can provide demonstrations or examples in the prompt, which leads to “one-shot” and “few-shot” prompting.

<mark>零样本行不通时，可以在提示里提供示范或示例，这就引出「单样本 (one-shot)」和「少样本 (few-shot)」提示。</mark>

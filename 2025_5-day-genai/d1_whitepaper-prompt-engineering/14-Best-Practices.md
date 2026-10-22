# Best Practices

最佳实践

Finding the right prompt requires tinkering. Language Studio in Vertex AI is a perfect place to play around with your prompts, with the ability to test against the various models.

找到合适的提示 (Prompt) 需要反复试。Vertex AI 里的 Language Studio 是摆弄提示的好地方，可以针对各种模型 (Model) 做测试。

Use the following best practices to become a pro in prompt engineering.

用下面这些最佳实践，成为提示工程 (Prompt Engineering) 的行家。

---

## Provide examples

提供示例

The most important best practice is to provide (one shot / few shot) examples within a prompt. This is highly effective because it acts as a powerful teaching tool. These examples showcase desired outputs or similar responses, allowing the model to learn from them and tailor its own generation accordingly. It’s like giving the model a reference point or target to aim for, improving the accuracy, style, and tone of its response to better match your expectations.

最重要的最佳实践，是在提示里提供（单样本 / 少样本，one shot / few shot）示例。这非常有效，因为它是一件有力的教学工具。这些示例展示期望的输出或类似的回答，让模型从中学习，并据此调整自己的生成。就像给模型一个参照点或要瞄准的目标，从而提高回答的准确性、风格和语气，使之更符合你的期望。

---

## Design with simplicity

设计要简单

Prompts should be concise, clear, and easy to understand for both you and the model. As a rule of thumb, if it’s already confusing for you it will likely be also confusing for the model. Try not to use complex language and don’t provide unnecessary information.

提示应当简洁、清楚，对你和模型都容易理解。经验是：如果它已经让你糊涂，多半也会让模型糊涂。尽量不用复杂的语言，也不要提供不必要的信息。

Examples:

例子：

BEFORE:

```text
I am visiting New York right now, and I'd like to hear more about great
locations. I am with two 3 year old kids. Where should we go during
our vacation?
```

AFTER REWRITE:

```text
Act as a travel guide for tourists. Describe great places to visit in
New York Manhattan with a 3 year old.
```

改写前：我现在正在纽约，想多听听有哪些好地方。我和两个 3 岁的孩子在一起。假期里我们该去哪里？

改写后：为游客扮演旅行向导。描述在纽约曼哈顿带一个 3 岁孩子值得去的好地方。

Try using verbs that describe the action. Here’s a set of examples:

试着用描述动作的动词。下面是一组例子：

Act, Analyze, Categorize, Classify, Contrast, Compare, Create, Describe, Define, Evaluate, Extract, Find, Generate, Identify, List, Measure, Organize, Parse, Pick, Predict, Provide, Rank, Recommend, Return, Retrieve, Rewrite, Select, Show, Sort, Summarize, Translate, Write.

扮演、分析、归类、分类、对照、比较、创建、描述、定义、评估 (Evaluation)、抽取、查找、生成、识别、列出、测量、组织、解析、挑选、预测、提供、排名、推荐、返回、检索、改写、选择、展示、排序、总结、翻译、写作。

---

## Be specific about the output

把输出说具体

Be specific about the desired output. A concise instruction might not guide the LLM enough or could be too generic. Providing specific details in the prompt (through system or context prompting) can help the model to focus on what’s relevant, improving the overall accuracy.

把期望的输出说具体。一条简短的指令可能不足以引导大语言模型 (LLM)，也可能太泛。在提示里提供具体细节（通过系统提示或上下文提示，system or context prompting）能帮模型聚焦相关内容，从而提高整体准确性。

Examples:

例子：

DO:

```text
Generate a 3 paragraph blog post about the top 5 video game consoles.
The blog post should be informative and engaging, and it should be
written in a conversational style.
```

DO NOT:

```text
Generate a blog post about video game consoles.
```

要这样做：写一篇 3 段的博客，讲排名前 5 的电子游戏主机。博客应当信息充分、吸引人，并用交谈式的风格来写。

不要这样做：写一篇关于电子游戏主机的博客。

---

## Use Instructions over Constraints

优先用指令，而不是约束

Instructions and constraints are used in prompting to guide the output of a LLM.

提示里用指令和约束来引导大语言模型的输出。

- An instruction provides explicit instructions on the desired format, style, or content of the response. It guides the model on what the model should do or produce.

指令明确说明回答期望的格式、风格或内容。它引导模型应当做什么、应当产出什么。

- A constraint is a set of limitations or boundaries on the response. It limits what the model should not do or avoid.

约束是对回答的一组限制或边界。它限制模型不应当做什么、应当避开什么。

Growing research suggests that focusing on positive instructions in prompting can be more effective than relying heavily on constraints. This approach aligns with how humans prefer positive instructions over lists of what not to do.

越来越多的研究表明，在提示里聚焦正面指令，可能比重度依赖约束更有效。这和人类更喜欢正面指令、而不是一长串「不要做什么」是一致的。

Instructions directly communicate the desired outcome, whereas constraints might leave the model guessing about what is allowed. It gives flexibility and encourages creativity within the defined boundaries, while constraints can limit the model’s potential. Also a list of constraints can clash with each other.

指令直接传达期望的结果，而约束可能让模型去猜什么是允许的。指令在划定的边界内给出灵活性并鼓励创意，约束则可能限制模型的潜力。一列约束彼此之间也可能冲突。

Constraints are still valuable but in certain situations. To prevent the model from generating harmful or biased content or when a strict output format or style is needed.

约束在某些情况下仍然有价值：防止模型生成有害或有偏见的内容，或者需要严格的输出格式或风格时。

If possible, use positive instructions: instead of telling the model what not to do, tell it what to do instead. This can avoid confusion and improve the accuracy of the output.

如果可能，用正面指令：不要告诉模型不要做什么，改成告诉它要做什么。这可以避免混淆，并提高输出的准确性。

DO:

```text
Generate a 1 paragraph blog post about the top 5 video game consoles.
Only discuss the console, the company who made it, the year, and total
sales.
```

DO NOT:

```text
Generate a 1 paragraph blog post about the top 5 video game consoles.
Do not list video game names.
```

要这样做：写一段博客，讲排名前 5 的电子游戏主机。只讨论主机、制造它的公司、年份和总销量。

不要这样做：写一段博客，讲排名前 5 的电子游戏主机。不要列出电子游戏的名字。

As a best practice, start by prioritizing instructions, clearly stating what you want the model to do and only use constraints when necessary for safety, clarity or specific requirements. Experiment and iterate to test different combinations of instructions and constraints to find what works best for your specific tasks, and document these.

作为最佳实践，先优先用指令，清楚说明你要模型做什么，只在安全、清晰或特定要求所必要时才用约束。试验并迭代，测试指令和约束的不同组合，找出对你的具体任务最好用的那种，并把这些记下来。

---

## Control the max token length

控制最大词元 (token) 长度

To control the length of a generated LLM response, you can either set a max token limit in the configuration or explicitly request a specific length in your prompt. For example:

要控制大语言模型生成回答的长度，可以在配置里设置最大词元上限，也可以在提示里明确要求某个具体长度。例如：

"Explain quantum physics in a tweet length message."

「用一条推文那么长的消息解释量子物理。」

---

## Use variables in prompts

在提示里使用变量

To reuse prompts and make it more dynamic use variables in the prompt, which can be changed for different inputs. E.g. as shown in Table 20, a prompt which gives facts about a city. Instead of hardcoding the city name in the prompt, use a variable. Variables can save you time and effort by allowing you to avoid repeating yourself. If you need to use the same piece of information in multiple prompts, you can store it in a variable and then reference that variable in each prompt. This makes a lot of sense when integrating prompts into your own applications.

为了复用提示并让它更动态，在提示里使用变量，变量可以随不同输入而改变。例如表 20，一条给出城市事实的提示。不要把城市名硬编码进提示，改用变量。变量让你不必重复自己，从而节省时间和力气。如果同一条信息要在多条提示里使用，可以把它存在变量里，再在每条提示里引用该变量。把提示集成进你自己的应用时，这很有意义。

**Prompt**

```text
VARIABLES
{city} = "Amsterdam"
PROMPT
You are a travel guide. Tell me a fact about the city: {city}
```

**Output**

```text
Amsterdam is a beautiful city full of canals, bridges, and narrow streets. It’s a
great place to visit for its rich history, culture, and nightlife.
```

**Table 20. Using variables in prompts**

表 20：在提示里使用变量。

**提示**

变量
{city} = "Amsterdam"
提示
你是一名旅行向导。告诉我关于这座城市的一个事实：{city}

**输出**

阿姆斯特丹是一座美丽的城市，满是运河、桥和窄街。它历史、文化和夜生活丰富，是个很好的游览地。

---

## Experiment with input formats and writing styles

试验输入格式和写法

Different models, model configurations, prompt formats, word choices, and submits can yield different results. Therefore, it’s important to experiment with prompt attributes like the style, the word choice, and the type prompt (zero shot, few shot, system prompt).

不同的模型、模型配置、提示格式、用词和提交方式，会得到不同结果。因此，要试验提示的属性，例如风格、用词，以及提示类型（零样本 zero shot、少样本 few shot、系统提示 system prompt）。

For example a prompt with the goal to generate text about the revolutionary video game console Sega Dreamcast, can be formulated as a question, a statement or an instruction, resulting in different outputs:

例如，目标是生成关于革命性电子游戏主机 Sega Dreamcast 的文本，可以写成问题、陈述或指令，结果会不同：

- Question: What was the Sega Dreamcast and why was it such a revolutionary console?

问题：Sega Dreamcast 是什么，为什么它是一台如此具有革命性的主机？

- Statement: The Sega Dreamcast was a sixth-generation video game console released by Sega in 1999. It...

陈述：Sega Dreamcast 是 Sega 在 1999 年发布的第六代电子游戏主机。它……

- Instruction: Write a single paragraph that describes the Sega Dreamcast console and explains why it was so revolutionary.

指令：写一段话，描述 Sega Dreamcast 主机，并解释它为什么如此具有革命性。

---

## For few-shot prompting with classification tasks, mix up the classes

分类任务的少样本提示要把类别打乱

Generally speaking, the order of your few-shots examples should not matter much. However, when doing classification tasks, make sure you mix up the possible response classes in the few shot examples. This is because you might otherwise be overfitting to the specific order of the examples. By mixing up the possible response classes, you can ensure that the model is learning to identify the key features of each class, rather than simply memorizing the order of the examples. This will lead to more robust and generalizable performance on unseen data.

一般来说，少样本示例的顺序不应该有太大影响。不过做分类任务时，一定要把少样本示例里可能的回答类别打乱。否则你可能过拟合到示例的特定顺序上。把可能的回答类别打乱，可以确保模型在学习识别每一类的关键特征，而不是仅仅记住示例的顺序。这样在未见过的数据上会更稳健、更能泛化。

A good rule of thumb is to start with 6 few shot examples and start testing the accuracy from there.

一个好的经验是从 6 个少样本示例开始，再从那里测试准确率。

---

## Adapt to model updates

适应模型更新

It’s important for you to stay on top of model architecture changes, added data, and capabilities. Try out newer model versions and adjust your prompts to better leverage new model features. Tools like Vertex AI Studio are great to store, test, and document the various versions of your prompt.

你要跟上模型架构的变化、新增的数据和能力。试用更新的模型版本，并调整提示，以便更好地利用新的模型特性。Vertex AI Studio 这类工具很适合存储、测试和记录提示的各个版本。

---

## Experiment with output formats

试验输出格式

Besides the prompt input format, consider experimenting with the output format. For non-creative tasks like extracting, selecting, parsing, ordering, ranking, or categorizing data try having your output returned in a structured format like JSON or XML.

除了提示的输入格式，也考虑试验输出格式。对抽取、选择、解析、排序、排名或给数据分类这类非创意任务，试着让输出以 JSON 或 XML 这类结构化格式返回。

There are some benefits in returning JSON objects from a prompt that extracts data. In a real-world application I don’t need to manually create this JSON format, I can already return the data in a sorted order (very handy when working with datetime objects), but most importantly, by prompting for a JSON format it forces the model to create a structure and limit hallucinations.

用抽取数据的提示返回 JSON 对象有一些好处。在真实应用里，我不需要手工拼这种 JSON 格式，数据已经可以按排好的顺序返回（处理 datetime 对象时非常方便）。更重要的是，要求 JSON 格式会迫使模型建立结构，并限制幻觉 (hallucination)。

In summary, benefits of using JSON for your output:

概括起来，用 JSON 作为输出的好处：

- Returns always in the same style

返回的风格始终一致

- Focus on the data you want to receive

聚焦你想收到的数据

- Less chance for hallucinations

幻觉的机会更少

- Make it relationship aware

让它意识到关系

- You get data types

你得到数据类型

- You can sort it

你可以把它排序

Table 4 in the few-shot prompting section shows an example on how to return structured output.

少样本提示一节里的表 4，展示了如何返回结构化输出的例子。

印刷本把表 4 放在「少样本提示」一节。表 4 实际在系统提示一节，是用 JSON 返回电影评论分类的例子。

---

## JSON Repair

JSON 修复 (JSON Repair)

While returning data in JSON format offers numerous advantages, it's not without its drawbacks. The structured nature of JSON, while beneficial for parsing and use in applications, requires significantly more tokens than plain text, leading to increased processing time and higher costs. Furthermore, JSON's verbosity can easily consume the entire output window, becoming especially problematic when the generation is abruptly cut off due to token limits. This truncation often results in invalid JSON, missing crucial closing braces or brackets, rendering the output unusable. Fortunately, tools like the json-repair library (available on PyPI) can be invaluable in these situations. This library intelligently attempts to automatically fix incomplete or malformed JSON objects, making it a crucial ally when working with LLM-generated JSON, especially when dealing with potential truncation issues.

以 JSON 格式返回数据有很多优点，但也不是没有缺点。JSON 的结构化有利于解析和在应用里使用，但比纯文本需要明显更多的词元，从而处理时间更长、成本更高。而且 JSON 很啰嗦，很容易占满整个输出窗口；生成因词元上限被突然截断时，问题尤其大。这种截断常常得到非法 JSON，缺了关键的闭合花括号或方括号，输出就没法用。幸好，json-repair 库（可在 PyPI 上取得）在这些情况下很有价值。这个库会聪明地尝试自动修复不完整或畸形的 JSON 对象，在处理大语言模型生成的 JSON、尤其是可能被截断时，它是一个关键帮手。

---

## Working with Schemas

使用模式 (schema)

Using structured JSON as an output is a great solution, as we've seen multiple times in this paper. But what about input? While JSON is excellent for structuring the output the LLM generates, it can also be incredibly useful for structuring the input you provide. This is where JSON Schemas come into play. A JSON Schema defines the expected structure and data types of your JSON input. By providing a schema, you give the LLM a clear blueprint of the data it should expect, helping it focus its attention on the relevant information and reducing the risk of misinterpreting the input. Furthermore, schemas can help establish relationships between different pieces of data and even make the LLM "time-aware" by including date or timestamp fields with specific formats.

如本文多次所见，用结构化 JSON 作为输出是个很好的办法。那输入呢？JSON 很适合组织大语言模型生成的输出，用来组织你提供的输入也同样有用。这就是 JSON 模式 (JSON Schema) 发挥作用的地方。JSON 模式定义 JSON 输入期望的结构和数据类型。提供模式，就是给大语言模型一份它应当预期的数据蓝图，帮助它把注意力集中在相关信息上，并降低误解输入的风险。此外，模式有助于在不同数据之间建立关系，甚至可以通过带特定格式的日期或时间戳字段，让大语言模型「有时间感」。

Here's a simple example:

下面是一个简单例子：

Let's say you want to use an LLM to generate descriptions for products in an e-commerce catalog. Instead of just providing a free-form text description of the product, you can use a JSON schema to define the product's attributes:

假设你想用大语言模型为电商目录里的产品生成描述。与其只提供一段自由文本的产品描述，不如用 JSON 模式定义产品的属性：

```json
{
  "type": "object",
  "properties": {
    "name": { "type": "string", "description": "Product name" },
    "category": { "type": "string", "description": "Product category" },
    "price": { "type": "number", "format": "float", "description": "Product price" },
    "features": {
      "type": "array",
      "items": { "type": "string" },
      "description": "Key features of the product"
    },
    "release_date": { "type": "string", "format": "date", "description": "Date the product was released"}
  },
```

**Snippet 5. Definition of the structured output schema**

片段 5：结构化输出模式的定义。印刷页在 `properties` 的闭合处被截断，后面的花括号没有印出来。

Then, you can provide the actual product data as a JSON object that conforms to this schema:

然后，你可以提供符合该模式的实际产品数据，作为一个 JSON 对象：

```json
{
  "name": "Wireless Headphones",
  "category": "Electronics",
  "price": 99.99,
  "features": ["Noise cancellation", "Bluetooth 5.0", "20-hour battery life"],
  "release_date": "2023-10-27"
}
```

**Snippet 6. Structured output from the LLM**

片段 6：来自大语言模型的结构化输出。

印刷标题写成「来自大语言模型的结构化输出」。框里的 JSON 是符合模式的产品输入：无线耳机，类别 Electronics，价格 99.99，特性为降噪、Bluetooth 5.0、20 小时电池续航，发布日期 2023-10-27。

By preprocessing your data and instead of providing full documents only providing both the schema and the data, you give the LLM a clear understanding of the product's attributes, including its release date, making it much more likely to generate an accurate and relevant description. This structured input approach, guiding the LLM's attention to the relevant fields, is especially valuable when working with large volumes of data or when integrating LLMs into complex applications.

先预处理数据，不要提供整篇文档，只同时提供模式和数据，你就让大语言模型清楚理解产品属性，包括发布日期，从而更可能生成准确、切题的描述。这种结构化输入把大语言模型的注意力引到相关字段上，在处理大量数据、或把大语言模型集成进复杂应用时尤其有价值。

---

## Experiment together with other prompt engineers

和其他提示工程师一起试验

If you are in a situation where you have to try to come up with a good prompt, you might want to find multiple people to make an attempt. When everyone follows the best practices (as listed in this chapter) you are going to see a variance in performance between all the different prompt attempts.

如果你必须试着写出一条好提示，不妨找几个人各自试一次。当每个人都遵循本章列出的最佳实践时，你仍会看到不同提示尝试之间的表现有差异。

---

## CoT Best practices

思维链 (Chain of Thought, CoT) 最佳实践

For CoT prompting, putting the answer after the reasoning is required because the generation of the reasoning changes the tokens that the model gets when it predicts the final answer.

对思维链提示，必须把答案放在推理 (Reasoning) 之后，因为推理的生成会改变模型在预测最终答案时拿到的词元。

With CoT and self-consistency you need to be able to extract the final answer from your prompt, separated from the reasoning.

使用思维链和自洽 (self-consistency) 时，你需要能从提示的结果里抽出最终答案，并把它和推理分开。

For CoT prompting, set the temperature to 0.

对思维链提示，把温度 (temperature) 设为 0。

Chain of thought prompting is based on greedy decoding, predicting the next word in a sequence based on the highest probability assigned by the language model. Generally speaking, when using reasoning, to come up with the final answer, there’s likely one single correct answer. Therefore the temperature should always set to 0.

思维链提示基于贪心解码 (greedy decoding)：按语言模型赋予的最高概率预测序列中的下一个词。一般来说，用推理来得出最终答案时，很可能只有一个正确答案。因此温度应当始终设为 0。

---

## Document the various prompt attempts

记录各次提示尝试

The last tip was mentioned before in this chapter, but we can’t stress enough how important it is: document your prompt attempts in full detail so you can learn over time what went well and what did not.

最后这条在本章前面提到过，但再怎么强调也不为过：把你的提示尝试完整详细地记下来，这样你才能随时间看出什么行、什么不行。

Prompt outputs can differ across models, across sampling settings, and even across different versions of the same model. Moreover, even across identical prompts to the same model, small differences in output sentence formatting and word choice can occur. (For example, as mentioned previously, if two tokens have the same predicted probability, ties may be broken randomly. This can then impact subsequent predicted tokens.).

提示的输出会因模型不同、采样 (Sampling) 设置不同、甚至同一模型的不同版本而不同。而且，即使对同一模型发出完全相同的提示，输出的句子格式和用词也可能有小差异。（例如前面说过，如果两个词元的预测概率相同，平局可能被随机打破。这接着会影响后续预测的词元。）

We recommend creating a Google Sheet with Table 21 as a template. The advantages of this approach are that you have a complete record when you inevitably have to revisit your prompting work–either to pick it up in the future (you’d be surprised how much you can forget after just a short break), to test prompt performance on different versions of a model, and to help debug future errors.

我们建议用表 21 当模板建一张 Google 表格。这样做的好处是，当你不可避免地要回头看提示工作时，会有一份完整记录：要么是将来接着做（短短休息之后你会忘掉多少，会让你吃惊），要么是在模型的不同版本上测试提示表现，要么是帮助调试以后的错误。

Beyond the fields in this table, it’s also helpful to track the version of the prompt (iteration), a field to capture if the result was OK/NOT OK/SOMETIMES OK, and a field to capture feedback. If you’re lucky enough to be using Vertex AI Studio, save your prompts (using the same name and version as listed in your documentation) and track the hyperlink to the saved prompt in the table. This way, you’re always one click away from re-running your prompts.

除了这张表里的字段，跟踪提示的版本（迭代）也有帮助，再加一个字段记录结果是 OK / NOT OK / SOMETIMES OK，以及一个字段记录反馈。如果你有幸在用 Vertex AI Studio，把提示保存下来（名称和版本与文档里列出的一致），并在表里跟踪已保存提示的超链接。这样，你始终离重新运行提示只有一次点击。

When working on a retrieval augmented generation system, you should also capture the specific aspects of the RAG system that impact what content was inserted into the prompt, including the query, chunk settings, chunk output, and other information.

做检索增强生成 (RAG) 系统时，还应当记下 RAG 系统里影响「哪些内容被插入提示」的具体方面，包括查询、分块设置、分块输出，以及其他信息。

Once you feel the prompt is close to perfect, take it to your project codebase. And in the codebase, save prompts in a separate file from code, so it’s easier to maintain. Finally, ideally your prompts are part of an operationalized system, and as a prompt engineer you should rely on automated tests and evaluation procedures to understand how well your prompt generalizes to a task.

一旦你觉得提示接近完美，就把它放进项目代码库。在代码库里，把提示存在与代码分开的文件中，这样更容易维护。最后，理想情况下你的提示是一套可运营系统的一部分；作为提示工程师，你应当依靠自动化测试和评估流程，来理解提示在一项任务上泛化得有多好。

Prompt engineering is an iterative process. Craft and test different prompts, analyze, and document the results. Refine your prompt based on the model’s performance. Keep experimenting until you achieve the desired output. When you change a model or model configuration, go back and keep experimenting with the previously used prompts.

提示工程是一个迭代过程。撰写并测试不同的提示，分析结果，并记下来。根据模型的表现打磨提示。持续试验，直到得到期望的输出。更换模型或模型配置时，回到先前用过的提示，继续试验。

| Name | [name and version of your prompt] | | |
| --- | --- | --- | --- |
| Goal | [One sentence explanation of the goal of this attempt] | | |
| Model | [name and version of the used model] | | |
| Temperature | [value between 0 - 1] | Token Limit | [number] |
| Top-K | [number] | Top-P | [number] |
| Prompt | [Write all the full prompt] | | |
| Output | [Write out the output or multiple outputs] | | |

**Table 21. A template for documenting prompts**

表 21：记录提示的模板。

| 名称 | ［你的提示的名称和版本］ | | |
| --- | --- | --- | --- |
| 目标 | ［用一句话说明这次尝试的目标］ | | |
| 模型 | ［所用模型的名称和版本］ | | |
| 温度 | ［0 到 1 之间的值］ | 词元上限 | ［数字］ |
| Top-K | ［数字］ | Top-P | ［数字］ |
| 提示 | ［写下完整的提示］ | | |
| 输出 | ［写下输出，或多次输出］ | | |

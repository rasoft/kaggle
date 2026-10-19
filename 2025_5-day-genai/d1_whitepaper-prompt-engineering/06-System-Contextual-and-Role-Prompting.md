# System, contextual and role prompting

<mark>系统提示 (system prompting)、上下文提示 (contextual prompting) 与角色提示 (role prompting)</mark>

System, contextual and role prompting are all techniques used to guide how LLMs generate text, but they focus on different aspects:

<mark>系统提示、上下文提示和角色提示都是用来引导大语言模型 (LLM) 如何生成文本的技巧，但侧重点不同：</mark>

- System prompting sets the overall context and purpose for the language model. It defines the ‘big picture’ of what the model should be doing, like translating a language, classifying a review etc.

<mark>系统提示为语言模型设定总体上下文和目的。它定义模型该做的「大局」，例如翻译一种语言、给评论分类等。</mark>

- Contextual prompting provides specific details or background information relevant to the current conversation or task. It helps the model to understand the nuances of what’s being asked and tailor the response accordingly.

<mark>上下文提示提供与当前对话或任务相关的具体细节或背景信息。它帮助模型理解所问之事的细微差别，并据此调整回答。</mark>

- Role prompting assigns a specific character or identity for the language model to adopt. This helps the model generate responses that are consistent with the assigned role and its associated knowledge and behavior.

<mark>角色提示给语言模型指定一个要扮演的角色或身份。这帮助模型生成与该角色及其相关知识、行为一致的回答。</mark>

There can be considerable overlap between system, contextual, and role prompting. E.g. a prompt that assigns a role to the system, can also have a context.

<mark>系统提示、上下文提示和角色提示之间可以有相当多的重叠。例如，一条给系统指定角色的提示 (Prompt)，也可以带有上下文。</mark>

However, each type of prompt serves a slightly different primary purpose:

<mark>不过，每一类提示的首要目的略有不同：</mark>

- System prompt: Defines the model’s fundamental capabilities and overarching purpose.

<mark>系统提示：定义模型 (Model) 的基本能力和总目的。</mark>

- Contextual prompt: Provides immediate, task-specific information to guide the response. It’s highly specific to the current task or input, which is dynamic.

<mark>上下文提示：提供即时的、针对任务的信息来引导回答。它高度针对当前任务或输入，而当前任务或输入是动态的。</mark>

- Role prompt: Frames the model’s output style and voice. It adds a layer of specificity and personality.

<mark>角色提示：框定模型输出的风格和语气。它加上一层具体性和个性。</mark>

Distinguishing between system, contextual, and role prompts provides a framework for designing prompts with clear intent, allowing for flexible combinations and making it easier to analyze how each prompt type influences the language model’s output.

<mark>把系统提示、上下文提示和角色提示区分开，就有了一个框架，用来设计意图清楚的提示，允许灵活组合，也更容易分析每一类提示如何影响语言模型的输出。</mark>

Let’s dive into these three different kinds of prompts.

<mark>下面分别看这三类提示。</mark>

---

## System prompting

<mark>系统提示</mark>

Table 3 contains a system prompt, where I specify additional information on how to return the output. I increased the temperature to get a higher creativity level, and I specified a higher token limit. However, because of my clear instruction on how to return the output the model didn’t return extra text.

<mark>表 3 是一条系统提示，我额外说明了如何返回输出。我提高了温度 (temperature) 以增加创意，也指定了更高的词元 (token) 上限。但由于我对如何返回输出的指令很清楚，模型没有返回多余文本。</mark>

| | |
| --- | --- |
| **Goal** | Classify movie reviews as positive, neutral or negative. |
| **Model** | gemini-pro |
| **Temperature** | 1 |
| **Token Limit** | 5 |
| **Top-K** | 40 |
| **Top-P** | 0.8 |

**Prompt**

```text
Classify movie reviews as positive, neutral or negative. Only
return the label in uppercase.
Review: "Her" is a disturbing study revealing the direction
humanity is headed if AI is allowed to keep evolving,
unchecked. It's so disturbing I couldn't watch it.
Sentiment:
```

**Output**

```text
NEGATIVE
```

**Table 3. An example of system prompting**

<mark>表 3：系统提示的一个例子。</mark>

| | |
| --- | --- |
| **<mark>目标</mark>** | <mark>把电影评论分为正面、中性或负面。</mark> |
| **<mark>模型</mark>** | gemini-pro |
| **<mark>温度</mark>** | 1 |
| **<mark>词元上限</mark>** | 5 |
| **Top-K** | 40 |
| **Top-P** | 0.8 |

**<mark>提示</mark>**

<mark>把电影评论分为正面、中性或负面。只返回大写标签。
评论："Her" 是一部令人不安的研究，揭示了如果允许 AI 不受约束地继续演化，人类将走向何方。它太令人不安了，我没法看下去。
情感：</mark>

**<mark>输出</mark>**

```text
NEGATIVE
```

System prompts can be useful for generating output that meets specific requirements. The name ‘system prompt’ actually stands for ‘providing an additional task to the system’. For example, you could use a system prompt to generate a code snippet that is compatible with a specific programming language, or you could use a system prompt to return a certain structure. Have a look into Table 4, where I return the output in JSON format.

<mark>系统提示可以用来生成满足特定要求的输出。「系统提示」这个名字，实际上就是「给系统再加一项任务」。例如，可以用系统提示生成与某种编程语言兼容的代码片段，也可以用系统提示返回某种结构。见表 4，我让输出以 JSON 格式返回。</mark>

| | |
| --- | --- |
| **Goal** | Classify movie reviews as positive, neutral or negative, return JSON. |
| **Model** | gemini-pro |
| **Temperature** | 1 |
| **Token Limit** | 1024 |
| **Top-K** | 40 |
| **Top-P** | 0.8 |

**Prompt**

````text
Classify movie reviews as positive, neutral or negative. Return
valid JSON:
Review: "Her" is a disturbing study revealing the direction
humanity is headed if AI is allowed to keep evolving,
unchecked. It's so disturbing I couldn't watch it.
Schema:
```
MOVIE:
{
"sentiment": String "POSITIVE" | "NEGATIVE" | "NEUTRAL",
"name": String
}
MOVIE REVIEWS:
{
"movie_reviews": [MOVIE]
}
```
JSON Response:
````

**Output**

```json
{
  "movie_reviews": [
    {
      "sentiment": "NEGATIVE",
      "name": "Her"
    }
  ]
}
```

**Table 4. An example of system prompting with JSON format**

<mark>表 4：用 JSON 格式做系统提示的一个例子。</mark>

| | |
| --- | --- |
| **<mark>目标</mark>** | <mark>把电影评论分为正面、中性或负面，并返回 JSON。</mark> |
| **<mark>模型</mark>** | gemini-pro |
| **<mark>温度</mark>** | 1 |
| **<mark>词元上限</mark>** | 1024 |
| **Top-K** | 40 |
| **Top-P** | 0.8 |

**<mark>提示</mark>**

<mark>把电影评论分为正面、中性或负面。返回合法的 JSON。评论："Her" 是一部令人不安的研究，揭示了如果允许 AI 不受约束地继续演化，人类将走向何方。它太令人不安了，我没法看下去。模式与英文提示相同：MOVIE 含 sentiment（POSITIVE、NEGATIVE 或 NEUTRAL）和 name；MOVIE REVIEWS 含 movie_reviews 数组。然后要求 JSON 回答。</mark>

**<mark>输出</mark>**

```json
{
  "movie_reviews": [
    {
      "sentiment": "NEGATIVE",
      "name": "Her"
    }
  ]
}
```

<mark>输出把评论标为 NEGATIVE，电影名是 Her。</mark>

There are some benefits in returning JSON objects from a prompt that extracts data. In a real-world application I don’t need to manually create this JSON format, I can already return the data in a sorted order (very handy when working with datetime objects), but most importantly, by prompting for a JSON format it forces the model to create a structure and limit hallucinations.

<mark>用抽取数据的提示返回 JSON 对象有一些好处。在真实应用里，我不需要手工拼这种 JSON 格式，数据已经可以按排好的顺序返回（处理 datetime 对象时非常方便）。更重要的是，要求 JSON 格式会迫使模型建立结构，并限制幻觉 (hallucination)。</mark>

System prompts can also be really useful for safety and toxicity. To control the output, simply add an additional line to your prompt like: ‘You should be respectful in your answer.’.

<mark>系统提示对安全和有害内容也很有用。要控制输出，只要在提示里再加一行，例如：「你的回答应当保持尊重。」</mark>

---

## Role prompting

<mark>角色提示</mark>

Role prompting is a technique in prompt engineering that involves assigning a specific role to the gen AI model. This can help the model to generate more relevant and informative output, as the model can craft its responses to the specific role that it has been assigned.

<mark>角色提示是提示工程里的一种技巧，给生成式 AI 模型指定一个具体角色。这能帮模型生成更切题、信息更丰富的输出，因为模型可以按被指定的角色来组织回答。</mark>

For example, you could role prompt a gen AI model to be a book editor, a kindergarten teacher, or a motivational speaker. Once the model has been assigned a role, you can then give it prompts that are specific to that role. For example, you could prompt a teacher to create a lesson plan that they can then review. Have a look into Table 5, where the model takes the role of a travel guide.

<mark>例如，你可以让生成式 AI 模型扮演图书编辑、幼儿园老师或励志演讲者。一旦指定了角色，就可以给它与该角色相关的提示。例如，可以让一位老师编写教案，再由他们审阅。见表 5，模型扮演旅行向导。</mark>

| | |
| --- | --- |
| **Goal** | Act as travel guide and provide 3 travel suggestions |
| **Model** | gemini-pro |
| **Temperature** | 1 |
| **Token Limit** | 1024 |
| **Top-K** | 40 |
| **Top-P** | 0.8 |

**Prompt**

```text
I want you to act as a travel guide. I will write to you
about my location and you will suggest 3 places to visit near
me. In some cases, I will also give you the type of places I
will visit.
My suggestion: "I am in Amsterdam and I want to visit
only museums."
Travel Suggestions:
```

**Output**

```text
1. Rijksmuseum: World-renowned museum, known for Dutch masterpieces
like Rembrandt’s “The Night Watch.” Don’t miss the incredible collection of
paintings and artifacts showcasing Dutch art and history.
2. Van Gogh Museum: Immerse yourself in the captivating works of Vincent
van Gogh. The museum houses the largest collection of his paintings and
drawings, including “The Starry Night” and “Sunflowers.”
3. Stedelijk Museum Amsterdam: Discover modern and contemporary art
from around the world. The museum’s collection includes works by Picasso,
Kandinsky, and Rietveld, housed in a striking modern building.
```

**Table 5. An example of role prompting**

<mark>表 5：角色提示的一个例子。</mark>

| | |
| --- | --- |
| **<mark>目标</mark>** | <mark>扮演旅行向导，并给出 3 条旅行建议</mark> |
| **<mark>模型</mark>** | gemini-pro |
| **<mark>温度</mark>** | 1 |
| **<mark>词元上限</mark>** | 1024 |
| **Top-K** | 40 |
| **Top-P** | 0.8 |

**<mark>提示</mark>**

<mark>我要你扮演旅行向导。我会告诉你我所在的位置，你建议我附近 3 个可去的地方。有时我也会告诉你我想去的地方类型。
我的建议："我在阿姆斯特丹，只想参观博物馆。"
旅行建议：</mark>

**<mark>输出</mark>**

<mark>1. 国立博物馆（Rijksmuseum）：世界知名的博物馆，以伦勃朗的《夜巡》等荷兰杰作闻名。不要错过那些展示荷兰艺术与历史的画作和文物。
2. 梵高博物馆（Van Gogh Museum）：沉浸在文森特·梵高迷人的作品里。馆藏有他最大规模的绘画和素描，包括《星月夜》和《向日葵》。
3. 阿姆斯特丹市立博物馆（Stedelijk Museum Amsterdam）：发现来自世界各地的现代与当代艺术。馆藏包括毕加索、康定斯基和里特维尔德的作品，坐落在一座醒目的现代建筑里。</mark>

The above example shows an example of taking the role of a travel agent. When you would change the role to a teacher of geography, you would notice that you will receive a different response.

<mark>上面的例子是扮演旅行代理人。如果把角色改成地理老师，你会发现得到的回答不同。</mark>

Defining a role perspective for an AI model gives it a blueprint of the tone, style, and focused expertise you’re looking for to improve the quality, relevance, and effectiveness of your output.

<mark>给 AI 模型定义一个角色视角，就给了它你想要的语气、风格和专长蓝图，从而提高输出的质量、相关性和有效性。</mark>

Here are some styles you can choose from which I find effective:

<mark>下面是一些我发现有效的风格，可以选用：</mark>

Confrontational, Descriptive, Direct, Formal, Humorous, Influential, Informal, Inspirational, Persuasive

<mark>对抗的、描述的、直接的、正式的、幽默的、有影响力的、非正式的、鼓舞的、有说服力的</mark>

Let’s change our prompt in Table 6 to include a humorous and inspirational style.

<mark>我们把表 6 里的提示改成带幽默和鼓舞的风格。</mark>

**Prompt**

```text
I want you to act as a travel guide. I will write to you about
my location and you will suggest 3 places to visit near me in
a humorous style.
My suggestion: "I am in Manhattan."
Travel Suggestions:
```

**Output**

```text
1. Behold the Empire State of Mind: Ascend to the dizzying heights of the Empire
State Building and bask in the glory of Manhattan's skyline. Prepare to feel like
King Kong atop the Big Apple, minus the giant ape-sized banana.
2. Get Artsy-Fartsy at MoMA: Unleash your inner art aficionado at the Museum
of Modern Art (MoMA). Gaze upon masterpieces that will boggle your
mind and make you question whether your stick-figure drawings have any
artistic merit.
3. Shop ‘Til You Drop on Fifth Avenue: Indulge in some retail therapy on the
iconic Fifth Avenue. Brace yourself for sticker shock as you window-shop (or
actually shop) at designer boutiques that will make your wallet cry. But hey,
you’re in Manhattan, so you might as well embrace the fabulousness!
```

**Table 6. An example of role prompting with a humorous tone and style**

<mark>表 6：带幽默语气和风格的角色提示的一个例子。</mark>

**<mark>提示</mark>**

<mark>我要你扮演旅行向导。我会告诉你我所在的位置，你用幽默的风格建议我附近 3 个可去的地方。
我的建议："我在曼哈顿。"
旅行建议：</mark>

**<mark>输出</mark>**

<mark>1. 一览「帝国之心」：登上帝国大厦令人眩晕的高处，沐浴曼哈顿天际线的荣光。准备好感觉自己像大苹果顶上的金刚，只是没有那根猩猩尺寸的香蕉。
2. 在 MoMA 附庸风雅：在现代艺术博物馆（MoMA）释放你内心的艺术行家。凝视那些让你目瞪口呆的杰作，并开始怀疑自己的火柴人画有没有任何艺术价值。
3. 在第五大道逛到腿软：在标志性的第五大道做一点购物疗法。在设计师精品店里橱窗购物（或真的下单）时，准备好被标价吓一跳，钱包会哭。不过嘿，你人在曼哈顿，不妨拥抱这份浮华！</mark>

---

## Contextual prompting

<mark>上下文提示</mark>

By providing contextual prompts, you can help ensure that your AI interactions are as seamless and efficient as possible. The model will be able to more quickly understand your request and be able to generate more accurate and relevant responses, as you can see in the example of Table 7.

<mark>提供上下文提示，有助于让你和 AI 的交互尽可能顺畅、高效。模型能更快理解你的请求，并生成更准确、更切题的回答，如表 7 的例子。</mark>

| | |
| --- | --- |
| **Goal** | Suggest articles for a blog about retro games |
| **Model** | gemini-pro |
| **Temperature** | 1 |
| **Token Limit** | 1024 |
| **Top-K** | 40 |
| **Top-P** | 0.8 |

**Prompt**

```text
Context: You are writing for a blog about retro 80's arcade
video games.
Suggest 3 topics to write an article about with a few lines of
description of what this article should contain.
```

**Output**

```text
1. The Evolution of Arcade Cabinet Design:
This article would explore the evolution of arcade cabinet designs, from the
early wood and metal cabinets of the 1970s to the sleek, neon-lit designs of
the 1980s and beyond.
2. Blast From The Past: Iconic Arcade Games of The 80’s:
This article would feature a glimpse into the history, impact, and legacy
of some of the most iconic and influential arcade games of the 1980s,
highlighting their innovations, popular mechanics, and enduring charm.
3. The Rise and Retro Revival of Pixel Art:
This article would delve into the evolution of pixel art as a defining visual
style of early arcade games, tracing its roots, exploring its techniques, and
discussing the resurgence of pixel art in modern games and digital art.
```

**Table 7. An example of contextual prompting**

<mark>表 7：上下文提示的一个例子。</mark>

| | |
| --- | --- |
| **<mark>目标</mark>** | <mark>为一份关于复古游戏的博客建议文章选题</mark> |
| **<mark>模型</mark>** | gemini-pro |
| **<mark>温度</mark>** | 1 |
| **<mark>词元上限</mark>** | 1024 |
| **Top-K** | 40 |
| **Top-P** | 0.8 |

**<mark>提示</mark>**

<mark>上下文：你在为一份关于 80 年代复古街机电子游戏的博客写作。
建议 3 个可以写文章的题目，并用几行字说明这篇文章应当包含什么。</mark>

**<mark>输出</mark>**

<mark>1. 街机机柜设计的演变：
这篇文章会探索街机机柜设计的演变，从 1970 年代早期的木头和金属机柜，到 1980 年代及之后光滑、霓虹灯照明的设计。
2. 旧日回响：80 年代的标志性街机游戏：
这篇文章会瞥见 1980 年代一些最标志性、最有影响力的街机游戏的历史、影响和遗产，突出它们的创新、流行机制和持久魅力。
3. 像素艺术的兴起与复古复兴：
这篇文章会深入像素艺术作为早期街机游戏标志性视觉风格的演变，追溯它的根源，探索它的技法，并讨论像素艺术在现代游戏和数字艺术中的回潮。</mark>

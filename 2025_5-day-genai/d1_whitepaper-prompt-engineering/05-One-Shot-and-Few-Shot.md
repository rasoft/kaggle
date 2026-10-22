# One-shot & few-shot

单样本 (one-shot) 与少样本 (few-shot)

When creating prompts for AI models, it is helpful to provide examples. These examples can help the model understand what you are asking for. Examples are especially useful when you want to steer the model to a certain output structure or pattern.

给 AI 模型 (Model) 写提示 (Prompt) 时，提供示例很有帮助。示例能帮模型理解你在要什么。当你想把模型引向某种输出结构或模式时，示例尤其有用。

A one-shot prompt, provides a single example, hence the name one-shot. The idea is the model has an example it can imitate to best complete the task.

单样本提示只提供一个示例，所以叫单样本。想法是：模型有一个可以模仿的例子，从而更好地完成任务。

A few-shot prompt 7 provides multiple examples to the model. This approach shows the model a pattern that it needs to follow. The idea is similar to one-shot, but multiple examples of the desired pattern increases the chance the model follows the pattern.

少样本提示 7 向模型提供多个示例。这种做法向模型展示它需要遵循的模式。想法与单样本类似，但期望模式的多个例子会提高模型遵循该模式的机会。

The number of examples you need for few-shot prompting depends on a few factors, including the complexity of the task, the quality of the examples, and the capabilities of the generative AI (gen AI) model you are using. As a general rule of thumb, you should use at least three to five examples for few-shot prompting. However, you may need to use more examples for more complex tasks, or you may need to use fewer due to the input length limitation of your model.

少样本提示需要多少示例，取决于几件事：任务复杂度、示例质量，以及你所用生成式 AI（gen AI）模型的能力。经验上，少样本提示至少用 3 到 5 个示例。更复杂的任务可能需要更多示例；受模型输入长度限制，有时也只能用更少。

Table 2 shows a few-shot prompt example, let’s use the same gemini-pro model configuration settings as before, other than increasing the token limit to accommodate the need for a longer response.

表 2 是一个少样本提示例子。除了提高词元 (token) 上限以容纳更长的回答，其余沿用之前的 gemini-pro 模型配置。

| | |
| --- | --- |
| **Goal** | Parse pizza orders to JSON |
| **Model** | gemini-pro |
| **Temperature** | 0.1 |
| **Token Limit** | 250 |
| **Top-K** | N/A |
| **Top-P** | 1 |

**Prompt**

````text
Parse a customer's pizza order into valid JSON:

EXAMPLE:
I want a small pizza with cheese, tomato sauce, and pepperoni.
JSON Response:
```
{
"size": "small",
"type": "normal",
"ingredients": [["cheese", "tomato sauce", "peperoni"]]
}
```

EXAMPLE:
Can I get a large pizza with tomato sauce, basil and mozzarella
{
"size": "large",
"type": "normal",
"ingredients": [["tomato sauce", "bazel", "mozzarella"]]
}

Now, I would like a large pizza, with the first half cheese and
mozzarella. And the other tomato sauce, ham and pineapple.
JSON Response:
````

**Output**

```json
{
"size": "large",
"type": "half-half",
"ingredients": [["cheese", "mozzarella"], ["tomato sauce",
"ham", "pineapple"]]
}
```

**Table 2. An example of few-shot prompting**

表 2：少样本提示的一个例子。

| | |
| --- | --- |
| **目标** | 把披萨订单解析成 JSON |
| **模型** | gemini-pro |
| **温度** | 0.1 |
| **词元上限** | 250 |
| **Top-K** | N/A |
| **Top-P** | 1 |

**提示**

把顾客的披萨订单解析成合法的 JSON。示例 1：我想要一份小号披萨，配奶酪、番茄酱和意大利辣香肠。示例 JSON 的拼写按原文保留为 peperoni。示例 2：可以给我一份大号披萨吗，配番茄酱、罗勒和马苏里拉。示例 JSON 的拼写按原文保留为 bazel。现在，我想要一份大号披萨，一半是奶酪和马苏里拉，另一半是番茄酱、火腿和菠萝。

**输出**

```json
{
"size": "large",
"type": "half-half",
"ingredients": [["cheese", "mozzarella"], ["tomato sauce",
"ham", "pineapple"]]
}
```

示例 JSON 里的拼写 peperoni、bazel 按原文保留。模型仍把订单解析成 half-half：一半是奶酪和马苏里拉，另一半是番茄酱、火腿和菠萝。

When you choose examples for your prompt, use examples that are relevant to the task you want to perform. The examples should be diverse, of high quality, and well written. One small mistake can confuse the model and will result in undesired output.

为提示挑选示例时，要用和你要做的任务相关的例子。示例应当多样、质量高、写得好。一个小错误就可能把模型弄糊涂，并导致不想要的输出。

If you are trying to generate output that is robust to a variety of inputs, then it is important to include edge cases in your examples. Edge cases are inputs that are unusual or unexpected, but that the model should still be able to handle.

如果你想让输出对各种各样的输入都稳妥，就应该在示例里放进边界情况。边界情况是不寻常或出乎意料的输入，但模型仍然应该能处理。

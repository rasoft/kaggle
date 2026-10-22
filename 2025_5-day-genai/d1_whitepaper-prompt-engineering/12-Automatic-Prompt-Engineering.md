# Automatic Prompt Engineering

自动提示工程 (Automatic Prompt Engineering, APE)

At this point you might realize that writing a prompt can be complex. Wouldn’t it be nice to automate this (write a prompt to write prompts)? Well, there’s a method: Automatic Prompt Engineering (APE). This method15 not only alleviates the need for human input but also enhances the model’s performance in various tasks.

到这里你可能已经意识到，写提示 (Prompt) 可能很复杂。要是能把它自动化（写一条提示去写提示）岂不很好？有一种方法：自动提示工程。这种方法 15 不仅减轻对人工输入的需要，还能在各种任务上提升模型 (Model) 的表现。

You will prompt a model to generate more prompts. Evaluate them, possibly alter the good ones. And repeat.

你提示模型去生成更多提示。评估它们，也许再改一改好的那些。然后重复。

For example, you can use automatic prompt engineering that will help with training a chatbot for a merchandise t-shirt webshop. We want to figure out all the various ways customers could phrase their order for buying a band merchandise t-shirt.

例如，可以用自动提示工程来帮助训练一个乐队周边 T 恤网店的聊天机器人。我们想弄清顾客购买乐队周边 T 恤时，可能用哪些不同说法下单。

1. Write the prompt which will generate the output variants. In this example, I am using gemini-pro to generate 10 instructions. See Table 15:

写出那条用来生成输出变体的提示。在这个例子里，我用 gemini-pro 生成 10 条指令。见表 15：

**Prompt**

```text
We have a band merchandise t-shirt webshop, and to train a
chatbot we need various ways to order: "One Metallica t-shirt
size S". Generate 10 variants, with the same semantics but keep
the same meaning.
```

**Output**

```text
1. I’d like to purchase a Metallica t-shirt in size small.
2. Can I order a small-sized Metallica t-shirt?
3. I’d like to buy one Metallica t-shirt in small.
4. One Metallica shirt, size small, please.
5. I want one Metallica t-shirt in size small.
6. I’d like to place an order for one Metallica t-shirt in small.
7. Small Metallica t-shirt, one please.
8. I’m looking for one Metallica t-shirt in small.
9. Can you get me one Metallica t-shirt in small?
10. One Metallica small t-shirt, please.
```

**Table 15. Use an LLM to generate prompts**

表 15：用大语言模型 (LLM) 生成提示。

**提示**

我们有一家乐队周边 T 恤网店。为了训练聊天机器人，我们需要「一件 Metallica T 恤，S 码」的各种下单说法。生成 10 个变体，语义相同，意思保持不变。

**输出**

1. 我想买一件小号的 Metallica T 恤。
2. 我可以订一件小号 Metallica T 恤吗？
3. 我想买一件小号的 Metallica T 恤。
4. 一件 Metallica 衬衫，小号，谢谢。
5. 我要一件小号的 Metallica T 恤。
6. 我想下一单，一件小号的 Metallica T 恤。
7. 小号 Metallica T 恤，来一件。
8. 我在找一件小号的 Metallica T 恤。
9. 能给我一件小号的 Metallica T 恤吗？
10. 一件 Metallica 小号 T 恤，谢谢。

2. Evaluate all of the instruction candidates by scoring the candidates based on a chosen metric, For example, you can use. BLEU (Bilingual Evaluation Understudy) or ROUGE (Recall-Oriented Understudy for Gisting Evaluation).

按选定的指标给所有指令候选打分，从而评估它们。例如可以用 BLEU（Bilingual Evaluation Understudy，双语评估替身）或 ROUGE（Recall-Oriented Understudy for Gisting Evaluation，面向召回的摘要评估替身）。

3. Select the instruction candidate with the highest evaluation score. This candidate will be the final prompt you can use in your software application or chatbot. You can also tweak the select prompt and evaluate again.

选出评估分数最高的指令候选。这个候选就是你可以放进软件应用或聊天机器人的最终提示。你也可以再改一改选中的提示，然后重新评估。

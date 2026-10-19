# Chain of Thought (CoT)

<mark>思维链 (Chain of Thought, CoT)</mark>

Chain of Thought (CoT) 9 prompting is a technique for improving the reasoning capabilities of LLMs by generating intermediate reasoning steps. This helps the LLM generate more accurate answers. You can combine it with few-shot prompting to get better results on more complex tasks that require reasoning before responding as it’s a challenge with a zero-shot chain of thought.

<mark>思维链提示 9 通过生成中间推理步骤，来提升大语言模型 (LLM) 的推理 (Reasoning) 能力。这帮助大语言模型生成更准确的答案。你可以把它和少样本 (few-shot) 提示 (Prompt) 结合起来，在需要先推理再回答的更复杂任务上得到更好的结果，因为零样本 (zero-shot) 思维链本身就比较难。</mark>

CoT has a lot of advantages. First of all, it’s low-effort while being very effective and works well with off-the-shelf LLMs (so no need to finetune). You also get interpretability with CoT prompting, as you can learn from the LLM’s responses and see the reasoning steps that were followed. If there’s a malfunction, you will be able to identify it. Chain of thought appears to improve robustness when moving between different LLM versions. Which means the performance of your prompt should drift less between different LLMs than if your prompt does not use reasoning chains. Of course there are also disadvantages, but they are somewhat intuitive.

<mark>思维链有很多优点。首先，它费力不多却很有效，而且对现成的大语言模型就好用（所以不必微调，fine-tune）。思维链提示还带来可解释性：你可以从大语言模型的回答里学习，并看到它遵循的推理步骤。如果出了故障，你能指出来。在不同大语言模型版本之间迁移时，思维链似乎能提高稳健性。也就是说，和不用推理链的提示相比，你的提示在不同大语言模型之间的表现漂移应该更小。当然也有缺点，但那些缺点多少是直观的。</mark>

The LLM response includes the chain of thought reasoning, which means more output tokens, which means predictions cost more money and take longer.

<mark>大语言模型的回答包含思维链推理，这意味着更多输出词元 (token)，意味着预测更花钱，也更慢。</mark>

To explain the following example in Table 11, let’s first try to create a prompt that is not using CoT prompting to showcase the flaws of a large language model.

<mark>为了说明表 11 里的例子，我们先写一条不用思维链提示的提示，来展示大语言模型的缺陷。</mark>

**Prompt**

```text
When I was 3 years old, my partner was 3 times my age. Now, I
am 20 years old. How old is my partner?
```

**Output**

```text
63 years old
```

**Table 11. An example of a prompt which is trying to solve a mathematical problem**

<mark>表 11：一条试图解决数学问题的提示。</mark>

**<mark>提示</mark>**

<mark>我 3 岁时，我的伴侣是我年龄的 3 倍。现在我 20 岁。我的伴侣多大？</mark>

**<mark>输出</mark>**

<mark>63 岁</mark>

Yikes. That’s obviously the wrong answer. As a matter of fact, LLMs often struggle with mathematical tasks and can provide incorrect answers – even for a task as simple as multiplying two numbers. This is because they are trained on large volumes of text and math may require a different approach. So let’s see if intermediate reasoning steps will improve the output.

<mark>哎呀。这显然是错的。事实上，大语言模型经常在数学任务上吃力，甚至连两数相乘这么简单的任务也会给错答案。这是因为它们在大量文本上训练，而数学可能需要另一种做法。所以我们看看中间推理步骤能不能改善输出。</mark>

**Prompt**

```text
When I was 3 years old, my partner was 3 times my age. Now,
I am 20 years old. How old is my partner? Let's think step
by step.
```

**Output**

```text
1. Let’s assume my current age is “x” years.
2. When I was 3 years old, my age was 3 years.
3. My partner’s age at that time was 3 times my age, which means my partner’s
age was 3 * 3 = 9 years.
4. Now, I am 20 years old, which means my age has increased by 20 - 3 = 17
years since I was 3 years old.
5. Since my partner’s age was 9 years when I was 3 years old, and my age has
increased by 17 years, my partner’s age must have also increased by 17 years.
6. Therefore, my partner’s current age is 9 + 17 = 26 years.
So, my partner is 26 years old.
```

**Table 12. An example of Chain of Thought prompting**

<mark>表 12：思维链提示的一个例子。</mark>

**<mark>提示</mark>**

<mark>我 3 岁时，我的伴侣是我年龄的 3 倍。现在我 20 岁。我的伴侣多大？让我们一步一步想。</mark>

**<mark>输出</mark>**

<mark>1. 假设我现在的年龄是 “x” 岁。
2. 我 3 岁时，我的年龄是 3 岁。
3. 那时我伴侣的年龄是我的 3 倍，也就是 3 * 3 = 9 岁。
4. 现在我 20 岁，也就是从 3 岁起增加了 20 - 3 = 17 岁。
5. 我 3 岁时伴侣是 9 岁，而我的年龄增加了 17 岁，伴侣的年龄也一定增加了 17 岁。
6. 因此，伴侣现在的年龄是 9 + 17 = 26 岁。
所以，我的伴侣 26 岁。</mark>

Alright, now the final answer is correct. That’s because we clearly instructed the LLM to explain each step instead of just returning an answer. It’s interesting to see that the model adds up the 17 increased years. In my head I would take the difference of years between my partner and me and add those up. (20+(9-3)). Let’s help the model to think a little bit more like me.

<mark>好，现在最终答案是对的。这是因为我们清楚地指示大语言模型解释每一步，而不是只返回一个答案。有意思的是，模型把增加的 17 年加了上去。我自己会先算我和伴侣的年龄差，再把差加上去。（20+(9-3)）。我们帮模型想得更像我一点。</mark>

Table 12 is an example of ‘zero-shot’ Chain of thought. Chain of thought prompting can be very powerful when combined with a single-shot or few-shot, as what you can see in Table 13:

<mark>表 12 是「零样本」思维链的例子。思维链提示和单样本 (one-shot) 或少样本结合时可以非常有力，如表 13：</mark>

**Prompt**

```text
Q: When my brother was 2 years old, I was double his age. Now
I am 40 years old. How old is my brother? Let's think step
by step.
A: When my brother was 2 years, I was 2 * 2 = 4 years old.
That's an age difference of 2 years and I am older. Now I am 40
years old, so my brother is 40 - 2 = 38 years old. The answer
is 38.
Q: When I was 3 years old, my partner was 3 times my age. Now,
I am 20 years old. How old is my partner? Let's think step
by step.
A:
```

**Output**

```text
When I was 3 years old, my partner was 3 * 3 = 9 years old. That’s an age
difference of 6 years and my partner is older. Now I am 20 years old, so my
partner is 20 + 6 = 26 years old. The answer is 26.
```

**Table 13. An example of chain of thought prompting with a single-shot**

<mark>表 13：带单样本的思维链提示的一个例子。</mark>

**<mark>提示</mark>**

<mark>问：我弟弟 2 岁时，我的年龄是他的两倍。现在我 40 岁。我弟弟多大？让我们一步一步想。
答：弟弟 2 岁时，我是 2 * 2 = 4 岁。年龄差是 2 岁，我更大。现在我 40 岁，所以弟弟是 40 - 2 = 38 岁。答案是 38。
问：我 3 岁时，我的伴侣是我年龄的 3 倍。现在我 20 岁。我的伴侣多大？让我们一步一步想。
答：</mark>

**<mark>输出</mark>**

<mark>我 3 岁时，伴侣是 3 * 3 = 9 岁。年龄差是 6 岁，伴侣更大。现在我 20 岁，所以伴侣是 20 + 6 = 26 岁。答案是 26。</mark>

Chain of thought can be useful for various use-cases. Think of code generation, for breaking down the request into a few steps, and mapping those to specific lines of code. Or for creating synthetic data when you have some kind of seed like “The product is called XYZ, write a description guiding the model through the assumptions you would make based on the product given title.” Generally, any task that can be solved by ‘talking through is a good candidate for a chain of thought. If you can explain the steps to solve the problem, try chain of thought.

<mark>思维链可以用于多种场景。例如代码生成：把请求拆成几步，再映射到具体代码行。或者在你有某种种子时制造合成数据，例如「产品叫 XYZ，写一段描述，引导模型根据给定的产品名称说出你会做的假设。」一般来说，凡是能靠「把步骤讲出来」解决的任务，都适合思维链。如果你能讲清解题步骤，就试试思维链。</mark>

Please refer to the notebook10 hosted in the GoogleCloudPlatform Github repository which will go into further detail on CoT prompting.

<mark>请参考托管在 GoogleCloudPlatform Github 仓库里的 notebook，10 它会更详细地讲思维链提示。</mark>

In the best practices section of this chapter, we will learn some best practices specific to Chain of thought prompting.

<mark>在本章的最佳实践一节，我们会学习一些专门针对思维链提示的最佳实践。</mark>

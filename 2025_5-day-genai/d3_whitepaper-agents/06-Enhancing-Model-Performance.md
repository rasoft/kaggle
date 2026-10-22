# Enhancing model performance with targeted learning

用针对性学习提升模型表现

A crucial aspect of using models effectively is their ability to choose the right tools when generating output, especially when using tools at scale in production. While general training helps models develop this skill, real-world scenarios often require knowledge beyond the training data. Imagine this as the difference between basic cooking skills and mastering a specific cuisine. Both require foundational cooking knowledge, but the latter demands targeted learning for more nuanced results.

有效使用模型 (Model) 的一个关键方面，是它们在生成输出时选对工具 (Tools) 的能力，尤其是在生产环境里大规模使用工具时。一般训练能帮助模型培养这项技能，但现实场景常常需要训练数据之外的知识。可以把这想成基本厨艺和精通某一种菜系之间的差别。两者都需要烹饪的基础知识，但后者要靠针对性学习，才能得到更细腻的结果。

To help the model gain access to this type of specific knowledge, several approaches exist:

要让模型获得这类专门知识，有几种做法：

- **In-context learning:** This method provides a generalized model with a prompt, tools, and few-shot examples at inference time which allows it to learn ‘on the fly' how and when to use those tools for a specific task. The ReAct framework is an example of this approach in natural language.
- **Retrieval-based in-context learning:** This technique dynamically populates the model prompt with the most relevant information, tools, and associated examples by retrieving them from external memory. An example of this would be the ‘Example Store’ in Vertex AI extensions or the data stores RAG based architecture mentioned previously.
- **Fine-tuning based learning:** This method involves training a model using a larger dataset of specific examples prior to inference. This helps the model understand when and how to apply certain tools prior to receiving any user queries.

- **上下文学习 (In-context Learning)：** 这种方法在推断时给一个通用模型提供提示、工具和少样本示例，让它「当场」学会为某项具体任务如何使用、何时使用这些工具。ReAct 框架就是这种方法在自然语言里的一个例子。

- **基于检索的上下文学习 (Retrieval-based In-context Learning)：** 这种技术从外部记忆中检索最相关的信息、工具和配套示例，动态地填进模型提示。例子包括 Vertex AI 扩展里的「示例存储 (Example Store)」，以及前面提到的基于数据存储 (Data Store) 的检索增强生成 (RAG) 架构。

- **基于微调的学习 (Fine-tuning Based Learning)：** 这种方法在推断之前，用一组更大的具体示例数据集来训练模型。这帮助模型在收到任何用户查询之前，就理解何时以及如何应用某些工具。

To provide additional insights on each of the targeted learning approaches, let’s revisit our cooking analogy.

为了把这几种针对性学习讲得更清楚，我们回到烹饪的比喻。

- Imagine a chef has received a specific recipe (the prompt), a few key ingredients (relevant tools) and some example dishes (few-shot examples) from a customer. Based on this limited information and the chef’s general knowledge of cooking, they will need to figure out how to prepare the dish ‘on the fly’ that most closely aligns with the recipe and the customer’s preferences. This is in-context learning.
- Now let’s imagine our chef in a kitchen that has a well-stocked pantry (external data stores) filled with various ingredients and cookbooks (examples and tools). The chef is now able to dynamically choose ingredients and cookbooks from the pantry and better align to the customer’s recipe and preferences. This allows the chef to create a more informed and refined dish leveraging both existing and new knowledge. This is retrieval-based in-context learning.
- Finally, let’s imagine that we sent our chef back to school to learn a new cuisine or set of cuisines (pre-training on a larger dataset of specific examples). This allows the chef to approach future unseen customer recipes with deeper understanding. This approach is perfect if we want the chef to excel in specific cuisines (knowledge domains). This is fine-tuning based learning.

- 想象一位厨师从客人那里拿到一份具体食谱（提示）、几样关键食材（相关工具）和几道示例菜（少样本示例）。凭这些有限的信息，加上厨师对烹饪的一般知识，他们得「当场」想出怎么做这道菜，才能最贴近食谱和客人的偏好。这就是上下文学习。

- 再想象这位厨师待在一间储藏充足的厨房里（外部数据存储），里面有各种食材和食谱书（示例和工具）。厨师现在可以从储藏室里动态挑选食材和食谱书，更好地对齐客人的食谱和偏好。这样，厨师就能同时利用已有知识和新知识，做出更有依据、更讲究的菜。这就是基于检索的上下文学习。

- 最后，想象我们把厨师送回学校，去学一种或几种新菜系（在一组更大的具体示例数据集上做预训练）。这让厨师以后面对没见过的客人食谱时，能有更深的理解。如果我们希望厨师在特定菜系（知识领域）里出色，这种做法就很合适。这就是基于微调的学习。

Each of these approaches offers unique advantages and disadvantages in terms of speed, cost, and latency. However, by combining these techniques in an agent framework, we can leverage the various strengths and minimize their weaknesses, allowing for a more robust and adaptable solution.

这几种做法在速度、成本和延迟上各有长短。不过，把这些技术放进一个智能体 (Agent) 框架里组合起来，就能用上各自的长处、压低各自的短处，得到更稳健、更能适应的方案。

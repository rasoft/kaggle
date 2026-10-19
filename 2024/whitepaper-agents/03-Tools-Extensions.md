# Tools: Our keys to the outside world

<mark>工具：通往外部世界的钥匙</mark>

While language models excel at processing information, they lack the ability to directly perceive and influence the real world. This limits their usefulness in situations requiring interaction with external systems or data. This means that, in a sense, a language model is only as good as what it has learned from its training data. But regardless of how much data we throw at a model, they still lack the fundamental ability to interact with the outside world. So how can we empower our models to have real-time, context-aware interaction with external systems? Functions, Extensions, Data Stores and Plugins are all ways to provide this critical capability to the model.

<mark>语言模型 (Language Model) 擅长处理信息，却不能直接感知和影响现实世界。这限制了它们在需要与外部系统或数据交互的场合里的用处。某种意义上，语言模型的好坏，只取决于它从训练数据里学到了什么。但无论往模型里投多少数据，它们仍然缺少与外部世界交互的基本能力。那么，怎样让模型与外部系统进行实时的、懂上下文的交互？函数 (Functions)、扩展 (Extensions)、数据存储 (Data Stores) 和插件 (Plugins)，都是把这项关键能力交给模型的方式。</mark>

While they go by many names, tools are what create a link between our foundational models and the outside world. This link to external systems and data allows our agent to perform a wider variety of tasks and do so with more accuracy and reliability. For instance, tools can enable agents to adjust smart home settings, update calendars, fetch user information from a database, or send emails based on a specific set of instructions.

<mark>它们的名字很多，但工具 (Tools) 才是基础模型 (foundational model) 与外部世界之间的连接。这条通往外部系统和数据的连接，让智能体 (Agent) 能做更多种类的任务，而且做得更准确、更可靠。例如，工具可以让智能体调整智能家居设置、更新日历、从数据库取出用户信息，或按一组具体指令发送邮件。</mark>

As of the date of this publication, there are three primary tool types that Google models are able to interact with: Extensions, Functions, and Data Stores. By equipping agents with tools, we unlock a vast potential for them to not only understand the world but also act upon it, opening doors to a myriad of new applications and possibilities.

<mark>截至本文出版之日，Google 模型能够交互的主要工具类型有三种：扩展、函数和数据存储。给智能体配备工具，就打开了一大片潜力：它们不仅能理解世界，还能对世界采取行动，通向大量新的应用和可能。</mark>

---

## Extensions

<mark>扩展</mark>

The easiest way to understand Extensions is to think of them as bridging the gap between an API and an agent in a standardized way, allowing agents to seamlessly execute APIs regardless of their underlying implementation. Let’s say that you’ve built an agent with a goal of helping users book flights. You know that you want to use the Google Flights API to retrieve flight information, but you’re not sure how you’re going to get your agent to make calls to this API endpoint.

<mark>理解扩展最简单的方式，是把它看成以标准化方式弥合 API 与智能体之间的缺口，让智能体无论底层实现如何，都能顺畅地执行 API。假设你做了一个智能体，目标是帮用户订机票。你知道要用 Google Flights API 来取航班信息，但还不确定怎样让智能体去调用这个 API 端点。</mark>

![How agents interact with external APIs](image_003_page_13.png)

<mark>图 3：智能体如何与外部 API 交互？智能体与 Google Flights API 之间还隔着一个问号。</mark>

One approach could be to implement custom code that would take the incoming user query, parse the query for relevant information, then make the API call. For example, in a flight booking use case a user might state “I want to book a flight from Austin to Zurich.” In this scenario, our custom code solution would need to extract “Austin” and “Zurich” as relevant entities from the user query before attempting to make the API call. But what happens if the user says “I want to book a flight to Zurich” and never provides a departure city? The API call would fail without the required data and more code would need to be implemented in order to catch edge and corner cases like this. This approach is not scalable and could easily break in any scenario that falls outside of the implemented custom code.

<mark>一种做法是写自定义代码：接收用户查询，从中解析出相关信息，再发起 API 调用。例如在订机票场景里，用户可能会说「I want to book a flight from Austin to Zurich.」（我想订一张从奥斯汀到苏黎世的机票。）此时，自定义代码必须先从查询里抽出「Austin」和「Zurich」这两个相关实体，才能尝试调用 API。但如果用户说「I want to book a flight to Zurich」（我想订一张去苏黎世的机票），却始终没有给出出发城市呢？缺少必要数据，API 调用就会失败，还得再写更多代码去接住这类边界和角落情况。这种做法无法扩展，一旦场景落到已实现的自定义代码之外，就很容易坏掉。</mark>

A more resilient approach would be to use an Extension. An Extension bridges the gap between an agent and an API by:

<mark>更稳妥的做法是使用扩展。扩展从两方面弥合智能体与 API 之间的缺口：</mark>

1. Teaching the agent how to use the API endpoint using examples.
2. Teaching the agent what arguments or parameters are needed to successfully call the API endpoint.

<mark>1. 用示例教智能体如何使用这个 API 端点。</mark>

<mark>2. 教智能体成功调用这个 API 端点需要哪些参数。</mark>

![Extensions connect agents to external APIs](image_004_page_14.png)

<mark>图 4：扩展把智能体连接到外部 API。扩展居中，一边连智能体，一边连 Google Flights API。示例说明 get_flights 可以取最新航班、用户要搜航班时应调用它，以及它的输入参数。</mark>

Extensions can be crafted independently of the agent, but should be provided as part of the agent’s configuration. The agent uses the model and examples at run time to decide which Extension, if any, would be suitable for solving the user’s query. This highlights a key strength of Extensions, their built-in example types, that allow the agent to dynamically select the most appropriate Extension for the task.

<mark>扩展可以独立于智能体来制作，但应当作为智能体配置的一部分提供。运行时，智能体利用模型和示例来决定哪一个扩展（如果有的话）适合解决用户的查询。这突出了扩展的一项关键优势：内置的示例类型，使智能体能动态选出最适合该任务的扩展。</mark>

![One-to-many relationship between agents, extensions, and APIs](2024/whitepaper-agents/images/image_005_page_14.png)

<mark>图 5：智能体、扩展与 API 之间的一对多关系。智能体包含推理循环和模型，经工具分别连到 Flights、Maps、Weather 三个扩展，再各自连到对应的 API。</mark>

Think of this the same way that a software developer decides which API endpoints to use while solving and solutioning for a user’s problem. If the user wants to book a flight, the developer might use the Google Flights API. If the user wants to know where the nearest coffee shop is relative to their location, the developer might use the Google Maps API. In this same way, the agent / model stack uses a set of known Extensions to decide which one will be the best fit for the user’s query. If you’d like to see Extensions in action, you can try them out on the Gemini application by going to Settings > Extensions and then enabling any you would like to test. For example, you could enable the Google Flights extension then ask Gemini “Show me flights from Austin to Zurich leaving next Friday.”

<mark>这和软件开发者在为用户问题求解、设计方案时决定用哪个 API 端点是一样的。用户想订机票，开发者可能会用 Google Flights API。用户想知道离自己最近的咖啡馆在哪，开发者可能会用 Google Maps API。同样，智能体 / 模型这一层会用一组已知扩展，决定哪一个最适合用户的查询。如果想看扩展实际怎么工作，可以在 Gemini 应用里打开 Settings > Extensions，启用想试的扩展。例如，启用 Google Flights 扩展，然后问 Gemini：「Show me flights from Austin to Zurich leaving next Friday.」（给我看下周五从奥斯汀飞往苏黎世的航班。）</mark>

---

## Sample Extensions

<mark>扩展示例</mark>

To simplify the usage of Extensions, Google provides some out of the box extensions that can be quickly imported into your project and used with minimal configurations. For example, the Code Interpreter extension in Snippet 1 allows you to generate and run Python code from a natural language description.

<mark>为了简化扩展的使用，Google 提供了一些开箱即用的扩展，可以快速导入项目，只需很少的配置就能用。例如，片段 1 里的代码解释器 (Code Interpreter) 扩展，能根据自然语言描述生成并运行 Python 代码。</mark>

```python
import vertexai
import pprint

PROJECT_ID = "YOUR_PROJECT_ID"
REGION = "us-central1"
vertexai.init(project=PROJECT_ID, location=REGION)

from vertexai.preview.extensions import Extension

extension_code_interpreter = Extension.from_hub("code_interpreter")
CODE_QUERY = """Write a python method to invert a binary tree in O(n) time."""

response = extension_code_interpreter.execute(
    operation_id="generate_and_execute",
    operation_params={"query": CODE_QUERY}
)

print("Generated Code:")
pprint.pprint({response['generated_code']})
# The above snippet will generate the following code.
```

```text
Generated Code:
class TreeNode:
  def __init__(self, val=0, left=None, right=None):
    self.val = val
    self.left = left
    self.right = right

def invert_binary_tree(root):
    """
    Inverts a binary tree.
    Args:
        root: The root of the binary tree.
    Returns:
        The root of the inverted binary tree.
    """
    if not root:
        return None
    # Swap the left and right children recursively
    root.left, root.right = invert_binary_tree(root.right), invert_binary_tree(root.left)
    return root

# Example usage:
# Construct a sample binary tree
root = TreeNode(4)
root.left = TreeNode(2)
root.right = TreeNode(7)
root.left.left = TreeNode(1)
root.left.right = TreeNode(3)
root.right.left = TreeNode(6)
root.right.right = TreeNode(9)

# Invert the binary tree
inverted_root = invert_binary_tree(root)
```

**Snippet 1. Code Interpreter Extension can generate and run Python code**

<mark>片段 1：代码解释器扩展可以生成并运行 Python 代码。原文这一段代码跨第 16–17 页。</mark>

To summarize, Extensions provide a way for agents to perceive, interact, and influence the outside world in a myriad of ways. The selection and invocation of these Extensions is guided by the use of Examples, all of which are defined as part of the Extension configuration.

<mark>总结一下：扩展为智能体提供了一种以多种方式感知、交互并影响外部世界的途径。选择并调用这些扩展，靠的是示例 (Examples)；这些示例都定义在扩展配置里。</mark>

# ReAct (reason & act)

<mark>推理与行动 (Reason and Act, ReAct)</mark>

Reason and act (ReAct) [10]13 prompting is a paradigm for enabling LLMs to solve complex tasks using natural language reasoning combined with external tools (search, code interpreter etc.) allowing the LLM to perform certain actions, such as interacting with external APIs to retrieve information which is a first step towards agent modeling.

<mark>推理与行动（ReAct）[10]13 提示 (Prompt) 是一种范式，让大语言模型 (LLM) 用自然语言推理 (Reasoning)，再结合外部工具 (Tools)（搜索、代码解释器等），去解决复杂任务。大语言模型从而可以执行某些动作，例如与外部 API 交互以检索信息。这是走向智能体 (Agent) 建模的第一步。</mark>

ReAct mimics how humans operate in the real world, as we reason verbally and can take actions to gain information. ReAct performs well against other prompt engineering approaches in a variety of domains.

<mark>推理与行动模仿人类在真实世界里的做法：我们用语言推理，也能采取行动来获取信息。在多个领域里，推理与行动相对其他提示工程 (Prompt Engineering) 方法表现良好。</mark>

ReAct prompting works by combining reasoning and acting into a thought-action loop. The LLM first reasons about the problem and generates a plan of action. It then performs the actions in the plan and observes the results. The LLM then uses the observations to update its reasoning and generate a new plan of action. This process continues until the LLM reaches a solution to the problem.

<mark>推理与行动提示把推理和行动合成一个「思考—行动」循环。大语言模型先对问题推理，并生成一个行动计划。然后它执行计划中的行动，并观察结果。大语言模型再用观察结果更新推理，生成新的行动计划。这个过程持续到大语言模型得出问题的解。</mark>

To see this in action, you need to write some code. In code Snippet 1 I am using the langchain framework for Python, together with VertexAI (google-cloud-aiplatform) and the google-search-results pip packages.

<mark>要看到它实际运行，需要写一些代码。在代码片段 1 里，我使用 Python 的 langchain 框架，以及 VertexAI（google-cloud-aiplatform）和 google-search-results 这两个 pip 包。</mark>

To run this sample you must create a (free) SerpAPI key from https://serpapi.com/manage-api-key and set an environment variable SERPAPI_API_KEY.

<mark>要运行这个示例，你必须在 https://serpapi.com/manage-api-key 创建一个（免费的）SerpAPI 密钥，并设置环境变量 SERPAPI_API_KEY。</mark>

Next let’s write some Python code, with the task for the LLM to figure out: How many children have a famous dad that performs in the band Metallica.

<mark>接下来写一些 Python 代码，任务是让大语言模型弄清：Metallica 乐队里那些有名的爸爸一共有多少个孩子。</mark>

```python
from langchain.agents import load_tools
from langchain.agents import initialize_agent
from langchain.agents import AgentType
from langchain.llms import VertexAI

prompt = "How many kids do the band members of Metallica have?"
llm = VertexAI(temperature=0.1)
tools = load_tools(["serpapi"], llm=llm)
agent = initialize_agent(
    tools,
    llm,
    agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True,
)
agent.run(prompt)
```

**Snippet 1. Creating a ReAct Agent with LangChain and VertexAI**

<mark>片段 1：用 LangChain 和 VertexAI 创建一个推理与行动智能体。</mark>

Code Snippet 2 shows the result. Notice that ReAct makes a chain of five searches. In fact, the LLM is scraping Google search results to figure out the band names. Then, it lists the results as observations and chains the thought for the next search.

<mark>代码片段 2 给出结果。注意推理与行动做了一连串五次搜索。实际上，大语言模型在抓取 Google 搜索结果来弄清乐队成员的名字。然后它把结果列为观察，并把思考链接到下一次搜索。</mark>

```text
> Entering new AgentExecutor chain...
Metallica has 4 members.
Action: Search
Action Input: How many kids does James Hetfield have?
Observation: three children
Thought: 1/4 Metallica band members have 3 children
Action: Search
Action Input: How many kids does Lars Ulrich have?
Observation: 3
Thought: 2/4 Metallica band members have 6 children
Action: Search
Action Input: How many kids does Kirk Hammett have?
Observation: Hammett has been married to his second wife Lani since 1998.
They have two sons, Angel (b. September 29, 2006) and Vincenzo (b. June
28, 2008).
Thought: 3/4 Metallica band members have 8 children
Action: Search
Action Input: How many kids does Robert Trujillo have?
Observation: 2
Thought: 4/4 Metallica band members have 10 children
Final Answer: 10
```

**Snippet 2. Executing ReAct Agent in the terminal**

<mark>片段 2：在终端里执行推理与行动智能体。乐队有 4 名成员。依次查到 James Hetfield 有 3 个孩子、Lars Ulrich 有 3 个、Kirk Hammett 有 2 个儿子（Angel 与 Vincenzo）、Robert Trujillo 有 2 个，合计 10。</mark>

Code Snippet 2 figures out that the band Metallica has four band members. Then it searches each band member to request the total of children and add up the total. Finally, it returns the total number of children as the final answer.

<mark>代码片段 2 弄清 Metallica 有四名成员。然后它搜索每一名成员，询问孩子总数并累加。最后把孩子总数作为最终答案返回。</mark>

ReAct prompting in practice requires understanding that you continually have to resend the previous prompts/responses (and do trimming of the extra generated content) as well as set up the model with appropriate examples/instructions. Please refer to the notebook14 hosted in the GoogleCloudPlatform Github repository, which goes into a bit more detail showing the actual LLM inputs and outputs with a more elaborate example.

<mark>实际使用推理与行动提示时要理解：你必须不断重发先前的提示 / 回答（并修剪多余的生成内容），还要用合适的示例 / 指令把模型设置好。请参考托管在 GoogleCloudPlatform Github 仓库里的 notebook，14 它用一个更完整的例子，更详细地展示实际的大语言模型输入和输出。</mark>

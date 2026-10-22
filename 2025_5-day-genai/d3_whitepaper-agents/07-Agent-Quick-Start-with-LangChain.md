# Agent quick start with LangChain

用 LangChain 快速上手智能体

In order to provide a real-world executable example of an agent in action, we’ll build a quick prototype with the LangChain and LangGraph libraries. These popular open source libraries allow users to build customer agents by “chaining” together sequences of logic, reasoning, and tool calls to answer a user’s query. We’ll use our gemini-1.5-flash-001 model and some simple tools to answer a multi-stage query from the user as seen in Snippet 8.

为了给出一个可以实际运行的智能体 (Agent) 例子，我们用 LangChain 和 LangGraph 库搭一个快速原型。这两个流行的开源库让用户可以把逻辑、推理 (Reasoning) 和工具调用的序列「链接」起来，回答用户的查询，从而构建定制智能体。我们会用 gemini-1.5-flash-001 模型 (Model) 和几个简单工具 (Tools)，回答用户的一个多阶段查询，如片段 8 所示。

The tools we are using are the SerpAPI (for Google Search) and the Google Places API. After executing our program in Snippet 8, you can see the sample output in Snippet 9.

这里用的工具是 SerpAPI（用于 Google 搜索）和 Google Places API。执行片段 8 里的程序之后，可以在片段 9 里看到示例输出。

```python
from langgraph.prebuilt import create_react_agent
from langchain_core.tools import tool
from langchain_community.utilities import SerpAPIWrapper
from langchain_community.tools import GooglePlacesTool

os.environ["SERPAPI_API_KEY"] = "XXXXX"
os.environ["GPLACES_API_KEY"] = "XXXXX"

@tool
def search(query: str):
    """Use the SerpAPI to run a Google Search."""
    search = SerpAPIWrapper()
    return search.run(query)

@tool
def places(query: str):
    """Use the Google Places API to run a Google Places Query."""
    places = GooglePlacesTool()
    return places.run(query)

model = ChatVertexAI(model="gemini-1.5-flash-001")
tools = [search, places]
query = "Who did the Texas Longhorns play in football last week? What is the address of the other team's stadium?"
agent = create_react_agent(model, tools)
input = {"messages": [("human", query)]}
for s in agent.stream(input, stream_mode="values"):
    message = s["messages"][-1]
    if isinstance(message, tuple):
        print(message)
    else:
        message.pretty_print()
```

**Snippet 8. Sample LangChain and LangGraph based agent with tools**

片段 8：带工具的 LangChain 与 LangGraph 智能体示例。

```text
=============================== Human Message ================================
Who did the Texas Longhorns play in football last week? What is the address
of the other team's stadium?
================================= Ai Message =================================
Tool Calls: search
Args:
    query: Texas Longhorns football schedule
================================ Tool Message ================================
Name: search
{...Results: "NCAA Division I Football, Georgia, Date..."}
================================= Ai Message =================================
The Texas Longhorns played the Georgia Bulldogs last week.
Tool Calls: places
Args:
    query: Georgia Bulldogs stadium
================================ Tool Message ================================
Name: places
{...Sanford Stadium Address: 100 Sanford...}
================================= Ai Message =================================
The address of the Georgia Bulldogs stadium is 100 Sanford Dr, Athens, GA
30602, USA.
```

**Snippet 9. Output from our program in Snippet 8**

片段 9：片段 8 中程序的输出。模型先用 search 查到德州长角牛上周对阵乔治亚斗牛犬，再用 places 查到球场地址：100 Sanford Dr, Athens, GA 30602, USA。

While this is a fairly simple agent example, it demonstrates the foundational components of Model, Orchestration, and tools all working together to achieve a specific goal. In the final section, we’ll explore how these components come together in Google-scale managed products like Vertex AI agents and Generative Playbooks.

这是一个相当简单的智能体例子，但它展示了模型、编排 (Orchestration) 和工具这些基础组件如何一起工作，去达成一个具体目标。最后一节会看这些组件如何在 Google 规模的托管产品里汇合，例如 Vertex AI 智能体和生成式 Playbook (Generative Playbooks)。

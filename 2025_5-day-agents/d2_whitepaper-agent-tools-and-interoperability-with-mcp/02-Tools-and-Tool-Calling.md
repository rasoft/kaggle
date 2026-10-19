# Tools and tool calling

<mark>工具与工具调用</mark>

## What do we mean by a tool?

<mark>工具是什么</mark>

In the world of modern AI, a tool is a function or a program an LLM-based application can use to accomplish a task outside the model's capabilities. The model itself generates content to respond to the user's question; tools let the application interact with other systems. Broadly speaking, tools fit into 2 types: they allow a model to know something or to do something. In other words, tools can retrieve data for the model to use in subsequent requests, by accessing structured and unstructured data sources; or, tools can perform an action on behalf of the user, often by calling an external API or by executing some other code or function.

<mark>在现代 AI 里，工具 (Tools) 是基于大语言模型 (LLM) 的应用可以拿来完成模型 (Model) 能力之外任务的函数或程序。模型自己生成内容来回答用户的问题；工具让应用去和其他系统交互。大体上，工具分成两类：让模型知道某件事，或让模型做成某件事。也就是说，工具可以访问结构化和非结构化数据源，取出数据供模型在后续请求里使用；也可以代表用户执行一个动作，常见做法是调用外部 API，或执行其他代码或函数。</mark>

An example application of a tool for an agent might include calling an API to get the weather forecast for the user's location, and presenting the information in the user's preferred units. This is a simple question, but to answer this correctly the model would need information about the user's current location and the current weather -- neither of those data points are included in the model's training data. The model also needs to be able to convert between temperature units; while foundation models are improving in their mathematical capabilities, this is not their strong suit and math computations are another area where it is generally best to call on an external function.

<mark>智能体 (Agent) 使用工具的一个例子：调用 API 获取用户所在位置的天气预报，并用用户偏好的单位呈现。问题本身很简单，但要答对，模型需要用户当前位置和当前天气。这两项都不在模型的训练数据里。模型还要能在温度单位之间换算。基础模型 (foundation model) 的数学能力在提高，但这不是它们的强项，数学计算通常也最好交给外部函数。</mark>

![Weather agent calling get_weather, get_location, and convert_temperature_units](image_001_page_9.png)

<mark>图 1：天气智能体的工具调用示例。用户问「今天天气怎么样？」；模型执行计划是：弄清用户在哪里，获取该地天气，再按用户偏好的单位回答。智能体调用 get_weather、get_location 和 convert_temperature_units。</mark>

---

## Types of tools

<mark>工具的类型</mark>

In an AI system, a tool is defined just like a function in a non-AI program. The tool definition declares a contract between the model and the tool. At a minimum, this includes a clear name, parameters, and a natural language description that explains its purpose and how it should be used. Tools come in several different types; three main types described here are Function Tools, Built-in Tools, and Agent Tools.

<mark>在 AI 系统里，工具的定义方式和普通程序里的函数一样。工具定义声明模型与工具之间的契约。至少包括一个清楚的名称、参数，以及一段自然语言描述，说明它的用途和用法。工具有好几种类型；这里讲的三种主要类型是函数工具 (Function Tools)、内置工具 (Built-in Tools) 和智能体工具 (Agent Tools)。</mark>

### Function Tools

<mark>函数工具</mark>

All models that support function calling<sup>10</sup> allow the developer to define external functions that the model can call as needed. The tool's definition should provide basic details about how the model should use the tool; this is provided to the model as part of the request context. In a Python framework like Google ADK, the definition passed to the model is extracted from the Python docstring in the tool code as in the example below.

<mark>所有支持函数调用 (function calling)<sup>10</sup> 的模型，都允许开发者定义模型可按需调用的外部函数。工具定义应当提供模型如何使用该工具的基本细节；这些内容会作为请求上下文的一部分交给模型。在 Google ADK 这类 Python 框架里，传给模型的定义是从工具代码的 Python docstring 里提取的，如下例。</mark>

This example shows a tool defined for Google ADK<sup>11</sup> that calls an external function to change the brightness of a light. The set_light_values is passed a ToolContext object (part of the Google ADK framework) to provide more details about the request context.

<mark>这个例子是为 Google ADK<sup>11</sup> 定义的工具，它调用外部函数来改变灯光亮度。set_light_values 会收到一个 ToolContext 对象（Google ADK 框架的一部分），用来提供请求上下文的更多细节。</mark>

```python
def set_light_values(
    brightness: int,
    color_temp: str,
    context: ToolContext) -> dict[str, int | str]:
    """This tool sets the brightness and color temperature of the room lights
       in the user's current location.
    Args:
        brightness: Light level from 0 to 100. Zero is off and 100 is full
                    brightness
        color_temp: Color temperature of the light fixture, which can be
                    `daylight`, `cool` or `warm`.
        context: A ToolContext object used to retrieve the user's location.
    Returns:
        A dictionary containing the set brightness and color temperature.
    """
    user_room_id = context.state['room_id']
    # This is an imaginary room lighting control API
    room = light_system.get_room(user_room_id)
    response = room.set_lights(brightness, color_temp)
    return {"tool_response": response}
```

**Snippet 1: Definition for set_light_values tool**

<mark>片段 1：set_light_values 工具的定义</mark>

### Built-in tools

<mark>内置工具</mark>

Some foundation models offer the ability to leverage built in tools, where the tool definition is given to the model implicitly, or behind the scenes of the model service. Google's Gemini API, for instance, provides several built-in tools: Grounding with Google Search<sup>12</sup>, Code Execution<sup>13</sup>, URL Context<sup>14</sup>, and Computer Use<sup>15</sup>.

<mark>有些基础模型提供使用内置工具的能力：工具定义是隐式交给模型的，或者说是在模型服务的幕后完成的。例如 Google 的 Gemini API 提供若干内置工具：基于 Google 搜索的接地 (Grounding with Google Search)<sup>12</sup>、代码执行 (Code Execution)<sup>13</sup>、URL 上下文 (URL Context)<sup>14</sup>，以及计算机使用 (Computer Use)<sup>15</sup>。</mark>

This example below shows how to invoke the Gemini built-in url_context tool. The tool definition itself is invisible to the developer; it's provided to the model separately.

<mark>下面的例子展示如何调用 Gemini 内置的 url_context 工具。工具定义本身对开发者不可见，它是另行提供给模型的。</mark>

```python
from google import genai
from google.genai.types import (
    Tool,
    GenerateContentConfig,
    HttpOptions,
    UrlContext
)
client = genai.Client(http_options=HttpOptions(api_version="v1")
model_id = "gemini-2.5-flash"
url_context_tool = Tool(
    url_context = UrlContext
)

url1 = "https://www.foodnetwork.com/recipes/ina-garten/perfect-roast-chicken-recipe-1940592"
url2 = "https://www.allrecipes.com/recipe/70679/simple-whole-roasted-chicken/"

response = client.models.generate_content(
    model=model_id,
    contents=("Compare the ingredients and cooking times from "
              f"the recipes at {url1} and {url2}"),
    config=GenerateContentConfig(
        tools=[url_context_tool],
        response_modalities=["TEXT"],
    )
)
for each in response.candidates[0].content.parts:
    print(each.text)
# For verification, you can inspect the metadata to see which URLs the
# model retrieved
print(response.candidates[0].url_context_metadata)
```

**Snippet 2: Calling url_context tool**

<mark>片段 2：调用 url_context 工具</mark>

### Agent Tools

<mark>智能体工具</mark>

An agent can also be invoked as a tool. This prevents a full handoff of the user conversation, allowing the primary agent to maintain control over the interaction and process the sub-agent's input and output as needed. In ADK, this is accomplished by using the AgentTool<sup>16</sup> class in the SDK. Google's A2A protocol<sup>17</sup>, discussed in Day 5: Prototype to Production, even allows you to make remote agents available as tools. In ADK, this is accomplished by using the AgentTool class in the SDK. Recently, the ADK has received a major upgrade with version 2.x, introducing a powerful graph-based framework that enables developers to organize individual agents into a sophisticated network of sub-agents.

<mark>智能体也可以被当作工具来调用。这样就不会把用户对话完全移交出去，主智能体仍能控制交互，并按需要处理子智能体的输入和输出。在 ADK 里，这通过 SDK 中的 AgentTool<sup>16</sup> 类完成。Google 的 A2A 协议（智能体对智能体，Agent-to-Agent）<sup>17</sup> 在「第 5 天：从原型到生产」中讨论，它甚至能让远程智能体作为工具可用。在 ADK 里，这通过 SDK 中的 AgentTool 类完成。最近 ADK 在 2.x 版做了一次大升级，引入基于图的框架，让开发者可以把各个智能体组织成一张精巧的子智能体网络。</mark>

```python
from google.adk.agents import LlmAgent
from google.adk.tools import AgentTool
tool_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="capital_agent",
    description="Returns the capital city for any country or state"
    instruction="""If the user gives you the name of a country or a state (e.g.
Tennessee or New South Wales), answer with the name of the capital city of that
country or state. Otherwise, tell the user you are not able to help them."""
)
user_agent = LlmAgent(
    model="gemini-2.5-flash",
    name="user_advice_agent",
    description="Answers user questions and gives advice",
    instruction="""Use the tools you have available to answer the
user's questions""",
    tools=[AgentTool(agent=capital_agent)]
)
```

**Snippet 3: AgentTool definition**

<mark>片段 3：AgentTool 定义</mark>

### Taxonomy of Agent Tools

<mark>智能体工具的分类</mark>

One way of categorizing agent tools is by their primary function, or the various types of interactions they facilitate. Here’s an overview of common types:

<mark>给智能体工具分类的一种方式，是看它们的主要功能，或它们促成的交互类型。常见类型如下：</mark>

- Information Retrieval: Allow agents to fetch data from various sources, such as web searches, databases, or unstructured documents.

<mark>信息检索 (Information Retrieval)：让智能体从各种来源取数据，例如网页搜索、数据库或非结构化文档。</mark>

- Action / Execution: Allow agents to perform real-world operations: sending emails, posting messages, initiating code execution, or controlling physical devices.

<mark>动作 / 执行 (Action / Execution)：让智能体做现实世界里的操作：发邮件、发消息、启动代码执行，或控制物理设备。</mark>

- System / API Integration: Allow agents to connect with existing software systems and APIs, integrate into enterprise workflows, or interact with third-party services.

<mark>系统 / API 集成 (System / API Integration)：让智能体连接现有软件系统和 API，接入企业工作流，或与第三方服务交互。</mark>

- Human-in-the-Loop: Facilitate collaboration with human users: ask for clarification, seek approval for critical actions, or hand off tasks for human judgment.

<mark>人在回路 (Human-in-the-Loop, HITL)：促成与人类用户的协作：请求澄清、为关键动作寻求批准，或把任务交由人类判断。</mark>

| Tool | Use Case | Key Design Tips |
| --- | --- | --- |
| Structured Data Retrieval | Querying databases, spreadsheets, or other structured data sources (e.g., MCP Toolbox, NL2SQL) | Define clear schemas, optimize for efficient querying, handle data types gracefully. |
| Unstructured Data Retrieval | Searching documents, web pages, or knowledge bases (e.g., RAG sample) | Implement robust search algorithms, consider context window limitations, and provide clear retrieval instructions. |
| Connecting to Built-in Templates | Generating content from predefined templates | Ensure template parameters are well-defined, provide clear guidance on template selection. |
| Google Connectors | Interacting with Google Workspace apps (e.g., Gmail, Drive, Calendar) | Leverage Google APIs, ensure proper authentication and authorization, handle API rate limits. |
| Third-Party Connectors | Integrating with external services and applications | Document external API specifications, manage API keys securely, implement error handling for external calls. |

| <mark>工具</mark> | <mark>使用场景</mark> | <mark>关键设计提示</mark> |
| --- | --- | --- |
| <mark>结构化数据检索</mark> | <mark>查询数据库、电子表格或其他结构化数据源（例如 MCP Toolbox、NL2SQL）</mark> | <mark>定义清楚的模式，为高效查询做优化，妥善处理数据类型。</mark> |
| <mark>非结构化数据检索</mark> | <mark>搜索文档、网页或知识库（例如 RAG 示例）</mark> | <mark>实现稳健的搜索算法，考虑上下文窗口的限制，并提供清楚的检索说明。</mark> |
| <mark>连接内置模板</mark> | <mark>从预定义模板生成内容</mark> | <mark>确保模板参数定义清楚，对如何选择模板给出明确指导。</mark> |
| <mark>Google 连接器</mark> | <mark>与 Google Workspace 应用交互（例如 Gmail、Drive、Calendar）</mark> | <mark>利用 Google API，确保正确的认证与授权，处理 API 速率限制。</mark> |
| <mark>第三方连接器</mark> | <mark>与外部服务和应用集成</mark> | <mark>记录外部 API 规范，安全地管理 API 密钥，为外部调用实现错误处理。</mark> |

**Table 1: Tool categories & design considerations**

<mark>表 1：工具类别与设计考量</mark>

---

## Best Practices

<mark>最佳实践</mark>

As tool use becomes more widespread in AI applications and new categories of tools emerge, recognized best practices for tool use are evolving rapidly. Nevertheless, several guidelines are emerging that seem broadly applicable.

<mark>随着工具使用 (Tool Use) 在 AI 应用里越来越普遍，新的工具类别也在出现，公认的工具使用最佳实践变化很快。尽管如此，有几条准则正在成形，看起来适用范围很广。</mark>

### Documentation is important

<mark>文档很重要</mark>

The tool documentation (name, description and attributes) are all passed to the model as a part of the request context, so all of these are important to help the model use the tool correctly.

<mark>工具文档（名称、描述和属性）都会作为请求上下文的一部分传给模型，所以这些都对模型正确使用工具很重要。</mark>

- Use a clear name: The name of the tool should be clearly descriptive, human readable, and specific to help the model decide which tool to use. For instance, create_critical_bug_in_jira_with_priority is clearer than update_jira. This is also important for governance; if tool calls are logged, having clear names will make audit logs more informative.

<mark>使用清楚的名称：工具名应当描述清楚、人类可读，并且具体，帮助模型决定用哪个工具。例如，create_critical_bug_in_jira_with_priority 比 update_jira 更清楚。这对治理也很重要；如果记录了工具调用，清楚的名称会让审计日志更有信息量。</mark>

- Describe all input and output parameters: All inputs to the tool should be clearly described, including both the required type and the use the tool will make of the parameter.

<mark>描述全部输入和输出参数：工具的所有输入都应当描述清楚，包括所需类型，以及工具会如何使用该参数。</mark>

- Simplify parameter lists: Long parameter lists can confuse the model; keep them parameter lists short and give parameters clear names.

<mark>简化参数列表：过长的参数列表会把模型搞糊涂；参数列表要短，参数名要清楚。</mark>

- Clarify tool descriptions: Provide a clear, detailed description of the input and output parameters, the purpose of the tool, and any other details needed to call the tool effectively. Avoid shorthand or technical jargon; focus on clear explanations using simple terminology.

<mark>把工具描述写清楚：对输入和输出参数、工具的用途，以及有效调用工具所需的其他细节，给出清楚、详细的描述。避免缩写或技术行话；用简单术语把解释写清楚。</mark>

- Add targeted examples: Examples can help address ambiguities, show how to handle tricky requests, or clarify distinctions in terminology. They can also be a way to refine and target model behavior without resorting to more expensive approaches like fine tuning. You can also dynamically retrieve examples related to the immediate task to minimize context bloat.

<mark>加入有针对性的示例：示例能帮助消除歧义、展示如何处理棘手请求，或澄清术语上的差别。它们也可以用来打磨并引导模型行为，而不必诉诸微调这类更贵的办法。也可以动态检索与当前任务相关的示例，以减少上下文膨胀。</mark>

- Provide default values: Provide default values for key parameters and be sure to document and describe the default values in the tool documentation. LLMs can often use default values correctly, if they are well-documented.

<mark>提供默认值：为关键参数提供默认值，并务必在工具文档里记录和描述这些默认值。只要文档写得好，大语言模型往往能正确使用默认值。</mark>

The following are examples of good and bad tool documentation.

<mark>下面是好的和差的工具文档示例。</mark>

```python
def get_product_information(product_id: str) -> dict:
  """
  Retrieves comprehensive information about a product based on the unique
  product ID.
  Args:
    product_id: The unique identifier for the product.
  Returns:
    A dictionary containing product details. Expected keys include:
      'product_name': The name of the product.
      'brand': The brand name of the product
      'description': A paragraph of text describing the product.
      'category': The category of the product.
      'status': The current status of the product (e.g., 'active',
      'inactive', 'suspended').
   Example return value:
    {
        'product_name': 'Astro Zoom Kid's Trainers',
        'brand': 'Cymbal Athletic Shoes',
        'description': '...',
        'category': 'Children's Shoes',
        'status': 'active'
    }
  """
```

**Snippet 4: Good tool documentation**

<mark>片段 4：好的工具文档</mark>

```python
def fetchpd(pid):
  """
  Retrieves product data

  Args:
     pid: id
  Returns:
     dict of data
  """
```

**Snippet 5: Bad tool documentation**

<mark>片段 5：差的工具文档</mark>

### Describe actions, not implementations

<mark>描述动作，不要描述实现</mark>

Assuming each tool is well-documented, the model's instructions should describe actions, not specific tools. This is important to eliminate any possibility of conflict between instructions on how to use the tool (which can confuse the LLM). Where the available tools can change dynamically, as with MCP, this is even more relevant.

<mark>假定每个工具都有良好文档，模型的指令应当描述动作，而不是点名具体工具。这一点很重要，可以消除「如何使用工具」的指令彼此冲突的可能（这种冲突会把大语言模型搞糊涂）。当可用工具会动态变化时，例如在 MCP 中，这一点更加要紧。</mark>

- Describe what, not how: Explain what the model needs to do, not how to do it. For example, say "create a bug to describe the issue", instead of "use the create_bug tool".

<mark>描述做什么，不要描述怎么做：说明模型需要完成什么，而不是怎么完成。例如说「创建一条缺陷来描述这个问题」，而不是「使用 create_bug 工具」。</mark>

- Don't duplicate instructions: Don't repeat or re-state the tool instructions or documentation. This can confuse the model, and creates an additional dependency between the system instructions and the tool implementation.

<mark>不要重复指令：不要重复或复述工具的指令或文档。这会把模型搞糊涂，还会在系统指令和工具实现之间多加一层依赖。</mark>

- Don't dictate workflows: Describe the objective, and allow scope for the model to use tools autonomously, rather than dictating a specific sequence of actions.

<mark>不要规定工作流：描述目标，给模型自主使用工具的余地，而不是规定一串具体动作的顺序。</mark>

- DO explain tool interactions: If one tool has a side-effect that may affect a different tool, document this. For instance, a fetch_web_page tool may store the retrieved web page in a file; document this so the agent knows how to access the data.

<mark>一定要说明工具之间的相互影响：如果一个工具的副作用可能影响另一个工具，就把这一点写进文档。例如，fetch_web_page 工具可能把取回的网页存进文件；写清楚这一点，智能体才知道如何取得这些数据。</mark>

### Publish tasks, not API calls

<mark>发布任务，不要发布 API 调用</mark>

Tools should encapsulate a task the agent needs to perform, not an external API. It's easy to write tools that are just thin wrappers over the existing API surface, but this is a mistake. Instead, tool developers should define tools that clearly capture specific actions the agent might take on behalf of the user, and document the specific action and the parameters needed. APIs are intended to be used by human developers with full knowledge of the available data and the API parameters; complex Enterprise APIs can have tens or even hundreds of possible parameters that influence the API output. Tools for agents, by contrast, are expected to be used dynamically, by an agent that needs to decide at runtime which parameters to use and what data to pass. If the tool represents a specific task the agent should accomplish, the agent is much more likely to be able to call it correctly.

<mark>工具应当封装智能体需要执行的一项任务，而不是一个外部 API。把现有 API 表面薄薄地包一层，写成工具，很容易，但这是个错误。工具开发者应当定义清楚捕捉智能体可能代表用户采取的具体动作的工具，并写明该动作和所需参数。API 是给人类开发者用的，他们完全了解可用数据和 API 参数；复杂的企业 API 可以有几十甚至上百个会影响输出的参数。给智能体用的工具则相反，预期由智能体动态使用：它必须在运行时决定用哪些参数、传入什么数据。如果工具代表的是智能体应当完成的一项具体任务，智能体正确调用它的可能性就大得多。</mark>

### Make tools as granular as possible

<mark>工具尽量拆细</mark>

Keeping functions concise and limited to a single function is standard coding best practice; follow this guidance when defining tools too. This makes it easier to document the tool and allows the agent to be more consistent in determining when the tool is needed.

<mark>让函数保持简短、只做一件事，是标准的编码最佳实践；定义工具时也遵循这条。这样更容易写文档，智能体判断何时需要该工具也会更稳定。</mark>

- Define clear responsibilities: Make sure each tool has a clear, well-documented purpose. What does it do? When should it be called? Does it have any side effects? What data will it return?

<mark>定义清楚的职责：确保每个工具都有清楚、文档完善的用途。它做什么？何时该调用？有没有副作用？会返回什么数据？</mark>

- Don't create multi-tools: In general, don't create tools that take many steps in turn or encapsulate a long workflow. These can be complicated to document and maintain, and can be difficult for LLMs to use consistently. There are scenarios when such a tool may be useful -- for instance, if a commonly performed workflow requires many tool calls in sequence, defining a single tool to encapsulate many operations may be more efficient. In these cases be sure to document very clearly what the tool is doing so the LLM can use the tool effectively.

<mark>不要做「多功能工具」：一般不要做那种依次走很多步、或把一条长工作流包进去的工具。它们文档和维护都很复杂，大语言模型也很难稳定地使用。有些场景下这种工具可能有用，例如一条经常执行的工作流需要按顺序做很多次工具调用，用一个工具把许多操作封装起来可能更高效。这时务必非常清楚地写明工具在做什么，大语言模型才能有效使用它。</mark>

### Design for concise output

<mark>为简洁输出而设计</mark>

Poorly designed tools can sometimes return large volumes of data, which can adversely affect performance and cost.

<mark>设计糟糕的工具有时会返回大量数据，从而损害性能和成本。</mark>

- Don't return large responses: Large data tables or dictionaries, downloaded files, generated images, etc. can all quickly swamp the output context of an LLM. These responses are also frequently stored in an agent's conversation history, so large responses can impact subsequent requests as well.

<mark>不要返回庞大的响应：大的数据表或字典、下载的文件、生成的图像等，都会很快淹没大语言模型的输出上下文。这些响应也常常存在智能体的对话历史里，所以庞大的响应还会影响后续请求。</mark>

- Use external systems: Make use of external systems for data storage and access. For instance, instead of returning a large query result directly to the LLM, insert it into a temporary database table and return the table name, so a subsequent tool can retrieve the data directly. Some AI frameworks also provide persistent external storage as part of the framework itself, such as the Artifact Service in Google ADK<sup>18</sup>.

<mark>使用外部系统：用外部系统来存储和访问数据。例如，不要把一大份查询结果直接返回给大语言模型，而是把它插入一张临时数据库表，只返回表名，让后续工具直接取数据。有些 AI 框架本身也提供持久的外部存储，例如 Google ADK 中的 Artifact Service<sup>18</sup>。</mark>

### Use validation effectively

<mark>用好校验</mark>

Most tool calling frameworks include optional schema validation for tool inputs and outputs. Use this validation capability wherever possible. Input and output schemas serve two roles with LLM tool calling. They serve as further documentation of the tool's capabilities and function, giving the LLM a clearer picture of when and how to use the tool; and they provide a run-time check on tool operation, allowing the application itself to validate whether the tool is being called correctly.

<mark>大多数工具调用框架都包含对工具输入和输出的可选模式校验。只要可能，就用上这层校验。在大语言模型的工具调用里，输入和输出模式有两个作用。它们是工具能力和功能的进一步文档，让大语言模型更清楚何时以及如何使用该工具；它们也在运行时检查工具操作，让应用自己校验工具是否被正确调用。</mark>

### Provide descriptive error messages

<mark>提供描述性的错误信息</mark>

Tool error messages are an overlooked opportunity for refining and documenting tool capabilities. Often, even well-documented tools will simply return an error code, or at best a short, non-descriptive error message. In most tool calling systems, the tool response will also be provided to the calling LLM, so it provides another avenue for giving instructions. The tool's error message should also give some instruction to the LLM about what to do to address the specific error. For example, a tool that retrieves product data could return a response that says "No product data found for product ID XXX. Ask the customer to confirm the product name, and look up the product ID by name to confirm you have the correct ID."

<mark>工具的错误信息是打磨和记录工具能力时被忽略的机会。即便文档写得很好的工具，也常常只返回一个错误码，最多是一句短而没有描述性的错误信息。在大多数工具调用系统里，工具响应也会交给发起调用的大语言模型，所以这是另一条下达指令的通道。工具的错误信息还应当告诉大语言模型，要处理这个具体错误该做什么。例如，一个检索产品数据的工具可以返回这样的响应：「找不到产品 ID XXX 的产品数据。请让客户确认产品名称，再按名称查找产品 ID，以确认你拿到的 ID 是对的。」</mark>

# Understanding the Model Context Protocol

<mark>理解模型上下文协议</mark>

## The "N x M" Integration Problem and the need for Standardization

<mark>「N × M」集成问题，以及为什么需要标准化</mark>

Tools provide the essential link between an AI agent or an LLM and the external world. The ecosystem of externally accessible tools, data sources and other integrations, however, is increasingly fragmented and complex. Integrating an LLM with an external tool usually requires a custom-built, one-off connector for every pairing of tool and application. This leads to an explosion in development effort, often called the "N x M" integration problem, where the number of necessary custom connections grows exponentially with each new model (N) or tool (M) added to the ecosystem.<sup>19</sup>

<mark>工具是 AI 智能体 (Agent) 或大语言模型 (LLM) 与外部世界之间的关键连接。然而，可从外部访问的工具、数据源和其他集成所构成的生态，正变得越来越碎片化、越来越复杂。把大语言模型和一个外部工具集成，通常要为每一对「工具 + 应用」定制一个一次性连接器。开发工作量因此爆炸，这常被称作「N × M」集成问题：生态里每新增一个模型 (N) 或工具 (M)，所需的定制连接数就指数增长。<sup>19</sup></mark>

Anthropic introduced the Model Context Protocol (MCP) in November 2024 as an open standard to begin addressing this situation. The goal of MCP from the outset has been to replace the fragmented landscape of custom integrations with a unified, plug-and-play protocol that could serve as a universal interface between AI applications and the vast world of external tools and data. By standardizing this communication layer, MCP aims to decouple the AI agent from the specific implementation details of the tools it uses, allowing for a more modular, scalable, and efficient ecosystem.

<mark>Anthropic 在 2024 年 11 月提出模型上下文协议 (Model Context Protocol, MCP)，作为开放标准，开始应对这一局面。MCP 从一开始的目标，就是用一套统一、即插即用的协议，取代碎片化的定制集成，成为 AI 应用与庞大的外部工具和数据世界之间的通用接口。通过把这层通信标准化，MCP 想把 AI 智能体与它所用工具的具体实现细节解耦，从而得到更模块化、可扩展、高效的生态。</mark>

---

## Core Architectural Components: Hosts, Clients, and Servers

<mark>核心架构组件：宿主、客户端与服务器</mark>

The Model Context Protocol implements a client-server model, inspired by the Language Server Protocol (LSP) in the software development world.<sup>9</sup> This architecture separates the AI application from the tool integrations and allows a more modular and extensible approach to tool development. The core MCP components are the Host, the Client, and the Server.

<mark>模型上下文协议实现的是客户端—服务器模型，灵感来自软件开发领域的语言服务器协议 (Language Server Protocol, LSP)。<sup>9</sup> 这一架构把 AI 应用与工具集成分开，让工具开发更模块化、更可扩展。MCP 的核心组件是宿主 (Host)、客户端 (Client) 和服务器 (Server)。</mark>

- MCP Host: The application responsible for creating and managing individual MCP clients; may be a standalone application, or a sub-component of a larger system such as a multi-agent system. Responsibilities include managing the user experience, orchestrating the use of tools, and enforcing security policies and content guardrails.

<mark>MCP 宿主：负责创建并管理各个 MCP 客户端的应用；可以是独立应用，也可以是更大系统（例如多智能体系统）里的一个子组件。职责包括管理用户体验、编排 (Orchestration) 工具的使用，以及执行安全策略和内容护栏。</mark>

- MCP Client: A software component embedded within the Host that maintains the connection with the Server. The responsibilities of the client are issuing commands, receiving responses, and managing the lifecycle of the communication session with its MCP Server.

<mark>MCP 客户端：嵌在宿主里、维持与服务器连接的软件组件。客户端的职责是发出命令、接收响应，并管理它与 MCP 服务器之间通信会话的生命周期。</mark>

- MCP Server: A program that provides a set of capabilities the server developer wants to make available to AI applications, often functioning as an adapter or a proxy for an external tool, data source, or API. Primary responsibilities are advertising available tools (tool discovery), receiving and executing commands, and formatting and returning results. In enterprise contexts, servers are also responsible for security, scalability and governance.

<mark>MCP 服务器：向 AI 应用提供一组服务器开发者希望开放的能力的程序，常常充当外部工具、数据源或 API 的适配器或代理。主要职责是通告可用工具（工具发现）、接收并执行命令，以及格式化并返回结果。在企业场景里，服务器还负责安全、可扩展性和治理。</mark>

Google provides multiple MCP Servers for its products including custom managed MCP servers on Google Cloud. The following diagram shows the relationships between each of these components and how they communicate.

<mark>Google 为其产品提供多个 MCP 服务器，包括 Google Cloud 上的定制托管 MCP 服务器。下图展示这些组件之间的关系，以及它们如何通信。</mark>

![MCP Host with three Clients calling get_weather and get_traffic on a Server](image_002_page_22.png)

<mark>图 2：智能体应用中的 MCP 宿主、客户端与服务器。宿主里的三个客户端各自经会话调用 tools/call；服务器提供 get_weather 和 get_traffic。图中给出一条 JSON-RPC 2.0 请求，方法为 tools/call，参数是 location 为 New York 的 get_weather。</mark>

This architectural model is aimed at supporting the development of a competitive and innovative AI tooling ecosystem. AI agent developers should be able to focus on their core competency—reasoning and user experience—while third-party developers can create specialized MCP servers for any conceivable tool or API.

<mark>这一架构模型旨在支持有竞争力、有创新的 AI 工具生态。AI 智能体开发者应当能把精力放在核心能力上，也就是推理 (Reasoning) 和用户体验；第三方开发者则可以为任何能想到的工具或 API 创建专门的 MCP 服务器。</mark>

---

## The Communication Layer: JSON-RPC, Transports, and Message Types

<mark>通信层：JSON-RPC、传输与消息类型</mark>

All communication between MCP clients and servers is built on a standardized technical foundation for consistency and interoperability.

<mark>MCP 客户端与服务器之间的全部通信，都建立在一套标准化的技术基础上，以保证一致性和互操作性。</mark>

**Base Protocol:** MCP uses JSON-RPC 2.0 as its base message format. This gives it a lightweight, text-based, and language-agnostic structure for all communications.

<mark>基础协议：MCP 用 JSON-RPC 2.0 作为基础消息格式。这为全部通信提供了轻量、基于文本、与语言无关的结构。</mark>

**Message Types:** The protocol defines four fundamental message types that govern the interaction flow:

<mark>消息类型：协议定义了四种基本消息类型，用来支配交互流程：</mark>

- Requests: An RPC call sent from one party to another that expects a response.

<mark>请求 (Requests)：一方发给另一方、并期待响应的 RPC 调用。</mark>

- Results: A message containing the successful outcome of a corresponding request.

<mark>结果 (Results)：包含对应请求成功结果的消息。</mark>

- Errors: A message indicating that a request failed, including code and description.

<mark>错误 (Errors)：表明请求失败的消息，包含代码和描述。</mark>

- Notifications: A one-way message that does not require a response and cannot be replied to.

<mark>通知 (Notifications)：不需要响应、也不能回复的单向消息。</mark>

**Transport Mechanisms:** MCP also needs a standard protocol for communication between the client and server, called a "transport protocol", to ensure each component is able to interpret the other's messages. MCP supports two transport protocols - one for local communication and one for remote connections.<sup>20</sup>

<mark>传输机制：MCP 还需要一套客户端与服务器之间通信的标准协议，称为「传输协议」，以确保各方都能解释对方的消息。MCP 支持两种传输协议：一种用于本地通信，一种用于远程连接。<sup>20</sup></mark>

- stdio (Standard Input/Output): Used for fast and direct communication in local environments where the MCP server runs as a subprocess of the Host application; used when tools need to access local resources such as the user's filesystem.

<mark>stdio（标准输入/输出，Standard Input/Output）：用于本地环境中快速、直接的通信。此时 MCP 服务器作为宿主应用的子进程运行；当工具需要访问用户文件系统等本地资源时使用。</mark>

- Streamable HTTP: Recommended remote client-server protocol.<sup>21</sup> It supports SSE streaming responses, but also allows stateless servers and can be implemented in a plain HTTP server without requiring SSE.

<mark>可流式 HTTP (Streamable HTTP)：推荐的远程客户端—服务器协议。<sup>21</sup> 它支持 SSE 流式响应，也允许无状态服务器，并且可以在普通 HTTP 服务器上实现，而不必依赖 SSE。</mark>

![stdio, HTTP plus SSE, and Streamable HTTP transports](image_003_page_24.png)

<mark>图 3：MCP 传输协议。应用内的宿主经 stdio 连接本地服务器上的 get_weather；经 HTTP + SSE 与有状态服务器上的 get_user_messages 建立 HTTP 会话；经可流式 HTTP 连接无状态服务器上的 get_latest_price，其中命令通道为 POST，通告通道为 GET。</mark>

---

## Key Primitives: Tools and others

<mark>关键原语：工具及其他</mark>

On top of the basic communication framework, MCP defines several key concepts or entity types to enhance the capabilities of LLM-based applications for interacting with external systems. The first three are capabilities offered by the Server to the Client; the remaining three are offered by the Client to the server. On the server side, these capabilities are: Tools, Resources and Prompts; and on the client side, the capabilities are Sampling, Elicitation and Roots.

<mark>在基本通信框架之上，MCP 定义了若干关键概念或实体类型，用来增强基于大语言模型的应用与外部系统交互的能力。前三种是服务器提供给客户端的能力；后三种是客户端提供给服务器的能力。服务器侧的能力是：工具 (Tools)、资源 (Resources) 和提示 (Prompts)；客户端侧的能力是：采样 (Sampling)、征询 (Elicitation) 和根 (Roots)。</mark>

Of these capabilities defined by the MCP specification, only Tools are broadly supported. As the table below shows, while Tools are supported by nearly all tracked client applications, Resources and Prompts are only supported by approximately a third, and support for client-side capabilities is significantly lower than that. So it remains to be seen whether these capabilities will play a significant role in future MCP deployments.

<mark>在 MCP 规范定义的这些能力里，只有工具得到了广泛支持。如下表所示，几乎所有被跟踪的客户端应用都支持工具，资源和提示大约只有三分之一支持，客户端侧能力的支持率还要低得多。这些能力会不会在未来的 MCP 部署里扮演重要角色，还有待观察。</mark>

| Capability | Supported | Not supported | Unknown/Other | % Supported |
| --- | --- | --- | --- | --- |
| Tools | 78 | 1 | 0 | 99% |
| Resources | 27 | 51 | 1 | 34% |
| Prompts | 25 | 54 | 0 | 32% |
| Sampling | 8 | 70 | 1 | 10% |
| Elicitation | 3 | 74 | 2 | 4% |
| Roots | 4 | 75 | 0 | 5% |

| <mark>能力</mark> | <mark>支持</mark> | <mark>不支持</mark> | <mark>未知 / 其他</mark> | <mark>支持比例</mark> |
| --- | --- | --- | --- | --- |
| <mark>工具</mark> | 78 | 1 | 0 | 99% |
| <mark>资源</mark> | 27 | 51 | 1 | 34% |
| <mark>提示</mark> | 25 | 54 | 0 | 32% |
| <mark>采样</mark> | 8 | 70 | 1 | 10% |
| <mark>征询</mark> | 3 | 74 | 2 | 4% |
| <mark>根</mark> | 4 | 75 | 0 | 5% |

**Table 2: Percentage of publicly available MCP clients supporting MCP server / client capabilities.** Source: https://modelcontextprotocol.io/clients, retrieved 15 September 2025

<mark>表 2：公开 MCP 客户端对 MCP 服务器 / 客户端能力的支持比例。来源：https://modelcontextprotocol.io/clients，检索于 2025 年 9 月 15 日。</mark>

In this section we will concentrate on Tools, since they have by far the broadest adoption and are the core driver of MCP value, and only briefly describe the remaining capabilities.

<mark>本节集中讲工具，因为它们的采用面远远最广，也是 MCP 价值的核心驱动；其余能力只作简要描述。</mark>

### Tools

<mark>工具</mark>

The Tool<sup>22</sup> entity in MCP is a standardized way for a server to describe a function it makes available to clients. Some examples might be read_file, get_weather, execute_sql, or create_ticket. MCP Servers publish a list of their available tools, including descriptions and parameter schemas, for agents to discover.

<mark>MCP 中的工具 (Tool)<sup>22</sup> 实体，是服务器向客户端描述它所提供函数的标准化方式。例子可以是 read_file、get_weather、execute_sql 或 create_ticket。MCP 服务器会发布可用工具的列表，包括描述和参数模式，供智能体发现。</mark>

### Tool Definition

<mark>工具定义</mark>

Tool definitions must conform to a JSON schema<sup>23</sup> with the following fields:

<mark>工具定义必须符合 JSON schema<sup>23</sup>，包含以下字段：</mark>

- name: Unique identifier for the tool

<mark>name：工具的唯一标识符</mark>

- title: [OPTIONAL] human-readable name for display purposes

<mark>title：［可选］供显示用的人类可读名称</mark>

- description: Human- (and LLM-) readable description of functionality

<mark>description：人类（以及大语言模型）可读的功能描述</mark>

- inputSchema: JSON schema defining expected tool parameters

<mark>inputSchema：定义期望工具参数的 JSON schema</mark>

- outputSchema: [OPTIONAL]: JSON schema defining output structure

<mark>outputSchema：［可选］定义输出结构的 JSON schema</mark>

- annotations: [OPTIONAL]: Properties describing tool behavior

<mark>annotations：［可选］描述工具行为的属性</mark>

Tools documentation in MCP should follow the same general best practices we described above. For instance, properties such as title and description may be optional in the schema, but they should always be included. They provide an important channel for giving more detailed instructions to client LLMs about how to use the tool effectively.

<mark>MCP 中的工具文档应当遵循上文所述的一般最佳实践。例如，title 和 description 在模式里可以是可选的，但应当始终写上。它们是一条重要通道，用来向客户端的大语言模型给出更详细的指令，说明如何有效使用该工具。</mark>

The inputSchema and outputSchema fields are also critical for ensuring correct usage of the tool. They should be clearly descriptive and carefully worded, and each property defined in both schemas should have a descriptive name and a clear description. Both schema fields should be treated as required.

<mark>inputSchema 和 outputSchema 字段对确保工具被正确使用也至关重要。它们应当描述清楚、措辞谨慎，两个模式里定义的每个属性都应当有描述性的名称和清楚的说明。这两个模式字段都应当当作必填来对待。</mark>

The annotations field is declared as optional and should remain that way. The properties defined in the spec are:

<mark>annotations 字段被声明为可选，也应当保持可选。规范里定义的属性是：</mark>

- destructiveHint: May perform destructive updates (default: true).

<mark>destructiveHint：可能执行破坏性更新（默认：true）。</mark>

- idempotentHint: Calling repeatedly with the same arguments will have no additional effect (default: false).

<mark>idempotentHint：用相同参数反复调用不会产生额外效果（默认：false）。</mark>

- openWorldHint: May interact with an "open world" of external entities (default: true).

<mark>openWorldHint：可能与外部实体构成的「开放世界」交互（默认：true）。</mark>

- readOnlyHint: Does not modify its environment (default: false)

<mark>readOnlyHint：不修改其所处环境（默认：false）</mark>

- title: Human-readable title for the tool (note that this is not required to agree with the title as provided in the tool definition).

<mark>title：工具的人类可读标题（注意，它不要求与工具定义里给出的 title 一致）。</mark>

All the properties declared in this field are only hints, and are not guaranteed to describe the tool's operations accurately. MCP clients should not rely on these properties from untrusted servers, and even when the server is trusted, the spec does not require that the tool properties are guaranteed to be true. Exercise caution when making use of these annotations.

<mark>该字段里声明的所有属性都只是提示，并不保证准确描述工具的操作。MCP 客户端不应当依赖来自不受信任服务器的这些属性；即便服务器受信任，规范也不要求这些工具属性保证为真。使用这些注解时要谨慎。</mark>

The following example shows an MCP Tool definition with each of these fields included.

<mark>下面的例子展示一个包含上述各字段的 MCP 工具定义。</mark>

```json
{
  "name": "get_stock_price",
  "title": "Stock Price Retrieval Tool",
  "description": "Get stock price for a specific ticker symbol. If 'date' is provided, it will retrieve the last price or closing price for that date. Otherwise it will retrieve the latest price.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "symbol": {
        "type": "string",
        "description": "Stock ticker symbol",
      }
      "date": {
        "type:" "string",
        "description": "Date to retrieve (in YYYY-MM-DD format)"
      }
    },
    "required": ["symbol"]
  },
  "outputSchema": {
    "type": "object",
    "properties": {
      "price": {
        "type": "number",
        "description": "Stock price"
      },
      "date": {
        "type": "string",
        "description": "Stock price date"
      }
    },
    "required": ["price", "date"]
  },
  "annotations": {
    "readOnlyHint": "true"
  }
}
```

**Snippet 6: Example tool definition for a stock price retrieval tool**

<mark>片段 6：股价检索工具的示例定义</mark>

### Tool Results

<mark>工具结果</mark>

MCP tools can return their results in a number of ways. Results can be structured or unstructured, and can contain multiple different content types. Results can link to other resources on the server, and results can also be returned as a single response or a stream of responses.

<mark>MCP 工具可以用多种方式返回结果。结果可以是结构化的或非结构化的，也可以包含多种不同的内容类型。结果可以链接到服务器上的其他资源，也可以作为单次响应或响应流返回。</mark>

#### Unstructured Content

<mark>非结构化内容</mark>

Unstructured content can take several types. The Text type represents unstructured string data; the Audio and Image content types contain base64-encoded image or audio data tagged with the appropriate MIME type.

<mark>非结构化内容可以有几种类型。Text 类型表示非结构化字符串数据；Audio 和 Image 内容类型包含 base64 编码的图像或音频数据，并标有相应的 MIME 类型。</mark>

MCP also allows Tools to return specified Resources, which gives developers more options for managing their application workflow. Resources can be returned either as a link to a Resource entity stored at another URI, including the title, description, size, and MIME type; or fully embedded in the Tool result. In either case, client developers should be very cautious about retrieving or using resources returned from an MCP server in this way, and should only use Resources from trusted sources.

<mark>MCP 也允许工具返回指定的资源，这给了开发者更多管理应用工作流的选择。资源可以以链接形式返回，指向存放在另一个 URI 的资源实体，并带上标题、描述、大小和 MIME 类型；也可以完整嵌入工具结果。无论哪种方式，客户端开发者都应当非常谨慎地检索或使用以这种方式从 MCP 服务器返回的资源，并且只应使用来自受信任来源的资源。</mark>

#### Structured Content

<mark>结构化内容</mark>

Structured content is always returned as a JSON object. Tool implementers should always use the outputSchema capability to provide a JSON schema clients can use to validate the tool results, and client developers should validate the tool results against the provided schema. Just as with standard function calling, a defined output schema serves a dual purpose: it allows the client to interpret and parse the output effectively, and it communicates to the calling LLM how and why to use this particular tool.

<mark>结构化内容始终以 JSON 对象返回。工具实现者应当始终使用 outputSchema 能力，提供客户端可用来校验工具结果的 JSON schema；客户端开发者也应当对照所提供的模式校验工具结果。和标准函数调用一样，定义好的输出模式有双重用途：它让客户端能有效解释和解析输出，也向发起调用的大语言模型传达为何以及如何使用这个特定工具。</mark>

### Error Handling

<mark>错误处理</mark>

MCP also defines two standard error reporting mechanisms. A Server can return standard JSON-RPC errors for protocol issues such as unknown tools, invalid arguments, or server errors. It can also return error messages in the tool results by setting the "isError": true parameter in the result object. These errors are used for errors generated in the operation of the tool itself, such as backend API failures, invalid data, or business logic errors. Error messages are an important and often overlooked channel for providing further context to the calling LLM. MCP tool developers should consider how best to use this channel for aiding their clients in failing over from errors. The following examples show how a developer might use each of these error types to provide additional guidance to the client LLM.

<mark>MCP 还定义了两种标准的错误报告机制。服务器可以对协议问题返回标准 JSON-RPC 错误，例如未知工具、无效参数或服务器错误。它也可以在结果对象里设置 "isError": true，把错误信息放进工具结果。这些错误用于工具自身操作中产生的错误，例如后端 API 失败、无效数据或业务逻辑错误。错误信息是向发起调用的大语言模型提供进一步上下文的重要通道，却常常被忽略。MCP 工具开发者应当考虑如何最好地利用这条通道，帮助客户端从错误中转移。下面的例子展示开发者如何用这两种错误类型，向客户端大语言模型提供额外指导。</mark>

```python
{
  "jsonrpc": "2.0",
  "id": 3,
  "error": {
    "code": -32602,
    "message": "Unknown tool: invalid_tool_name. It may be misspelled, or the tool may not exist on this server. Check the tool name and if necessary request an updated list of tools."
  }
}
```

**Snippet 7: Example protocol error.** Source: https://modelcontextprotocol.io/specification/2025-06-18/server/tools#error-handling, retrieved 2025-09-16.

<mark>片段 7：协议错误示例。来源：https://modelcontextprotocol.io/specification/2025-06-18/server/tools#error-handling，检索于 2025-09-16。</mark>

```python
{
  "jsonrpc": "2.0",
  "id": 4,
  "result": {
    "content": [
      {
        "type": "text",
        "text": "Failed to fetch weather data: API rate limit exceeded. Wait 15 seconds before calling this tool again."
      }
    ],
    "isError": true
  }
}
```

**Snippet 8: Example tool execution error.** Source: https://modelcontextprotocol.io/specification/2025-06-18/server/tools#error-handling, retrieved 2025-09-16

<mark>片段 8：工具执行错误示例。来源：https://modelcontextprotocol.io/specification/2025-06-18/server/tools#error-handling，检索于 2025-09-16。</mark>

---

## Other Capabilities

<mark>其他能力</mark>

In addition to Tools, the MCP specification defines five other capabilities that servers and clients can provide. As we noted above, though, only a small number of MCP implementations support these capabilities, so it remains to be seen whether they will play an important role in MCP-based deployments.

<mark>除了工具，MCP 规范还定义了服务器和客户端可以提供的另外五种能力。不过如上文所说，只有少数 MCP 实现支持这些能力，所以它们会不会在基于 MCP 的部署里扮演重要角色，还有待观察。</mark>

### Resources

<mark>资源</mark>

Resources<sup>24</sup> are a server-side capability intended to provide contextual data that can be accessed and used by the Host application. Resources provided by an MCP server might include the content of a file, a record from a database, a database schema, an image or another piece of static data information the server developers intend to be used by a client. Commonly cited examples of possible Resources include log files, configuration data, market statistics, or structured blobs such as PDFs or images. Introducing arbitrary external content into the LLM's context carries significant security risks (see below), however, so any resource consumed by an LLM client should be validated and retrieved from a trusted URL.

<mark>资源 (Resources)<sup>24</sup> 是一种服务器侧能力，用来提供宿主应用可以访问和使用的上下文数据。MCP 服务器提供的资源可以包括文件内容、数据库中的一条记录、数据库模式、图像，或服务器开发者打算让客户端使用的其他静态数据。常被举出的可能资源包括日志文件、配置数据、市场统计，或 PDF、图像这类结构化二进制块。然而，把任意外部内容引入大语言模型的上下文会带来显著的安全风险（见下文），所以大语言模型客户端消费的任何资源都应当经过校验，并从受信任的 URL 检索。</mark>

### Prompts

<mark>提示</mark>

Prompts<sup>25</sup> in MCP are another server-side capability, allowing the server to provide reusable prompt examples or templates related to its Tools and Resources. Prompts are intended to be retrieved and used by the client to interact directly with an LLM. By providing a Prompt, an MCP server can give its clients a higher-level description of how to use the tools it provides.

<mark>MCP 中的提示 (Prompts)<sup>25</sup> 是另一种服务器侧能力，允许服务器提供与其工具和资源相关的可复用提示示例或模板。提示预期由客户端检索，并用来直接与大语言模型交互。通过提供提示，MCP 服务器可以向客户端给出如何使用它所提供工具的更高层描述。</mark>

While they do have the potential to add value to an AI system, in a distributed enterprise environment the use of Prompts introduces some evident security concerns. Allowing a third-party service to inject arbitrary instructions into the execution path of the application is risky, even when filtered by classifiers, auto-raters, or other LLM-based detection methods. At the moment, our recommendation is that Prompts should be used rarely, if at all, until a stronger security model is developed.

<mark>它们确实有可能为 AI 系统增加价值，但在分布式企业环境里，使用提示会带来一些明显的安全顾虑。允许第三方服务把任意指令注入应用的执行路径是有风险的，即便经过分类器、自动评分器或其他基于大语言模型的检测方法过滤，也是如此。目前我们的建议是，在更强的安全模型出现之前，提示应当很少使用，甚至不用。</mark>

### Sampling

<mark>采样</mark>

Sampling<sup>26</sup> is a client-side capability that allows an MCP server to request an LLM completion from the client. If one of the server's capabilities needs input from an LLM, instead of implementing the LLM call and using the results internally, the server would issue a Sampling request back to the client for the client to execute. This reverses the typical flow of control, allowing a tool to leverage the Host's core AI model to perform a sub-task, such as asking the LLM to summarize a large document the server just fetched. The MCP specification recommends that clients insert a human in the loop stage in Sampling, so that there is always the option for a user to deny a server's Sampling request.

<mark>采样 (Sampling)<sup>26</sup> 是一种客户端侧能力，允许 MCP 服务器向客户端请求一次大语言模型补全。如果服务器的某项能力需要大语言模型的输入，服务器不是自己实现这次调用并在内部使用结果，而是向客户端发回一个采样请求，由客户端执行。这把典型的控制流倒了过来，让工具能利用宿主的核心 AI 模型去做一个子任务，例如请大语言模型摘要服务器刚刚取到的一份大文档。MCP 规范建议客户端在采样中插入一个人在回路 (Human-in-the-Loop) 阶段，从而始终保留用户拒绝服务器采样请求的选项。</mark>

Sampling presents both opportunities and challenges for developers. By offloading LLM calls to the client, Sampling gives client developers control over the LLM providers used in their applications, and allows costs to be borne by the application developer instead of the service provider. Sampling also gives the client developer control of any content guardrails and security filters required around the LLM call, and provides a clean way to insert a human approval step for LLM requests that occur in the application's execution path. On the other hand, like the Prompt capability, Sampling also opens an avenue for potential prompt injection in the client application. Clients should take care to filter and validate any prompt accompanying a sampling request, and should ensure that the human-in-the-loop control phase is implemented with effective controls for users to interact with the sampling request.

<mark>采样对开发者既是机会也是挑战。把大语言模型调用卸载到客户端之后，采样让客户端开发者能控制应用所用的大语言模型提供方，也让成本由应用开发者而不是服务提供方承担。采样还让客户端开发者能控制大语言模型调用周围所需的内容护栏和安全过滤器，并为执行路径上出现的大语言模型请求提供一条干净的途径来插入人工批准步骤。另一方面，和提示能力一样，采样也为客户端应用中潜在的提示注入开了一条路。客户端应当仔细过滤并校验伴随采样请求的任何提示，并确保人在回路的控制阶段实现了有效控制，让用户能够与采样请求交互。</mark>

### Elicitation

<mark>征询</mark>

Elicitation<sup>27</sup> is another client-side capability, similar to Sampling, that allows an MCP server to request additional user information from the client. Instead of requesting an LLM call, an MCP tool using Elicitation can query the host application dynamically for additional data to complete the tool request. Elicitation provides a formal mechanism for a server to pause an operation and interact with the human user via the client's UI, allowing the client to maintain control of the user interaction and data sharing, while giving the server a way to get user input.

<mark>征询 (Elicitation)<sup>27</sup> 是另一种客户端侧能力，与采样类似，允许 MCP 服务器向客户端请求额外的用户信息。使用征询的 MCP 工具不是请求一次大语言模型调用，而是可以动态向宿主应用查询额外数据，以完成工具请求。征询为服务器提供了一种正式机制，用来暂停操作，并通过客户端的界面与人类用户交互。客户端因此仍能控制用户交互和数据共享，服务器则有办法获得用户输入。</mark>

Security and privacy issues are important concerns around this capability. The MCP spec notes that "Servers MUST NOT use elicitation to request sensitive information", and that users should be clearly informed about the use of the information and able to approve, decline or cancel the request. These guidelines are critical to implementing Elicitation in a way that respects and preserves user privacy and security. The injunction against requesting sensitive information is impossible to enforce in a systematic manner, so client developers need to be vigilant about potential misuse of this capability. If a client does not provide strong guardrails around elicitation requests and a clear interface for approving or denying requests, a malicious server developer could easily extract sensitive information from the user.

<mark>围绕这一能力，安全和隐私是重要关切。MCP 规范指出：「服务器不得使用征询来请求敏感信息」，并且应当清楚地告知用户信息的用途，使用户能够批准、拒绝或取消请求。这些准则对于以尊重并保护用户隐私和安全的方式实现征询至关重要。禁止请求敏感信息这一点无法以系统化的方式强制执行，所以客户端开发者需要对这一能力的潜在滥用保持警惕。如果客户端不为征询请求提供强护栏，也不提供批准或拒绝请求的清楚界面，恶意的服务器开发者就能轻易从用户那里套取敏感信息。</mark>

### Roots

<mark>根</mark>

Roots, the third client-side capability, "define the boundaries of where servers can operate within the filesystem"<sup>28</sup>. A Root definition includes a URI that identifies the root; at the time of writing, the MCP specification restricts Root URIs to file: URIs only, but this may change in future revisions. A server receiving a Root specification from a client is expected to confine its operations just to that scope. In practice, it is not yet clear whether or how Roots would be used in a production MCP system. For one thing, there are no guardrails in the specification around the behavior of servers with respect to Roots, whether the root is a local file or another URI type. The clearest statement about this in the spec is that "servers SHOULD .. respect root boundaries during operations."<sup>29</sup> Any client developer would be wise not to rely too heavily on server behavior regarding Roots.

<mark>根 (Roots) 是第三种客户端侧能力，「定义服务器可以在文件系统中操作的边界」<sup>28</sup>。根的定义包含一个标识该根的 URI；在撰写本文时，MCP 规范把根 URI 限制为仅 file: URI，但未来修订可能会改变这一点。收到客户端根规范的服务器，预期把操作限制在该范围内。实践中，根会不会、以及如何在生产 MCP 系统里使用，还不清楚。原因之一是，规范里没有围绕服务器对根的行为设置护栏，无论根是本地文件还是另一种 URI 类型。规范里关于这一点最清楚的表述是：「服务器应当……在操作期间尊重根的边界。」<sup>29</sup> 任何客户端开发者都不宜过度依赖服务器在根方面的行为。</mark>

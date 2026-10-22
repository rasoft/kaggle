# Agentic RAG: A Critical Evolution in Retrieval-Augmented Generation

智能体式检索增强生成 (Agentic RAG)：检索增强生成的一次关键演进

A significant advancement in multi-agent architectures is Agentic Retrieval-Augmented Generation (Agentic RAG). Traditional RAG pipelines rely on a static approach—retrieving knowledge from vector databases and feeding it into an LLM for synthesis. However, this approach often fails when dealing with ambiguous, multi-step, or multi-perspective queries.

多智能体 (Multi-Agent) 架构的一项重大进展，是智能体式检索增强生成 (Agentic RAG)。传统的检索增强生成 (RAG) 流水线依赖一种静态做法——从向量数据库中检索知识，再送进大语言模型 (LLM) 去综合。然而，面对含糊的、多步骤的或多视角的查询，这种做法常常会失败。

Agentic RAG introduces autonomous retrieval agents that actively refine their search based on iterative reasoning. These agents enhance retrieval in the following ways:

智能体式 RAG 引入了自主的检索智能体 (Agent)。它们基于迭代推理 (Reasoning)，主动改进自己的搜索。这些智能体从以下几方面增强检索：

- Context-Aware Query Expansion: Instead of relying on a single search pass, agents generate multiple query refinements to retrieve more relevant and comprehensive results.

- 上下文感知的查询扩展：智能体不再依赖单次搜索，而是生成多种查询细化，以检索更相关、更全面的结果。

- Multi-Step Reasoning: Agents decompose complex queries into smaller logical steps, retrieving information sequentially to build structured responses.

- 多步推理：智能体把复杂查询分解为更小的逻辑步骤，按顺序检索信息，从而组织出有结构的回答。

- Adaptive Source Selection: Instead of fetching data from a single vector database, retrieval agents dynamically select the best knowledge sources based on context.

- 自适应的来源选择：检索智能体不再从单一向量数据库取数据，而是依据上下文动态选择最好的知识来源。

- Validation and Correction: Evaluator agents cross-check retrieved knowledge for hallucinations and contradictions before integrating it into the final response.

- 校验与纠正：评估智能体在把检索到的知识纳入最终回答之前，会交叉检查其中的幻觉和相互矛盾之处。

This approach significantly improves response accuracy, explainability, and adaptability, making it a crucial innovation for enterprises dealing with complex knowledge retrieval tasks in areas like legal research, scientific discovery, and business intelligence.

这一做法显著提高了回答的准确性、可解释性和适应性。对企业在法律研究、科学发现和商业智能等领域处理复杂的知识检索任务来说，它是一项关键创新。

---

## Agentic RAG and its Importance

智能体式 RAG 及其重要性

Agentic RAG (Retrieval-Augmented Generation) is an advanced approach that combines the strengths of RAG with the autonomy of AI agents. Traditional RAG systems retrieve relevant information from external knowledge sources to enhance LLM responses. Agentic RAG takes this a step further by employing intelligent agents to orchestrate the retrieval process, evaluate the retrieved information, and make decisions about how to best utilize it.

智能体式 RAG（检索增强生成）是一种进阶做法，把 RAG 的长处与 AI 智能体的自主性结合起来。传统 RAG 系统从外部知识来源检索相关信息，用来增强 LLM 的回答。智能体式 RAG 更进一步：用智能体来编排 (Orchestration) 检索过程，评估检索到的信息，并决定如何最好地加以利用。

Agentic RAG offers several advantages over traditional RAG:

与传统 RAG 相比，智能体式 RAG 有以下几项优势：

- Improved Accuracy: Agents can evaluate the quality of retrieved information and make decisions about which sources to trust, leading to more accurate and reliable responses.

- 准确性更高：智能体可以评估检索到的信息质量，并决定信任哪些来源，从而给出更准确、更可靠的回答。

- Enhanced Contextual Understanding: Agents can consider the context of the user's query and the retrieved information to generate more relevant and meaningful responses.

- 上下文理解更强：智能体可以同时考虑用户查询的上下文和检索到的信息，从而生成更相关、更有意义的回答。

- Increased Adaptability: Agents can adapt to changing information needs and dynamically adjust their retrieval strategies to provide the most up-to-date and relevant information. This adaptability is crucial in complex domains where information is constantly evolving, such as healthcare, finance, and legal research.

- 适应性更强：智能体可以适应不断变化的信息需求，并动态调整检索策略，以提供最新、最相关的信息。在医疗、金融和法律研究这类信息持续演变的复杂领域，这种适应性至关重要。

![Agentic RAG workflow diagram from Vectorize.io](image_012_page_35.png)

[图 9：来自 Vectorize.io 的智能体式 RAG 工作流<sup>25</sup>。标题为 Agentic RAG Workflow。左侧 Available Functions 含 Tool Functions、Action Functions、LLM Functions，以及单独标出的 Retrieval Functions。中间是 AI Agent Application：红色弯箭头标为 call function，指向左侧函数；向右送出 prompt 与可用函数（含 tools，type 为 "function"）。右侧 LLM Layer 排列 Anthropic、OpenAI、Meta 和 Google 的标识，红色弯箭头标为 function to call + function params，折回中间。下方 Persistent Knowledge 含 Graph DB、Vector DB 和 Relational DB；智能体向下的箭头标为 standard RAG retrieval，Retrieval Functions 一侧标有 JSON / REST APIs。]

Agentic RAG is particularly valuable in complex domains where information is constantly evolving, such as healthcare, finance, and legal research. For example, in healthcare, agentic RAG can help navigate complicated medical databases, research papers, and patient records, providing doctors with comprehensive and accurate information.

在信息持续演变的复杂领域，智能体式 RAG 尤其有价值，例如医疗、金融和法律研究。以医疗为例，智能体式 RAG 能帮助人们在复杂的医学数据库、研究论文和病历中穿行，为医生提供全面而准确的信息。

---

## Better Search, Better RAG

更好的搜索，更好的 RAG

Almost all RAG approaches require a search engine to index and retrieve relevant data. The introduction of agents allows for refinement of query, filtering, ranking, and the final answer. Agentic RAG agents are executing several searches to retrieve information.

几乎所有 RAG 做法都需要搜索引擎来索引并检索相关数据。引入智能体之后，就可以改进查询、过滤、排序和最终答案。智能体式 RAG 中的智能体会执行多次搜索来检索信息。

For developers who are trying to optimize existing RAG implementations, it is usually most valuable to improve search results (measured in recall) prior to introducing agents. Some of the main techniques to improve search performance are:

对想优化现有 RAG 实现的开发者来说，通常最有价值的是先改进搜索结果（以召回率 (recall) 衡量），再引入智能体。改进搜索效果的一些主要技术如下：

- Parse source documents and chunk them: Vertex AI Layout Parser can handle complex document layouts, embedded tables, and embedded images like charts, and uses a semantic chunker to keep chunks on topic with a hierarchy of headings.

- 解析源文档并分块：Vertex AI Layout Parser 能处理复杂的文档版式、内嵌表格，以及图表这类内嵌图像，并用语义分块器，借助标题层级让各个文本块保持在同一主题上。

- Add metadata to your chunks: synonyms, keywords, authors, dates, tags and categories allow your searches to boost, bury, and filter; these allow your users or your agents more control over search results.

- 为文本块添加元数据：同义词、关键词、作者、日期、标签和类别，让搜索可以提升、压低和过滤结果；用户或智能体因此能对搜索结果有更多控制。

- Fine tune the embedding model or add a search adaptor which changes embedding space: these allow the searchable index of vectors to represent your domain better than a general purpose embedding model.

- 微调嵌入模型，或加入会改变嵌入空间的搜索适配器：这样，可搜索的向量索引就能比通用嵌入模型更好地表示你的领域。

- A faster vector database can improve search quality: to search embeddings, you must make a tradeoff between speed and accuracy, upgrading to an ultra-fast Vertex AI Vector Search can improve both latency and quality.

- 更快的向量数据库可以提升搜索质量：搜索嵌入时，必须在速度和准确度之间取舍。升级到极快的 Vertex AI Vector Search 之后，延迟和质量都能得到改善。

- Use a ranker: vector searches are fast but approximate, they should return dozens or hundreds of results which need to be re-ranked by a more sophisticated system to ensure the top few results are the most relevant or best answer.

- 使用排序器：向量搜索很快，但是近似的，应当返回几十条到几百条结果，再由更精细的系统重排序，以确保最前面的几条是最相关的，或是最好的答案。

- Implement check grounding: as a safeguard on grounded generation, you can ensure each phrase is actually citable by retrieved chunks.

- 实现 check grounding：作为对依据锚定 (grounding) 生成的一道防护，你可以确保每个短语确实能被检索到的文本块引用。

![Common RAG and search components in Vertex AI Search](image_013_page_37.png)

[图 10：常见的 RAG 与搜索组件，展示 Vertex AI Search<sup>26</sup>、搜索构建 API<sup>27</sup> 和 RAG Engine<sup>28</sup>。上排括注为 Vertex AI Search is a fully managed, Google quality Search & RAG provider，流水线依次是 Collection（web、files、DBs、connectors 等）、Process & Annotate、Embed、Index / Retrieve、Rank、Generate、Validate、Serving。下排标题为 Build your own Search，依次是 Collection、Layout Parser API、Vertex Text Embeddings、Vector Search、Ranking API、Gemini API Grounding、Check Grounding API、Serving；其中 Layout Parser API、Vertex Text Embeddings、Vector Search 和 Gemini API Grounding 标有 Updates。底部横条是 RAG Engine，说明经由 Python SDK 编排，并支持许多其他组件。]

Vertex AI Search<sup>26</sup> is a powerful search engine providing Google quality search for your data and can be used with any RAG or Agentic RAG implementation. Each of the above components is automatically available within Vertex AI Search, without any development time at all. For developers who want to build their own search engine, each of the above components is exposed as a standalone API<sup>27</sup>, and RAG Engine<sup>28</sup> can orchestrate the whole pipeline easily, with a LlamaIndex-like Python-based interface.

Vertex AI Search<sup>26</sup> 是强大的搜索引擎，能为你的数据提供 Google 品质的搜索，并可与任何 RAG 或智能体式 RAG 实现一起使用。上述每个组件都自动包含在 Vertex AI Search 之中，完全不需要开发时间。想自建搜索引擎的开发者，可以把上述每个组件当作独立的 API<sup>27</sup> 来用；RAG Engine<sup>28</sup> 则能用类似 LlamaIndex 的 Python 界面，轻松编排整条流水线。

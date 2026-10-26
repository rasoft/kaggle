# Applications

应用

Large language models are revolutionizing the way we interact with and process information. With their unprecedented ability to understand context and generate content, they’re transforming numerous applications in the worlds of text, code, images, audio and video. Here we collected a few examples of application areas, but the reader should keep in mind that this is not a comprehensive list and that many new ideas are emerging continuously about how to best utilize the capabilities of these new tools. For more information about optimally building and deploying functioning applications based on the following mentioned use cases, refer to the subsequent whitepapers.

大语言模型 (LLM) 正在改变我们与信息交互、处理信息的方式。凭借理解上下文和生成内容的空前能力，它们正在改造文本、代码、图像、音频和视频世界中的许多应用。这里我们收集了几个应用领域的例子，但读者应记住：这不是一份完整清单，关于如何最好地利用这些新工具的能力，新想法在不断出现。关于如何基于下面提到的用例，最优地构建并部署能工作的应用，请参阅后续白皮书。

It is also very simple to generate text-based responses for your use case using either the Google Cloud Vertex AI SDK or the Developer focused AI studio. Snippet 3 shows code examples from these SDKs to generate responses to text prompts using the Gemini model. Note that the multimodal aspects of Gemini are covered in their respective dedicated whitepapers.

用 Google Cloud Vertex AI SDK，或面向开发者的 AI Studio，为你的用例生成基于文本的回答也非常简单。片段 3 展示来自这些 SDK 的代码示例，用 Gemini 模型 (Model) 为文本提示 (Prompt) 生成回答。注意，Gemini 的多模态方面在各自专门的白皮书里讲述。

**Python**

```python
%pip install --upgrade --quiet google-genai
import sys
if "google.colab" in sys.modules:
    from google.colab import auth

    auth.authenticate_user()
from IPython.display import HTML, Markdown, display
from google import genai
from google.genai.types import (
    FunctionDeclaration,
    GenerateContentConfig,
    GoogleSearch,
    HarmBlockThreshold,
    HarmCategory,
    MediaResolution,
    Part,
    Retrieval,
    SafetySetting,
    Tool,
    ToolCodeExecution,
    VertexAISearch,
)
import os
PROJECT_ID = "[your-project-id]"  # @param {type: "string", placeholder: "[your-project-id]", isTemplate: true}
if not PROJECT_ID or PROJECT_ID == "[your-project-id]":
    PROJECT_ID = str(os.environ.get("GOOGLE_CLOUD_PROJECT"))
LOCATION = os.environ.get("GOOGLE_CLOUD_REGION", "us-central1")
client = genai.Client(vertexai=True, project=PROJECT_ID, location=LOCATION)
MODEL_ID = "gemini-2.0-flash-001"  # @param {type: "string"}
response = client.models.generate_content(
    model=MODEL_ID, contents="What’s the largest planet in our solar system?"
)
display(Markdown(response.text))
```

**Snippet 2. Using Vertex AI and Google AI studio SDKs for unimodal text generation**

片段 2：用 Vertex AI 和 Google AI Studio 的 SDK 做单模态文本生成。

---

## Code and mathematics

代码与数学

Generative models can comprehend and generate code and algorithms to supercharge developers by assisting them across many application areas. Some of the popular use cases for code include:

生成模型能够理解并生成代码和算法，在许多应用领域协助开发者，从而增强他们的能力。代码方面一些流行的用例包括：

- Code generation: LLMs can be prompted in natural language to generate code in a specific programming language to perform certain operations. The output can be used as a draft.

- 代码生成：可以用自然语言提示大语言模型，让它用特定编程语言生成代码来完成某些操作。输出可以当作草稿。

- Code completion: LLMs can proactively suggest useful code as the user types it. This can save developers time and improve code quality.

- 代码补全：大语言模型可以在用户键入时主动建议有用的代码。这能节省开发者的时间，并提高代码质量。

- Code refactoring and debugging: LLMs can help reduce technical debt by refactoring and debugging code to improve quality, efficiency and correctness.

- 代码重构与调试：大语言模型可以通过重构和调试代码来提高质量、效率和正确性，从而帮助减少技术债。

- Code translation: LLMs can significantly help developer time and effort by helping to convert code from one programming language to another. For example, an LLM might convert Python code to Java.

- 代码翻译：大语言模型可以帮忙把代码从一种编程语言转换成另一种，从而显著节省开发者的时间和精力。例如，大语言模型可能把 Python 代码转换成 Java。

- Test case generation: LLMs can be prompted to generate unit tests for a provided codebase which saves considerable time and reduces errors.

- 测试用例生成：可以提示大语言模型为一份给定的代码库生成单元测试，这节省大量时间并减少错误。

- Code documentation and understanding: LLMs can be used in a conversational manner to engage in a natural language chat to help you understand a codebase. They can also generate appropriate comments, understand copyright status, and create release notes.

- 代码文档与理解：可以以对话方式使用大语言模型，用自然语言聊天来帮助你理解代码库。它们也可以生成合适的注释、理解版权状态，并撰写发布说明。

Recently, a number of exciting advancements have been made in the space of competitive coding and mathematics. AlphaCode 2,<sup>64</sup> combines Gemini’s reasoning capabilities with search and the use of tools to solve competitive coding problems. It receives as input a description of a problem to solve, and outputs a code solution that solves the problem. It now ranks among the top 15% competitive coders on the popular Codeforces competitive coding platform. FunSearch<sup>65</sup> uses an evolutionary procedure which is based on pairing a pre-trained LLM with a systematic evaluator. It solved the cap set problem<sup>66</sup>, an open problem in mathematics, and also discovered more efficient bin-packing algorithms which are used in many applications such as making data centers more efficient. Another recent approach called AlphaGeometry tackles the problem of finding proofs for complex geometric theorems. It comprises a neuro-symbolic system made up of a neural language model and a symbolic deduction engine. AlphaGeometry managed to solve 25 out of 30 Olympiad geometry problems, where the average human gold medalist scores on average 25.9.<sup>67</sup>

近来，竞赛编程和数学领域有若干令人兴奋的进展。AlphaCode 2<sup>64</sup> 把 Gemini 的推理 (Reasoning) 能力与搜索和工具使用结合起来，解决竞赛编程问题。它接收一份待解决问题的描述作为输入，输出解决该问题的代码。它现在位列流行的 Codeforces 竞赛编程平台上前 15% 的竞赛程序员。FunSearch<sup>65</sup> 使用一种进化过程，基于把一个预训练 (pre-training) 的大语言模型与一个系统化的评估器配对。它解决了数学中的一个开放问题——帽集问题，<sup>66</sup> 也发现了更高效的装箱算法，这类算法用于许多应用，例如让数据中心更高效。另一项近期方法称为 AlphaGeometry，处理为复杂几何定理寻找证明的问题。它由一个神经—符号系统组成，其中包括一个神经语言模型和一个符号演绎引擎。AlphaGeometry 解出了 30 道奥林匹克几何题中的 25 道，而人类金牌选手的平均得分是 25.9。<sup>67</sup>

---

## Machine translation

机器翻译

LLMs are capable of generating fluid, high-quality and contextually accurate translations. This is possible due to the LLM’s deep understanding of linguistic nuances, idioms, and context. The following are some possible real world use cases:

大语言模型能够生成流畅、高质量且在上下文上准确的译文。这之所以可能，是因为大语言模型对语言细微差别、习语和上下文有深入理解。下面是一些可能的真实用例：

- Instant messaging apps: In messaging platforms, LLMs can provide on-the-fly translations that feel natural. Unlike previous algorithms that might translate word-for-word, LLMs understand slang, colloquialisms, and regional differences, enhancing cross-language communication.

- 即时通讯应用：在通讯平台上，大语言模型可以提供感觉自然的即时翻译。与可能逐词翻译的先前算法不同，大语言模型理解俚语、口语和地区差异，从而增强跨语言沟通。

- E-commerce: On global platforms like AliExpress, product descriptions are automatically translated. LLMs help with ensuring cultural nuances and idiomatic expressions in product details are appropriately translated, leading to fewer misunderstandings.

- 电子商务：在 AliExpress 这样的全球平台上，产品描述被自动翻译。大语言模型帮助确保产品细节中的文化细微差别和习语表达被恰当地翻译，从而减少误解。

- Travel apps: In apps like Google Translate, travelers get real-time spoken translations. With LLMs, the translated conversations are smoother, making interactions in foreign countries more effortless.

- 旅行应用：在 Google 翻译这样的应用里，旅行者得到实时的口语翻译。有了大语言模型，译出的对话更顺，使在外国的交流更不费力。

---

## Text summarization

文本摘要

Text summarization is a core capability of many of the LLMs mentioned in this whitepaper. There are a number of natural potential use cases which include:

文本摘要是本白皮书提到的许多大语言模型的一项核心能力。若干自然的潜在用例包括：

- News aggregators: LLMs could craft summaries that capture not only the main events but also the sentiment and tone of the article, providing readers with a more holistic understanding.

- 新闻聚合器：大语言模型可以撰写摘要，不仅抓住主要事件，也抓住文章的情感和语气，给读者更整体的理解。

- Research databases: LLMs could help researchers generate abstracts that encapsulate the core findings and implications of scientific papers.

- 研究数据库：大语言模型可以帮助研究者生成摘要，概括科学论文的核心发现和含义。

- Chat management: In platforms like Google Chat, LLM-based systems could generate thread summaries that capture the urgency and tone, aiding users in prioritizing their responses.

- 聊天管理：在 Google Chat 这样的平台上，基于大语言模型的系统可以生成话题串摘要，抓住紧急程度和语气，帮助用户优先处理回复。

---

## Question-answering

问答

The older generation of QA systems often worked by keyword matching, frequently missing out on the contextual depth of user queries. LLMs, however, dive deep into context. They can infer user intent, traverse vast information banks, and provide answers that are contextually rich and precise. Some of the examples where this could be used include:

较老一代的问答系统常常靠关键词匹配工作，经常错过用户查询的上下文深度。大语言模型则深入上下文。它们能推断用户意图，遍历庞大的信息库，并提供在上下文上丰富而精确的答案。一些可以用到这一点的例子包括：

- Virtual assistants: LLMs can offer detailed explanations of a weather forecast considering the user’s location, time of year, and recent weather trends.

- 虚拟助手：大语言模型可以结合用户的位置、一年中的时间和近期天气趋势，对天气预报给出详细解释。

- Customer support: In business platforms, LLM-based bots could provide answers that take into account the user’s purchase history, past queries, and potential issues, offering personalized assistance.

- 客户支持：在商业平台上，基于大语言模型的机器人可以给出把用户购买历史、过往查询和潜在问题考虑进去的答案，提供个性化协助。

- Academic platforms: On academic platforms like Wolfram Alpha, LLMs could cater to user queries by understanding the depth and context of academic questions, offering answers that suit everyone from a high school student to a postgraduate researcher.

- 学术平台：在 Wolfram Alpha 这样的学术平台上，大语言模型可以通过理解学术问题的深度和上下文来回应查询，给出从高中生到研究生都合适的答案。

The quality of the generated answers, as well as the corresponding citations and sources can be significantly improved by using advanced search systems (such as those based on Retrieval Augmented Generation (RAG) architectures) to expand the prompt with relevant information, as well as post-hoc grounding after the response has been generated. Clear instructions, roles of what should and should not be used to answer the question, and advanced prompt engineering approaches (such as chain of thought and search/RAG architectures), combined with a lower temperature value amongst other things can also help greatly.

生成答案的质量，以及对应的引用和来源，可以通过使用高级搜索系统（例如基于检索增强生成（Retrieval Augmented Generation, RAG）架构的系统）来显著提高：用相关信息扩展提示，并在回答生成之后做事后的依据锚定。清晰的指令、哪些应当用于回答问题、哪些不应当的角色设定，以及高级提示工程 (Prompt Engineering) 方法（例如思维链 (chain of thought) 和搜索 / RAG 架构），再加上较低的温度 (temperature) 值等，也会有很大帮助。

---

## Chatbots

聊天机器人

Earlier chatbots followed scripted pathways, leading to ‘mechanical’ conversations. LLMs transform this space by offering dynamic, human-like interactions. They can analyze sentiment, context, and even humor, making digital conversations feel more authentic. Some examples of where this can be used include:

更早的聊天机器人遵循写好的路径，导致「机械」的对话。大语言模型通过提供动态、像人一样的交互改变了这个领域。它们能分析情感、上下文，甚至幽默，使数字对话感觉更真实。一些可以用到这一点的例子包括：

- Customer service: A chatbot on retail platforms like Zara could not only answer product-related queries but also offer fashion advice based on current trends.

- 客户服务：Zara 这样的零售平台上的聊天机器人不仅可以回答与产品相关的查询，也可以基于当前潮流提供穿衣建议。

- Entertainment: On Media LLM-driven chatbots could engage with users dynamically, reacting to live events in the stream and moderating chats with contextual understanding.

- 娱乐：在媒体上，由大语言模型驱动的聊天机器人可以动态地与用户互动，对直播流中的事件作出反应，并以对上下文的理解来主持聊天。

---

## Content generation

内容生成

Text generation isn’t new, but what LLMs bring to the table is the unprecedented ability to generate human-like text that’s contextually relevant and rich in detail. Earlier models would often lose context or coherence over longer passages. LLMs, with their vast knowledge and nuanced understanding, can craft text spanning various styles, tones, and complexities, mixing factuality with creativity (depending on the context) effectively bridging the gap between machine-generated and human-written content. The following are some real-world examples:

文本生成并不新鲜。大语言模型带来的，是生成像人写的、在上下文上相关且细节丰富的文本这一空前能力。更早的模型在更长的段落上常常失去上下文或连贯性。大语言模型凭借广博的知识和细致的理解，可以撰写跨越各种风格、语气和复杂度的文本，把事实性与创造性混合起来（视上下文而定），有效地弥合机器生成内容与人写内容之间的差距。下面是一些真实例子：

- Content creation: Platforms could utilize LLMs to help marketers develop advertisements. Instead of generic content, the LLMs could generate creative, targeted, and audience-specific messages.

- 内容创作：平台可以利用大语言模型帮助营销人员开发广告。大语言模型可以生成有创造性、有针对性、针对特定受众的信息，而不是通用内容。

- Scriptwriting: LLMs could potentially assist with producing scripts for movies or TV shows. Writers could input themes or plot points, and the model can suggest dialogues or scene descriptions, enhancing the creative process.

- 剧本写作：大语言模型有可能协助制作电影或电视剧本。写作者可以输入主题或情节点，模型可以建议对白或场景描述，从而增强创作过程。

Text generation is a wide task encompassing a variety of use cases that might range from those where correctness of the generated output is more or less important than its creativity/diversity of the language. The sampling methods and parameters like temperature should be tuned accordingly. For more information, see the prompt engineering and architecting for LLM applications whitepapers.

文本生成是一项很宽的任务，涵盖多种用例：有的用例里，生成输出的正确性比语言的创造性 / 多样性更重要或更不重要。采样 (Sampling) 方法和温度等参数应当相应调整。更多信息见提示工程白皮书，以及为大语言模型应用做架构的白皮书。

---

## Natural language inference

自然语言推理

Natural language inference (NLI) is the task of determining whether a given textual hypothesis can be logically inferred from a textual premise.

自然语言推理 (Natural Language Inference, NLI) 是这样一项任务：判断一个给定的文本假设能否从一段文本前提中逻辑地推出。

Traditional models struggled with nuanced relationships or those that require a deeper understanding of context. LLMs, with their intricate grasp of semantics and context, excel at tasks like these, bringing accuracy levels close to human performance. The following are some real-world examples:

传统模型难以处理细微的关系，或那些需要更深理解上下文的关系。大语言模型对语义和上下文有细密的把握，擅长这类任务，把准确度带到接近人的水平。下面是一些真实例子：

- Sentiment analysis: Businesses could utilize LLMs to infer customer sentiment from product reviews. Instead of just basic positive or negative tags, they could extract nuanced emotions like ‘satisfaction,’ ‘disappointment,’ or ‘elation’.

- 情感分析：企业可以利用大语言模型从产品评论中推断顾客情感。它们可以提取「满意」「失望」或「兴高采烈」这类细微情绪，而不只是基本的正面或负面标签。

- Legal document review: Law firms could employ LLMs to infer implications and intentions in contracts, ensuring there are no contradictions or potentially problematic clauses.

- 法律文书审阅：律师事务所可以雇用大语言模型来推断合同中的含义和意图，确保没有矛盾或潜在有问题的条款。

- Medical diagnoses: By analyzing patient descriptions and histories, LLMs could assist doctors in inferring potential diagnoses or health risks, ensuring early intervention.

- 医疗诊断：通过分析患者的描述和病史，大语言模型可以协助医生推断潜在诊断或健康风险，以确保早期干预。

The whitepapers on domain specific LLMs, prompt engineering, and architecting for LLM applications give further insight into these use cases.

关于领域专用大语言模型、提示工程，以及为大语言模型应用做架构的白皮书，对这些用例有进一步的阐述。

---

## Text classification

文本分类

Text classification involves categorizing text into predefined groups. While traditional algorithms were efficient, they often struggled with ambiguous or overlapping categories. LLMs, given their deep understanding of context, can classify text with higher precision, even when faced with subtle distinctions. Some examples of this include:

文本分类是把文本归入预先定义的组。传统算法效率高，但常常难以处理含糊或重叠的类别。大语言模型由于对上下文有深入理解，可以以更高的精度分类文本，即便面对细微差别。一些例子包括：

- Spam detection: Email services could utilize LLMs to classify emails as spam or legitimate. Instead of just keyword-based detection, the models understand the context and intent, potentially reducing false positives.

- 垃圾邮件检测：电子邮件服务可以利用大语言模型把邮件分为垃圾邮件或正常邮件。模型理解上下文和意图，而不只是基于关键词的检测，从而有可能减少误报。

- News categorization: News platforms could employ LLMs to categorize articles into topics like ‘technology,’ ‘politics,’ or ‘sports,’ even when articles blur the boundaries between categories.

- 新闻分类：新闻平台可以雇用大语言模型把文章归入「科技」「政治」或「体育」等主题，即便文章模糊了类别之间的边界。

- Customer feedback sorting: Businesses could analyze customer feedback through LLMs to categorize them into areas like ‘product design,’ ‘customer service,’ or ‘pricing,’ ensuring targeted responses.

- 顾客反馈分拣：企业可以通过大语言模型分析顾客反馈，把它们归入「产品设计」「客户服务」或「定价」等领域，以确保有针对性的回应。

- Evaluating LLMs as autorater: LLMs could be used to rate, compare and rank the generated outputs of other LLMs as well.

- 把大语言模型当作自动评分器来评估：大语言模型也可以用来给其他大语言模型的生成输出评分、比较和排序。

---

## Text analysis

文本分析

LLMs excel at deep text analysis – extracting patterns, understanding themes, and gleaning insights from vast textual datasets. Where traditional tools would scratch the surface, LLMs delve deep, offering rich and actionable insights. Some potential real-world examples are:

大语言模型擅长深入的文本分析：从庞大的文本数据集中提取模式、理解主题并获得洞察。传统工具只触及表面的地方，大语言模型深入进去，提供丰富且可付诸行动的洞察。一些潜在的真实例子是：

- Market research: Companies could leverage LLMs to analyze consumer conversations on social media, extracting trends, preferences, and emerging needs.

- 市场研究：公司可以利用大语言模型分析社交媒体上的消费者对话，提取趋势、偏好和正在出现的需求。

- Literary analysis: Academics could employ LLMs to understand themes, motifs, and character developments in literary works, offering fresh perspectives on classic and contemporary literature.

- 文学分析：学者可以雇用大语言模型来理解文学作品中的主题、母题和人物发展，为经典和当代文学提供新的视角。

---

## Multimodal applications

多模态应用

Multimodal LLMs, capable of processing and generating text, images, audio, and video, have opened up a new frontier in AI, offering a range of exciting and innovative applications across various sectors. The following are some examples:

能够处理和生成文本、图像、音频和视频的多模态大语言模型，在 AI 中打开了一片新的前沿，在各个部门提供一系列令人兴奋的创新应用。下面是一些例子：

Creative content generation:

创造性内容生成：

- Storytelling: An AI system could watch an image or video and spin a captivating narrative, integrating details from the visual with its knowledge base.

- 讲故事：一个 AI 系统可以观看一幅图像或一段视频，并编织一段吸引人的叙事，把视觉中的细节与它的知识库结合起来。

- Advertising and marketing: Generating targeted and emotionally resonant advertisements based on product photos or videos.

- 广告与营销：基于产品照片或视频，生成有针对性、在情感上能引起共鸣的广告。

Education and accessibility:

教育与无障碍：

- Personalized learning: Tailoring educational materials to individual learning styles by combining text with interactive visual and audio elements.

- 个性化学习：把文本与交互式的视觉和音频元素结合起来，按个人的学习风格裁剪教育材料。

- Assistive technology: Multimodal LLMs could power tools that describe images, videos, and audio for visually or hearing-impaired individuals.

- 辅助技术：多模态大语言模型可以驱动为视障或听障人士描述图像、视频和音频的工具。

Business and industry:

商业与产业：

- Document understanding and summarization: Automatically extracting key information from complex documents, combining text and visuals like invoices and contracts.

- 文档理解与摘要：从复杂文档中自动提取关键信息，把文本与视觉结合起来，例如发票和合同。

- Customer service: Multimodal chatbots can understand and respond to customer queries combining text and images, offering a richer and more personalized experience.

- 客户服务：多模态聊天机器人可以理解并回应结合了文本和图像的顾客查询，提供更丰富、更个性化的体验。

Science and research:

科学与研究：

- Medical diagnosis: Analyzing medical scans and reports together, identifying potential issues and providing insights for doctors.

- 医疗诊断：把医学扫描和报告放在一起分析，识别潜在问题，并为医生提供洞察。

- Bioinformatics and drug discovery: Integrating knowledge from diverse data sources like medical images, protein structures, and research papers to accelerate research.

- 生物信息学与药物发现：整合来自医学图像、蛋白质结构和研究论文等多样数据源的知识，以加速研究。

These examples are just the tip of the iceberg. As research progresses, the applications of multimodal LLMs are only expected to grow, transforming our daily lives in diverse and profound ways. Multimodal LLMs also benefit greatly from the existing methodologies of Unimodal LLMs (i.e., text based LLMs).

这些例子只是冰山一角。随着研究进展，多模态大语言模型的应用只会增长，以多样而深刻的方式改变我们的日常生活。多模态大语言模型也大大受益于单模态大语言模型（也就是基于文本的大语言模型）已有的方法。

LLMs, thanks to their ability to understand and process language, are reshaping how we interact with, generate, and analyze text across diverse sectors. As they continue to evolve, their applications will only grow, boosting the ability for machines and humans to have rich natural language interactions.

大语言模型凭借理解并处理语言的能力，正在重塑我们在不同部门里与文本交互、生成文本和分析文本的方式。随着它们继续演进，应用只会增长，增强机器与人进行丰富的自然语言交互的能力。

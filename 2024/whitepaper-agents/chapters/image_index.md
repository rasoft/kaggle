# Agents — Image Index

<mark>智能体 — 图片索引</mark>

Cover and contents decoration on pages 1–3 are not body figures. The Agents vs. models chart (page 8) and the Tools recap table (page 32) are vector tables, reproduced as Markdown tables in the chapter files. The 14 figures below are the raster figures placed in the chapter files.

<mark>第 1–3 页的封面和目录装饰不是正文图。第 8 页的「智能体与模型」对照和第 32 页的「工具回顾」表是矢量表格，已在章节里做成 Markdown 表。下面 14 张是放入章节的位图。</mark>

## 2. What is an agent?

<mark>2. 什么是智能体</mark>

- **image_001_page_6.png** — Figure 1, page 6

<mark>图 1，第 6 页。智能体运行时：编排（画像、目标与指令，短期与长期记忆，基于模型的推理 / 规划）、模型、工具。用户查询进入，智能体响应返回。</mark>

- **image_002_page_11.png** — Figure 2, page 11

<mark>图 2，第 11 页。编排层里的 ReAct：Question、Thought、Action、Action Input、Observation、Final Answer。工具为 Flights、Search、Code、Calc。</mark>

## 3. Tools: Extensions

<mark>3. 工具：扩展</mark>

- **image_003_page_13.png** — Figure 3, page 13

<mark>图 3，第 13 页。智能体与 Google Flights API 之间隔着一个问号：智能体怎样调用外部 API。</mark>

- **image_004_page_14.png** — Figure 4, page 14

<mark>图 4，第 14 页。扩展居中，双向连接智能体与 Google Flights API，并附带 get_flights 的用法、调用时机和参数示例。</mark>

- **image_005_page_14.png** — Figure 5, page 14

<mark>图 5，第 14 页。一个智能体（推理循环、模型、工具）对应多个扩展：Flights、Maps、Weather，各自接到对应 API。</mark>

## 4. Tools: Functions

<mark>4. 工具：函数</mark>

- **image_006_page_19.png** — Figure 7, page 19

<mark>图 7，第 19 页。智能体与函数双向连接，函数并不直接连到 Google Flights API。示例包括已知函数规格、调用说明，以及返回的 function_call JSON。</mark>

- **image_007_page_20.png** — Figure 8, page 20

<mark>图 8，第 20 页。A：扩展在智能体侧执行，一路连到 Google Flights API。B：函数留在智能体侧描述，真正的 API 调用由客户端 UI / 中间件绕回去执行。</mark>

- **image_008_page_23.png** — Figure 9, page 23

<mark>图 9，第 23 页。函数调用时序：用户、客户端 UI、智能体、模型、Google Places API。模型只生成 JSON，客户端拦截后再调用 API。</mark>

## 5. Tools: Data stores

<mark>5. 工具：数据存储</mark>

- **image_009_page_27.png** — Figure 10, page 27

<mark>图 10，第 27 页。智能体与私有文档、网站、结构化数据之间隔着一个问号。</mark>

- **image_010_page_28.png** — Figure 11, page 28

<mark>图 11，第 28 页。数据存储把智能体接到私有文档、网站和结构化数据。</mark>

- **image_011_page_29.png** — Figure 12, page 29

<mark>图 12，第 29 页。一个智能体对应多个数据存储：非结构化（入职 PDF）、网站（cloud.google.com/blog）、结构化（财务表格）。</mark>

- **image_012_page_30.png** — Figure 13, page 30

<mark>图 13，第 30 页。RAG 请求生命周期：用户查询生成嵌入，匹配向量数据库，取回内容交给智能体，再给出响应。</mark>

- **image_013_page_31.png** — Figure 14, page 31

<mark>图 14，第 31 页。带 ReAct 的 RAG 示例。用户问育儿假政策；动作为向量搜索；工具为 pdf、website、sheets 三个数据存储。</mark>

## 8. Production applications with Vertex AI agents

<mark>8. 用 Vertex AI 智能体构建生产应用</mark>

- **image_014_page_39.png** — Figure 15, page 39

<mark>图 15，第 39 页。Vertex AI 上的端到端架构：自定义 UI、智能体（提示与工具定义）、模型、函数执行环、扩展执行环、Google Places API 与向量搜索 API。</mark>

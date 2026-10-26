# Foundational Large Language Models & Text Generation

基础大语言模型与文本生成

Authors: Mohammadamin Barektain, Anant Nawalgaria, Daniel J. Mankowitz, Majd Al Merey, Yaniv Leviathan, Massimo Mascaro, Matan Kalman, Elena Buchatskaya, Aliaksei Severyn, Irina Sigler, and Antonio Gulli

作者：Mohammadamin Barektain、Anant Nawalgaria、Daniel J. Mankowitz、Majd Al Merey、Yaniv Leviathan、Massimo Mascaro、Matan Kalman、Elena Buchatskaya、Aliaksei Severyn、Irina Sigler、Antonio Gulli

February 2025

2025 年 2 月

---

## Acknowledgements

致谢

Content contributors

内容贡献者

Adam Sadvovsky

Yonghui Wu

Andrew Dai

Efi Kokiopolou

Chuck Sugnet

Aleksey Vlasenko

Erwin Huizenga

Aida Nematzadeh

Ira Ktena

Olivia Wiles

Lavi Nigam

Curators and Editors

策划与编辑

Antonio Gulli

Anant Nawalgaria

Grace Mollison

Technical Writer

技术写作

Mark Iverson

Designer

设计师

Michael Lanning

---

## Table of contents

目录

Introduction — 6

引言 — 6

Why language models are important — 7

语言模型为什么重要 — 7

Large language models — 8

大语言模型 — 8

Transformer — 9

Transformer — 9

Input preparation and embedding — 11

输入准备与嵌入 — 11

Multi-head attention — 12

多头注意力 — 12

Understanding self-attention — 12

理解自注意力 — 12

Multi-head attention: power in diversity — 14

多头注意力：多样性带来的能力 — 14

Layer normalization and residual connections — 15

层归一化与残差连接 — 15

Feedforward layer — 15

前馈层 — 15

Encoder and decoder — 16

编码器与解码器 — 16

Mixture of Experts (MoE) — 17

混合专家 (MoE) — 17

Training the transformer — 20

训练 Transformer — 20

Data preparation — 21

数据准备 — 21

Training and loss function — 21

训练与损失函数 — 21

The evolution of transformers — 23

Transformer 的演进 — 23

GPT-1 — 23

GPT-1 — 23

BERT — 25

BERT — 25

GPT-2 — 25

GPT-2 — 25

GPT-3/3.5/4 — 27

GPT-3/3.5/4 — 27

LaMDA — 28

LaMDA — 28

Gopher — 29

Gopher — 29

GLaM — 31

GLaM — 31

Chinchilla — 31

Chinchilla — 31

PaLM — 33

PaLM — 33

PaLM 2 — 33

PaLM 2 — 33

Gemini — 34

Gemini — 34

Gemma — 37

Gemma — 37

LLaMA — 38

LLaMA — 38

Mixtral — 39

Mixtral — 39

OpenAI O1 — 40

OpenAI O1 — 40

DeepSeek — 40

DeepSeek — 40

Other open models — 41

其他开放模型 — 41

Comparison — 43

比较 — 43

Fine-tuning large language models — 45

微调大语言模型 — 45

Supervised fine-tuning — 46

监督微调 — 46

Reinforcement learning from human feedback — 47

基于人类反馈的强化学习 — 47

Parameter Efficient Fine-Tuning — 49

参数高效微调 — 49

Using large language models — 52

使用大语言模型 — 52

Prompt engineering — 52

提示工程 — 52

Sampling Techniques and Parameters — 53

采样技术与参数 — 53

Task-based Evaluation — 54

面向任务的评估 — 54

Accelerating inference — 57

加速推断 — 57

Trade offs — 58

权衡 — 58

The Quality vs Latency/Cost Tradeoff — 58

质量与延迟 / 成本的权衡 — 58

The Latency vs Cost Tradeoff — 59

延迟与成本的权衡 — 59

Output-approximating methods — 60

近似输出的方法 — 60

Quantization — 60

量化 — 60

Distillation — 61

蒸馏 — 61

Output-preserving methods — 62

保持输出的方法 — 62

Flash Attention — 63

Flash Attention — 63

Prefix Caching — 63

前缀缓存 — 63

Speculative Decoding — 65

推测解码 — 65

Batching and Parallelization — 67

批处理与并行 — 67

Applications — 68

应用 — 68

Code and mathematics — 71

代码与数学 — 71

Machine translation — 72

机器翻译 — 72

Text summarization — 73

文本摘要 — 73

Question-answering — 73

问答 — 73

Chatbots — 74

聊天机器人 — 74

Content generation — 75

内容生成 — 75

Natural language inference — 75

自然语言推理 — 75

Text classification — 76

文本分类 — 76

Text analysis — 77

文本分析 — 77

Multimodal applications — 78

多模态应用 — 78

Summary — 80

总结 — 80

Endnotes — 82

尾注 — 82

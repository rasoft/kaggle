# Prompt Engineering

提示工程 (Prompt Engineering)

Author: Lee Boonstra

作者：Lee Boonstra

February 2025

2025 年 2 月

---

## Acknowledgements

致谢

Content contributors

内容贡献者

Michael Sherman

Yuan Cao

Erick Armbrust

Anant Nawalgaria

Antonio Gulli

Simone Cammel

Curators and Editors

策划与编辑

Antonio Gulli

Anant Nawalgaria

Grace Mollison

Technical Writer

技术写作

Joey Haymaker

Designer

设计师

Michael Lanning

---

## Table of contents

目录

Introduction — 6

引言 — 6

Prompt engineering — 7

提示工程 — 7

LLM output configuration — 8

大语言模型输出配置 — 8

Output length — 8

输出长度 — 8

Sampling controls — 9

采样控制 — 9

Temperature — 9

温度 — 9

Top-K and top-P — 10

Top-K 与 top-P — 10

Putting it all together — 11

合在一起看 — 11

Prompting techniques — 13

提示技巧 — 13

General prompting / zero shot — 13

一般提示 / 零样本 — 13

One-shot & few-shot — 15

单样本与少样本 — 15

System, contextual and role prompting — 18

系统提示、上下文提示与角色提示 — 18

System prompting — 19

系统提示 — 19

Role prompting — 21

角色提示 — 21

Contextual prompting — 23

上下文提示 — 23

Step-back prompting — 25

后退提示 — 25

Chain of Thought (CoT) — 29

思维链 (Chain of Thought, CoT) — 29

Self-consistency — 32

自洽 (Self-consistency) — 32

Tree of Thoughts (ToT) — 36

思维树 (Tree of Thoughts, ToT) — 36

ReAct (reason & act) — 37

推理与行动 (Reason and Act, ReAct) — 37

Automatic Prompt Engineering — 40

自动提示工程 (Automatic Prompt Engineering) — 40

Code prompting — 42

代码提示 — 42

Prompts for writing code — 42

用于写代码的提示 — 42

Prompts for explaining code — 44

用于解释代码的提示 — 44

Prompts for translating code — 46

用于翻译代码的提示 — 46

Prompts for debugging and reviewing code — 48

用于调试和审阅代码的提示 — 48

What about multimodal prompting? — 54

多模态提示呢？ — 54

Best Practices — 54

最佳实践 — 54

Provide examples — 54

提供示例 — 54

Design with simplicity — 55

设计要简单 — 55

Be specific about the output — 56

把输出说具体 — 56

Use Instructions over Constraints — 56

优先用指令，而不是约束 — 56

Control the max token length — 58

控制最大词元长度 — 58

Use variables in prompts — 58

在提示里使用变量 — 58

Experiment with input formats and writing styles — 59

试验输入格式和写法 — 59

For few-shot prompting with classification tasks, mix up the classes — 59

分类任务的少样本提示要把类别打乱 — 59

Adapt to model updates — 60

适应模型更新 — 60

Experiment with output formats — 60

试验输出格式 — 60

JSON Repair — 61

JSON 修复 — 61

Working with Schemas — 62

使用模式 — 62

Experiment together with other prompt engineers — 63

和其他提示工程师一起试验 — 63

CoT Best practices — 64

思维链最佳实践 — 64

Document the various prompt attempts — 64

记录各次提示尝试 — 64

Summary — 66

总结 — 66

Endnotes — 68

尾注 — 68

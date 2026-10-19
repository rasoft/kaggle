# Prompt Engineering

<mark>提示工程 (Prompt Engineering)</mark>

Author: Lee Boonstra

<mark>作者：Lee Boonstra</mark>

February 2025

<mark>2025 年 2 月</mark>

---

## Acknowledgements

<mark>致谢</mark>

Content contributors

<mark>内容贡献者</mark>

Michael Sherman

Yuan Cao

Erick Armbrust

Anant Nawalgaria

Antonio Gulli

Simone Cammel

Curators and Editors

<mark>策划与编辑</mark>

Antonio Gulli

Anant Nawalgaria

Grace Mollison

Technical Writer

<mark>技术写作</mark>

Joey Haymaker

Designer

<mark>设计师</mark>

Michael Lanning

---

## Table of contents

<mark>目录</mark>

Introduction — 6

<mark>引言 — 6</mark>

Prompt engineering — 7

<mark>提示工程 — 7</mark>

LLM output configuration — 8

<mark>大语言模型输出配置 — 8</mark>

Output length — 8

<mark>输出长度 — 8</mark>

Sampling controls — 9

<mark>采样控制 — 9</mark>

Temperature — 9

<mark>温度 — 9</mark>

Top-K and top-P — 10

<mark>Top-K 与 top-P — 10</mark>

Putting it all together — 11

<mark>合在一起看 — 11</mark>

Prompting techniques — 13

<mark>提示技巧 — 13</mark>

General prompting / zero shot — 13

<mark>一般提示 / 零样本 — 13</mark>

One-shot & few-shot — 15

<mark>单样本与少样本 — 15</mark>

System, contextual and role prompting — 18

<mark>系统提示、上下文提示与角色提示 — 18</mark>

System prompting — 19

<mark>系统提示 — 19</mark>

Role prompting — 21

<mark>角色提示 — 21</mark>

Contextual prompting — 23

<mark>上下文提示 — 23</mark>

Step-back prompting — 25

<mark>后退提示 — 25</mark>

Chain of Thought (CoT) — 29

<mark>思维链 (Chain of Thought, CoT) — 29</mark>

Self-consistency — 32

<mark>自洽 (Self-consistency) — 32</mark>

Tree of Thoughts (ToT) — 36

<mark>思维树 (Tree of Thoughts, ToT) — 36</mark>

ReAct (reason & act) — 37

<mark>推理与行动 (Reason and Act, ReAct) — 37</mark>

Automatic Prompt Engineering — 40

<mark>自动提示工程 (Automatic Prompt Engineering) — 40</mark>

Code prompting — 42

<mark>代码提示 — 42</mark>

Prompts for writing code — 42

<mark>用于写代码的提示 — 42</mark>

Prompts for explaining code — 44

<mark>用于解释代码的提示 — 44</mark>

Prompts for translating code — 46

<mark>用于翻译代码的提示 — 46</mark>

Prompts for debugging and reviewing code — 48

<mark>用于调试和审阅代码的提示 — 48</mark>

What about multimodal prompting? — 54

<mark>多模态提示呢？ — 54</mark>

Best Practices — 54

<mark>最佳实践 — 54</mark>

Provide examples — 54

<mark>提供示例 — 54</mark>

Design with simplicity — 55

<mark>设计要简单 — 55</mark>

Be specific about the output — 56

<mark>把输出说具体 — 56</mark>

Use Instructions over Constraints — 56

<mark>优先用指令，而不是约束 — 56</mark>

Control the max token length — 58

<mark>控制最大词元长度 — 58</mark>

Use variables in prompts — 58

<mark>在提示里使用变量 — 58</mark>

Experiment with input formats and writing styles — 59

<mark>试验输入格式和写法 — 59</mark>

For few-shot prompting with classification tasks, mix up the classes — 59

<mark>分类任务的少样本提示要把类别打乱 — 59</mark>

Adapt to model updates — 60

<mark>适应模型更新 — 60</mark>

Experiment with output formats — 60

<mark>试验输出格式 — 60</mark>

JSON Repair — 61

<mark>JSON 修复 — 61</mark>

Working with Schemas — 62

<mark>使用模式 — 62</mark>

Experiment together with other prompt engineers — 63

<mark>和其他提示工程师一起试验 — 63</mark>

CoT Best practices — 64

<mark>思维链最佳实践 — 64</mark>

Document the various prompt attempts — 64

<mark>记录各次提示尝试 — 64</mark>

Summary — 66

<mark>总结 — 66</mark>

Endnotes — 68

<mark>尾注 — 68</mark>

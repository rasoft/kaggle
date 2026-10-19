# 4. Evaluating Skills

<mark>4. 评估技能</mark>

Now you have a first skill, or maybe a small library of them. The question that immediately follows is: how do you know they actually work? How skills fail, how to test them, and the four conditions every skill should pass before it earns a place in your library.

<mark>现在你有了第一个技能 (Skill)，或者已经有了一个小技能库。紧接着的问题是：你怎么知道它们真的管用？技能会怎么失败，怎么测试它们，以及每个技能在库里占有一席之地之前，应该通过的四个条件。</mark>

> An Agent Skill without a test is a hope, not a capability.

<mark>没有测试的智能体技能 (Agent Skill) 只是一种希望，不是一种能力。</mark>

When researchers recently benchmarked 84 real-world agent tasks in SkillsBench (2025)<sup>7</sup>, they found that 19% performed worse with a skill than without one. These poorly designed skills were not just neutral noise, they actively degraded capability. Fortunately, these failures are predictable and fall into four distinct modes:

<mark>研究者最近在 SkillsBench（2025）<sup>7</sup> 上基准测试了 84 个真实世界的智能体 (Agent) 任务，发现其中 19% 在有技能时比没有技能更差。这些设计拙劣的技能不只是中性噪声，它们会主动削弱能力。好在这些失败是可预测的，并落进四种不同模式：</mark>

1. Trigger Failure: The wrong skill fires, or the correct one fails to fire.

<mark>1. 触发失败 (Trigger Failure)：错误的技能开火了，或者正确的那个没有开火。</mark>

2. Execution Failure: The skill triggers correctly, but produces incorrect output or errant tool calls.

<mark>2. 执行失败 (Execution Failure)：技能触发正确，但产出了错误输出，或发出了偏离的工具 (Tools) 调用。</mark>

3. Token Budget Failure: A massive skill body crowds the context window, degrading performance on unrelated turns.

<mark>3. Token 预算失败 (Token Budget Failure)：庞大的技能正文挤占上下文窗口，让无关轮次的表现下降。</mark>

4. Regression: A newly added skill overlaps with an existing one, breaking previously working routing.

<mark>4. 回归 (Regression)：新加的技能和已有技能重叠，弄坏了原本能用的路由。</mark>

Trigger failures surface in routing logs; execution failures in output quality; token budget failures under realistic context load; regression failures only when the full library is exercised together.

<mark>触发失败出现在路由日志里；执行失败出现在输出质量里；token 预算失败出现在真实的上下文负载下；回归失败只有在整个技能库一起被操练时才会出现。</mark>

![Four failure modes of Agent Skills](image_001_page_19.png)

<mark>[图片_001：智能体技能的四种失败模式 - 第 19 页]</mark>

Figure 1: Notice how the failure modes branch out. Trigger and execution failures happen on a single-turn level, while token budget and regression failures only appear when multiple skills interact under a heavy production load.

<mark>图 1：注意失败模式如何分叉。触发失败和执行失败发生在单轮层面，而 token 预算失败和回归失败，只有在多个技能于沉重的生产负载下相互作用时才会出现。</mark>

---

## The Evaluation Toolkit

<mark>评估工具箱</mark>

Five complementary testing patterns cover the full failure surface.

<mark>五种互补的测试模式，覆盖完整的失败面。</mark>

| Pattern | Description | Example | Failure Mode Addressed | When Required |
| --- | --- | --- | --- | --- |
| Eval-as-Unit-Test | Test file for the skill running in CI on every change | Three JSON eval cases run via agenteval on every push; a failing test blocks merges | All | Every skill, every change |
| Golden Dataset | Curated, versioned (input, expected output) pairs stored with the skill | 30 representative queries with expected tool calls/formats committed in the skill directory | Execution, Trigger | Draft tier and above |
| LLM-as-Judge | A peer model evaluates output against a rubric at scale | Reference-guided scoring across three rubric dimensions, run twice with swapped positions to neutralize ordering bias | Execution | Read-only and draft |
| Adversarial / Red-Team | Systematic probing designed to expose failure modes | One rephrasing and one negative boundary case for every positive trigger; agentregress flags regressions | Trigger, Execution | Before action-allowed graduation |
| Canary / Shadow Mode | Deployment to controlled traffic before full rollout | Shadow: Parallel offline comparison. Canary: 1% live traffic monitored via selftune for 24 hours | Regression | Before each action-allowed release |

<mark>表 1：评估工具箱。五种互补的测试模式，用来覆盖智能体技能的完整失败面。</mark>

| <mark>模式</mark> | <mark>说明</mark> | <mark>示例</mark> | <mark>针对的失败模式</mark> | <mark>何时必需</mark> |
| --- | --- | --- | --- | --- |
| <mark>单元测试式评估 (Eval-as-Unit-Test)</mark> | <mark>技能的测试文件，每次变更都在 CI 中运行</mark> | <mark>每次推送用 agenteval 跑 3 个 JSON 评估用例；失败的测试会挡住合并</mark> | <mark>全部</mark> | <mark>每个技能，每次变更</mark> |
| <mark>黄金数据集 (Golden Dataset)</mark> | <mark>与技能一起存放的、经过整理并版本化的（输入，期望输出）对</mark> | <mark>30 条有代表性的查询，带期望的工具调用和格式，提交在技能目录里</mark> | <mark>执行、触发</mark> | <mark>草稿层及以上</mark> |
| <mark>大模型即评委 (LLM-as-Judge)</mark> | <mark>一个对等模型按量规大规模评估输出</mark> | <mark>沿三个量规维度做参照引导打分，交换位置再跑一次，以抵消顺序偏差</mark> | <mark>执行</mark> | <mark>只读 (Read-Only) 与草稿</mark> |
| <mark>对抗 / 红队 (Adversarial / Red-Team)</mark> | <mark>系统性探测，用来暴露失败模式</mark> | <mark>每个正向触发配一条改写和一条负向边界用例；agentregress 标记回归</mark> | <mark>触发、执行</mark> | <mark>在允许执行 (Action-Allowed) 晋级之前</mark> |
| <mark>金丝雀 / 影子模式 (Canary / Shadow Mode)</mark> | <mark>全量发布前，先部署到受控流量</mark> | <mark>影子：并行的离线对比。金丝雀：1% 线上流量，经 selftune 监控 24 小时</mark> | <mark>回归</mark> | <mark>每次允许执行的发布之前</mark> |

Table 1: The Evaluation Toolkit, outlining five complementary testing patterns designed to cover the full failure surface of Agent Skills.

<mark>表 1：评估工具箱，列出五种互补的测试模式，用来覆盖智能体技能的完整失败面。</mark>

---

## The trigger is the first gate

<mark>触发是第一道门</mark>

![Metadata as a thin routing layer](image_002_page_21.png)

<mark>[图片_002：元数据作为薄路由层 - 第 21 页]</mark>

Figure 2: This visual highlights the gatekeeping mechanism. The metadata acts as a thin routing layer, keeping the active token count low until the specific activation cues match the user intent.

<mark>图 2：这张图突出门禁机制。元数据充当一层薄路由，把活跃 token 数压低，直到具体的激活线索匹配用户意图。</mark>

A skill that never fires cannot help. A skill that fires too broadly injects irrelevant context. Vercel's production analysis<sup>8</sup> revealed a 56% non-invocation rate for skills expected to activate consistently. More critically, a skill stripped of its instructions scored 58%, while the agent without the skill scored 63%. This 5-point deficit demonstrates that a poorly-designed skill can actively subtract capability.

<mark>从不触发的技能帮不上忙。触发面太宽的技能会注入无关上下文。Vercel 的生产分析<sup>8</sup> 显示，那些本该稳定激活的技能有 56% 的未调用率。更关键的是，被剥掉指令的技能得了 58%，而没有该技能的智能体得了 63%。这 5 分的缺口说明，设计拙劣的技能会主动减去能力。</mark>

In this same study, Vercel also noted that a passive AGENTS.md index of project conventions achieved a 100% pass rate against a 53% baseline. This reinforces that skills are best reserved for narrow, action-specific workflows, whereas global context should remain in passive, always-accessible documentation.

<mark>同一项研究里，Vercel 还指出，一份被动的、记录项目约定的 AGENTS.md 索引，相对 53% 的基线达到了 100% 的通过率。这强化了一点：技能最好留给窄的、针对具体动作的工作流；全局上下文应留在被动的、始终可访问的文档里。</mark>

Now, to hit the industry-standard 90% trigger accuracy rate, your SKILL.md description, the only thing the model sees during routing, must pass four checks:

<mark>要把触发准确率打到行业标准的 90%，你的 SKILL.md description——模型在路由时唯一能看到的东西——必须通过四项检查：</mark>

- Testable specificity: You must write 3 positive and 3 negative triggers.

<mark>可测试的具体性：你必须写下 3 个正向触发和 3 个负向触发。</mark>

- Clarity: Ambiguous queries don't overlap with adjacent skills.

<mark>清晰：含糊的查询不会和相邻技能重叠。</mark>

- Execution fidelity: It describes actual performance, not aspirational behavior.

<mark>执行保真：它描述的是实际表现，不是愿望中的行为。</mark>

- Rephrasing stability: It routes consistently regardless of how the user phrases the intent.

<mark>改写稳定性：无论用户怎么表述意图，路由都保持一致。</mark>

---

## Output quality and tool trajectory

<mark>输出质量与工具轨迹 (tool trajectory)</mark>

Once a skill triggers, test both the final output (what the agent says) and the tool trajectory (what the agent does) separately.

<mark>技能一旦触发，就要把最终输出（智能体说了什么）和工具轨迹（智能体做了什么）分开测试。</mark>

A smart way to do this is to use the Evaluation-Driven Development (EDD). Invert the workflow by writing three JSON evaluation cases (Input, Expected Tools, Expected Output) before drafting the SKILL.md. It forces a clear functional spec upfront. When using LLM-as-Judge to score outputs at scale, remember two non-negotiables: swap the positions of the reference and actual outputs to eliminate ordering bias, and calibrate against human ratings until you hit 90% agreement.

<mark>一个聪明的做法是采用评估驱动开发 (Evaluation-Driven Development, EDD)。把工作流倒过来：在起草 SKILL.md 之前，先写 3 个 JSON 评估用例（输入、期望工具、期望输出）。这会迫使你事先写清功能规格。用大模型即评委大规模给输出打分时，有两件不能让步：交换参照输出和实际输出的位置，以消除顺序偏差；并对照人工评分校准，直到一致率达到 90%。</mark>

Latitude's analysis (March 2026)<sup>9</sup> found that final-output-only scoring passes 20% to 40% more cases than trajectory-aware scoring. This gap represents instances where the agent reached the correct answer via an incorrect sequence of tool calls. Acceptable in read-only scenarios. Critical in action-allowed skills, where incorrect tool trajectories can cause irreversible side effects.

<mark>Latitude 的分析（2026 年 3 月）<sup>9</sup> 发现，只看最终输出的打分，比带轨迹意识的打分多通过 20% 到 40% 的用例。这个缺口代表的是：智能体通过错误的工具调用序列，到达了正确答案。在只读场景里这可以接受。在允许执行的技能里这很关键，错误的工具轨迹会造成不可逆的副作用。</mark>

The Google ADK eval framework<sup>10</sup> offers three trajectory scoring modes: EXACT (exact order), IN_ORDER (ordered subset), and ANY_ORDER (unordered subset). Trajectory validation should align with the skill tier: read-only skills can use ANY_ORDER, action-allowed skills require IN_ORDER or EXACT.

<mark>Google ADK 评估框架<sup>10</sup> 提供三种轨迹评分模式：EXACT（精确顺序）、IN_ORDER（有序子集）和 ANY_ORDER（无序子集）。轨迹校验应对齐技能层级：只读技能可以用 ANY_ORDER，允许执行的技能需要 IN_ORDER 或 EXACT。</mark>

![Evaluation-driven development inversion path](image_003_page_23.png)

<mark>[图片_003：评估驱动开发的倒置路径 - 第 23 页]</mark>

Figure 3: Follow the inversion path. Instead of writing code first, the workflow forces you to define expected tool trajectories and evaluation rubrics as the very first step.

<mark>图 3：沿着这条倒置路径走。工作流迫使你把定义期望的工具轨迹和评估量规作为第一步，而不是先写代码。</mark>

---

## System vs. Skill: The Evaluation Illusion

<mark>系统与技能：评估错觉</mark>

Trajectory testing evaluates the composite system of the host agent interacting with the skill rather than the skill in isolation. When a multi-skill trajectory fails, it is often impossible to decouple agent routing, instruction quality, or execution fidelity. To simplify calibration, evaluate skills via a "Single-Skill Sub-Agent pattern" (Agent + 1 Skill vs. Base Agent); save complex multi-skill co-loading for advanced production staging.

<mark>轨迹测试评估的是宿主智能体与技能交互的复合系统，而不是孤立的技能。一条多技能轨迹失败时，往往无法把智能体路由、指令质量和执行保真拆开。为了简化校准，用「单技能子智能体模式」来评估技能（智能体 + 1 个技能，对比基础智能体）；把复杂的多技能共同加载 (co-load) 留到更靠后的生产预发。</mark>

Evaluation-Driven Development (EDD)<sup>11</sup> inverts the workflow by writing three JSON evaluation cases (Input, Expected Tools, Expected Output) before drafting the SKILL.md. It forces a clear functional spec upfront. This forces a clear functional specification upfront. A minimal eval case looks like this:

<mark>评估驱动开发 (EDD)<sup>11</sup> 把工作流倒过来：在起草 SKILL.md 之前先写 3 个 JSON 评估用例（输入、期望工具、期望输出）。这会迫使你事先写清功能规格。一个最小评估用例如下：</mark>

```json
{
  "case_id": "refund_dup_charge_001",
  "input": "I was charged twice for order #4521 last Tuesday",
  "expected_skill": "refund_processor",
  "expected_tool_calls": [
    {"tool": "lookup_order", "args": {"order_id": "4521"}},
    {"tool": "check_duplicate_charge", "args": {"order_id": "4521"}}
  ],
  "expected_output_format": "confirmation_with_refund_id",
  "rubric": ["acknowledges duplicate", "cites order id", "provides next step"]
}
```

Snippet 3: A minimal JSON evaluation case example used in Evaluation-Driven Development (EDD) to explicitly define input parameters, expected tool trajectories, and evaluation rubrics upfront.

<mark>代码片段 3：评估驱动开发 (EDD) 中的一个最小 JSON 评估用例，用来事先明确输入参数、期望的工具轨迹和评估量规。</mark>

<mark>字段含义：case_id 为 refund_dup_charge_001。输入是「上周二订单 #4521 被扣了两次款」。期望技能是 refund_processor。期望工具调用是 lookup_order 与 check_duplicate_charge，参数 order_id 均为 4521。期望输出格式是带退款编号的确认。量规是：承认重复扣款、引用订单号、给出下一步。</mark>

Drafting three such cases upfront surfaces description ambiguities and tool-trajectory errors before they compound in the skill body.

<mark>事先起草三个这样的用例，能在描述歧义和工具轨迹错误堆进技能正文之前，就把它们暴露出来。</mark>

When using LLM-as-Judge to score outputs at scale, remember two non-negotiables: swap the positions of the reference and actual outputs to eliminate ordering bias, and calibrate against human ratings until you hit 90% agreement.

<mark>用大模型即评委大规模给输出打分时，记住两件不能让步的事：交换参照输出和实际输出的位置，以消除顺序偏差；并对照人工评分校准，直到一致率达到 90%。</mark>

---

## Token budget: isolation is a trap

<mark>Token 预算：孤立评估是个陷阱</mark>

Never evaluate a skill purely in isolation. Agents in production co-load 5 to 15 skills simultaneously. A skill body exceeding 5,000 tokens might work perfectly alone, but it will cause context rot when co-loaded.

<mark>永远不要纯粹孤立地评估一个技能。生产中的智能体会同时共同加载 5 到 15 个技能。一份超过 5,000 token 的技能正文，单独跑可能完美，共同加载时却会造成上下文腐烂。</mark>

The Compound Evaluation Trap: Skill vs. Agent

<mark>复合评估陷阱：技能对比智能体</mark>

Trajectory testing evaluates the composite system. The skill and the host agent together. If a test fails, avoid over-engineering the 'SKILL.md' for a specific model, which ruins portability. Instead, isolate execution logic from routing by using a "Two-Tiered Assert Framework": validate underlying tool code independently, and audit `SKILL.md` triggers across multiple model families to catch brittle, architecture-locked descriptions.

<mark>轨迹测试评估的是复合系统，也就是技能和宿主智能体一起。如果测试失败，不要为某一个模型把 SKILL.md 过度工程化，那会毁掉可移植性。反过来，用「两层断言框架」把执行逻辑和路由拆开：独立验证底层工具代码，并跨多个模型家族审计 SKILL.md 的触发，以抓住脆弱的、锁死在某一种架构上的描述。</mark>

MCPVerse<sup>12</sup> noted an 18.2% accuracy drop in Claude-4-Sonnet due to tool proliferation and context attention competition. Additionally, Chroma Research (2025)<sup>13</sup> found that all frontier models degrade as input grows, particularly when hindered by co-loaded noise.

<mark>MCPVerse<sup>12</sup> 指出，由于工具增殖和上下文注意力竞争，Claude-4-Sonnet 的准确率下降了 18.2%。此外，Chroma Research（2025）<sup>13</sup> 发现，所有前沿模型都会随着输入变长而变差，在共同加载的噪声妨碍时尤其如此。</mark>

![Performance gap between one skill and fifteen co-loaded skills](image_004_page_26.png)

<mark>[图片_004：单个技能与 15 个共同加载技能的性能差距 - 第 26 页]</mark>

Figure 4: Look at the performance gap between a single running skill and 15 co-loaded skills. The curve illustrates why passing an isolated test is a false positive for production readiness.

<mark>图 4：看单个正在运行的技能与 15 个共同加载技能之间的性能差距。这条曲线说明，为什么通过孤立测试对生产就绪来说是假阳性。</mark>

Because of this, skills must graduate through strict tiers of authority:

<mark>因此，技能必须沿着严格的权限层级晋级：</mark>

- Read-Only: LLM-as-Judge eval; 90% trigger accuracy.

<mark>只读 (Read-Only)：大模型即评委评估；触发准确率 90%。</mark>

- Draft-Only (Human Review): Golden dataset of 20+ cases; human approval.

<mark>仅草稿 (Draft-Only)（人工审阅）：20 个以上用例的黄金数据集；人工批准。</mark>

- Action-Allowed: Full adversarial red-teaming; sustained success across multiple runs (not just a single lucky pass); no rollback events; sustained pass^k.

<mark>允许执行 (Action-Allowed)：完整的对抗性红队测试；多次运行持续成功（不只是一次侥幸通过）；没有回滚事件；持续的 pass^k。</mark>

pass^k measures consistent, rather than occasional, success by running the evaluation k times and requiring success on every run. On tau-bench (Yao et al., 2024)<sup>14</sup>, GPT-4o scored 61% on pass^1 but dropped below 25% on pass^8, demonstrating that single-run success is a poor predictor of production reliability.

<mark>pass^k 衡量的是稳定成功，而不是偶尔成功：把评估跑 k 次，并要求每一次都成功。在 tau-bench（Yao 等人，2024）<sup>14</sup> 上，GPT-4o 的 pass^1 是 61%，但 pass^8 掉到 25% 以下。这说明单次运行成功很难预测生产可靠性。</mark>

When calibrating these thresholds, two factors are critical:

<mark>校准这些阈值时，有两个因素很关键：</mark>

1. Production Degradation: ReliabilityBench<sup>15</sup> shows that production performance typically drops 20% to 30% compared to offline benchmark pass@1 numbers.

<mark>1. 生产降级：ReliabilityBench<sup>15</sup> 表明，生产表现通常比离线基准的 pass@1 数字低 20% 到 30%。</mark>

2. Simulation Bias: Simulation-based evaluations can suffer from an optimistic bias of up to 9% (the "Lost in Simulation"<sup>16</sup> finding).

<mark>2. 仿真偏差：基于仿真的评估可能有最高 9% 的乐观偏差（「迷失在仿真中」，Lost in Simulation<sup>16</sup> 的发现）。</mark>

Consequently, human review of representative outputs remains the ultimate validation signal for action-allowed graduation.

<mark>因此，对有代表性的输出做人工审阅，仍然是允许执行晋级的最终验证信号。</mark>

---

## What "eval coverage" means

<mark>「评估覆盖」是什么意思</mark>

A skill achieves complete eval coverage by satisfying four conditions mapped directly to the primary failure modes:

<mark>一个技能要达到完整的评估覆盖，需要满足直接映射到主要失败模式的四个条件：</mark>

- Trigger Failure: Verifying trigger behavior with both positive (should fire) and negative (should not fire) test cases.

<mark>触发失败：用正向（应该触发）和负向（不应该触发）测试用例验证触发行为。</mark>

- Execution Failure: Ensuring correct outputs across a representative range of expected inputs.

<mark>执行失败：在有代表性的期望输入范围内，确保输出正确。</mark>

- Regression: Confirming that adding the skill causes zero performance drops in the existing library.

<mark>回归：确认加入该技能后，现有技能库的表现零下降。</mark>

- Token Budget Failure: Bounding the skill's token footprint to ensure it does not degrade performance on unrelated turns.

<mark>Token 预算失败：给技能的 token 占用设上限，确保它不会拉低无关轮次的表现。</mark>

This checklist governs graduation; failure on any single condition holds the skill in the draft tier, regardless of its happy-path performance. Once verified, the skill and its accompanying eval suite are ready for production deployment (detailed in Section 5).

<mark>这份清单决定能否晋级。任何一个条件失败，技能就留在草稿层，不管它在顺利路径上表现多好。验证通过后，技能和配套的评估套件就可以进入生产部署（详见第 5 节）。</mark>

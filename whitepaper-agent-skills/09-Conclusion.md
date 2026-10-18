# 9. Conclusion

<mark>9. 结论</mark>

We began this whitepaper by looking at a surprisingly simple concept: a folder containing a markdown file and a few optional scripts. Yet, this lightweight structure, the Agent Skill, is fundamentally reshaping how we build AI Agents. It finally provides foundation models with true, testable procedural memory, allowing them to remember how to execute tasks step-by-step. By relying on the magic of progressive disclosure, skills solve the problem of context rot. A single, general-purpose agent can now seamlessly access many specialized workflows without choking its token budget.

<mark>这份白皮书从一个简单得惊人的概念开始：一个文件夹，里面有一个 Markdown 文件和几份可选脚本。然而，这个轻量结构——智能体技能 (Agent Skill)——正在从根本上重塑我们构建 AI 智能体 (Agent) 的方式。它终于给基础模型 (Model) 提供了真正可测试的程序性记忆 (Procedural Memory)，让它们能记住如何逐步执行任务。依靠渐进式披露 (Progressive Disclosure) 的魔力，技能解决了上下文腐烂 (Context Rot) 的问题。单个通用智能体现在可以顺滑地访问许多专职工作流，而不会噎住自己的 token 预算。</mark>

The pattern we keep coming back to in this paper is that the format is deliberately small so that the interesting work happens around it, not inside it. Evaluating Skills under realistic co-loaded conditions is interesting. Composing Skills into workflows without using the context window as a message bus is interesting. Letting agents draft Skills from successful traces, with humans reviewing rather than authoring, is interesting. Encoding two decades of institutional knowledge into a versioned, testable, governable library is interesting. All of these are now tractable in a way they weren't twelve months ago, because the primitive exists.

<mark>本文一再回到的模式是：格式被故意做得很小，这样有意思的工作发生在它周围，而不是它内部。在真实的共同加载条件下评估技能，是有意思的。把技能组合成工作流，却不把上下文窗口当消息总线，是有意思的。让智能体从成功轨迹起草技能，由人来审而不是由人来写，是有意思的。把二十年的机构知识编码成一个有版本、可测试、可治理的技能库，是有意思的。这些事在十二个月前还做不成，现在变得可处理，是因为这个原语存在了。</mark>

Throughout this paper, we have also tried to be specific about what's settled, what's still emerging, and what's likely to change. The format is settled: agentskills.io is now an open standard with adoption across every major coding agent, AI chatbot, and agent framework that matters. The architecture around it is still emerging: evaluation under co-loaded conditions, Skills-library-level optimization, agent-driven Skill creation, and the governance patterns that make all of this safe at scale.

<mark>整篇论文里，我们也尽量说清什么已经定了，什么还在出现，什么可能会变。格式已经定了：agentskills.io 现在是开放标准，每一个重要的编码智能体、AI 聊天机器人和智能体框架都在采用。它周围的架构仍在出现：共同加载条件下的评估 (Evaluation)、技能库层面的优化、由智能体驱动的技能创建，以及让这一切在规模上仍然安全的治理模式。</mark>

If you are starting today, our suggestion is the one we've made throughout: start small, start with knowledge you already have, treat Skills as code, measure what you ship, and don't reach for a multi-agent architecture when a Skills will do. The teams that figure this out now will build cleaner systems than the teams that wait for the industry consensus to catch up. The format is settled. The work is just beginning.

<mark>如果你今天才开始，我们的建议就是全文一直在说的那句：从小处开始，从你已经有的知识开始，把技能当代码，度量你交付的东西，一个技能够用时就不要伸手去拿多智能体架构。现在就把这件事想清楚的团队，会做出比那些等待行业共识追上来的团队更干净的系统。格式已经定了。工作才刚刚开始。</mark>

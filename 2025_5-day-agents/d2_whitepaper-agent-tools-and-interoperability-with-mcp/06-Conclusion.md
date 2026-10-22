# Conclusion

结论

Foundation models, when isolated, are limited to pattern prediction based on their training data. On their own, they cannot perceive new information or act upon the external world; tools give them these capabilities. As this paper has detailed, the effectiveness of these tools depends heavily on deliberate design. Clear documentation is crucial, as it directly instructs the model. Tools must be designed to represent granular, user-facing tasks, not just mirror complex internal APIs. Furthermore, providing concise outputs and descriptive error messages is essential for guiding an agent's reasoning. These design best practices form the necessary foundation for any reliable and effective agentic system.

孤立的基础模型 (foundation model) 只能根据训练数据做模式预测。单靠自身，它们无法感知新信息，也无法对外部世界采取行动；工具 (Tools) 给了它们这些能力。正如本文所详述的，这些工具是否有效，很大程度上取决于有意的设计。清楚的文档至关重要，因为它直接指导模型 (Model)。工具必须被设计成代表细粒度、面向用户的任务，而不是仅仅照搬复杂的内部 API。此外，提供简洁的输出和描述性的错误信息，对引导智能体 (Agent) 的推理 (Reasoning) 必不可少。这些设计最佳实践，构成任何可靠、有效的智能体系统 (Agentic System) 所必需的基础。

The Model Context Protocol (MCP) was introduced as an open standard to manage this tool interaction, aiming to solve the "N x M" integration problem and foster a reusable ecosystem. While its ability to dynamically discover tools provides an architectural basis for more autonomous AI, this potential is accompanied by substantial risks for enterprise adoption. MCP's decentralized, developer-focused origins mean it does not currently include enterprise-grade features for security, identity management, and observability. This gap creates a new threat landscape, including attacks like Dynamic Capability Injection, Tool Shadowing, and "confused deputy" vulnerabilities.

模型上下文协议 (Model Context Protocol, MCP) 作为开放标准被提出，用来管理这种工具交互，目标是解决「N × M」集成问题，并培育可复用的生态。它动态发现工具的能力，为更自主的 AI 提供了架构基础，但这一潜力伴随着企业采用时的重大风险。MCP 起源于去中心化、以开发者为中心的场景，这意味着它目前并不包含企业级的安全、身份管理和可观测性特性。这一缺口造成了新的威胁版图，包括动态能力注入 (Dynamic Capability Injection)、工具遮蔽 (Tool Shadowing)，以及「混淆代理人」(confused deputy) 漏洞这类攻击。

The future of MCP in the enterprise, therefore, will likely not be its "pure" open-protocol form but rather a version integrated with layers of centralized governance and control. This creates an opportunity for platforms that can enforce the security and identity policies not natively present in MCP. Adopters must implement a multi-layered defense, leveraging API gateways for policy enforcement, mandating hardened SDKs with explicit allowlists, and adhering to secure tool design practices. MCP provides the standard for tool interoperability, but the enterprise bears the responsibility of building the secure, auditable, and reliable framework required for its operation.

因此，MCP 在企业中的未来，很可能不是它「纯」的开放协议形态，而是与一层层集中治理和控制集成之后的版本。这为那些能够执行 MCP 原生并不具备的安全与身份策略的平台创造了机会。采用者必须实现多层防御：利用 API 网关执行策略，强制使用带显式允许列表的加固 SDK，并遵守安全的工具设计实践。MCP 提供了工具互操作性的标准，但企业承担着为它的运行建立安全、可审计、可靠框架的责任。

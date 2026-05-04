---
title: SRE  Agent Harness - 架构、能力与演进
date: 2026-05-02T19:53:17+08:00
description: ""
tags:
  - AI-Agent
categories: []
series: []
draft: true
toc: true
---

# SRE  Agent Harness- 架构、能力与演进

> [!summary] 读完本文，你将
> - 了解Harness Agent的基本概念
> - 了解项目架构以及相关技术点的实现方式
> - 了解如何应用平台/工具产出能力
> - 了解Agent下一步如何迭代/演进


## Agent Harness 的由来

Agent Harness 并不是由某一个人单独提出的全新概念，而是 Agent 工程化实践中逐渐形成的术语。Anthropic 在 2025 年底已经用 “agent harness” 描述 Claude Agent SDK 这类运行基础设施[^1] ；Mitchell Hashimoto 在 2026 年 2 月将相关实践命名为 “harness engineering”[^2]；随后 OpenAI、LangChain、Microsoft 等进一步把它系统化，尤其 LangChain 用 “Agent = Model + Harness” 给出了非常清晰的架构定义[^3]。

从近两年的发展来看，模型能力与工程化手段已经可以支持AI（LLM）自主感知并对真实世界做出影响，Agent Harness 解决的问题是如何让AI运行的更可靠。

![[Pasted image 20260502212712.png]]

## 所以，什么是 Agent Harness？

*个人认为：Harness 这个词很形象，Harness做的事情就好像在研究如何更好的控制一匹马车*

> **If you're not the model, you're the harness.** [^3]

除了模型的一切，都可称之为Harness，Agent = 模型+Harness。

模型是“大脑”，负责思考、推理与生成，让Agent拥有智能。Harness 决定怎么做、能不能做、做完怎么验，让Agent安全、稳定、可控地完成任务。

从现有工程实践经验看，Harness 包括如下内容：

![[Pasted image 20260502233454.png]]

- **Agent Loop**：它围绕感知 → 思考 → 行动 → 观察不断迭代，直到完成任务或达到停止条件。
- **工具层（Tools）**：为 Agent 提供与外部世界交互的能力。包括 沙箱及内置工具、本地 CLI、MCP 连接器、工具注册与管理，让 Agent 能查询信息、执行命令、调用服务。
- **上下文层（Context）**：负责把“模型当前该看到什么”组织好。包括 长期记忆、短期记忆、Prompt、压缩器，用于管理任务背景、历史信息和上下文窗口。
- **编排层（Orchestration）**：负责组织复杂任务的执行方式。包括 SubAgent、Agent Team、Workflow，用于拆分任务、分工协作、控制执行流程。
- **Session 层（Session）**：负责管理一次会话或任务运行期的状态。包括 Session 存储器、Session 管理器，用于保存上下文快照、任务进度和会话生命周期。
- **插件层（Plugins）**：用于扩展 Harness 的能力边界。包括Skill、Plugin、Hook，让系统可以灵活增加能力模块、外部扩展和生命周期钩子。
- **观测与评价层（Observability & Evaluation）**：负责让 Agent 的运行过程“看得见、评得出、能改进”。包括 Trace、Feedback、Evals，用于追踪执行链路、收集反馈、评估效果。
- **安全与治理（贯穿全局）**：不是单独一层，而是贯穿整个 Harness 的约束机制。它负责 权限控制、审计、限流、数据安全、成本控制，保证 Agent 在可控边界内运行。

## 结合当前的项目实现，介绍下每一层的作用

## SRE Agent Harness 是重复造轮子吗


---
参考文献

[^1]: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents

[^2]: https://mitchellh.com/writing/my-ai-adoption-journey

[^3]: https://www.langchain.com/blog/the-anatomy-of-an-agent-harness

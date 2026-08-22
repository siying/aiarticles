# AI Agent 核心架构与范式

## 1. 什么是 AI Agent？

**AI Agent（人工智能体）** 是以大语言模型（LLM）为核心大脑，具备**自主感知环境、独立规划、调用工具与采取行动**以完成复杂目标任务的自动化智能系统。

```
                    ┌─────────────────────────┐
                    │      感知 (Perception)   │
                    └───────────┬─────────────┘
                                │
                    ┌───────────▼─────────────┐
                    │       核心大脑 (LLM)     │
                    │   规划 ⇄ 记忆 ⇄ 反思    │
                    └───────────┬─────────────┘
                                │
                    ┌───────────▼─────────────┐
                    │      行动 (Action/Tools) │
                    │   代码 / API / 搜索     │
                    └─────────────────────────┘
```

---

## 2. Agent 的四大核心要素

### 1. 规划 (Planning)
- **子任务拆解**：将用户的大目标分解为一系列更小、可执行的子任务。
- **自我反思 (Self-Reflection)**：检查过去的行动执行结果，发现错误并调整策略（如 Reflexion 框架）。

### 2. 记忆 (Memory)
- **短期记忆 (Short-term Memory)**：当前会话的上下文窗口（In-context learning）。
- **长期记忆 (Long-term Memory)**：通过向量数据库（Vector DB）存储历史知识、用户画像与经验，按需检索召回。

### 3. 工具使用 (Tool Use / Function Calling)
Agent 通过标准的接口（API、数据库查询、浏览器自动化、Python 解释器等）与外部物理世界交互，弥补 LLM 知识时效性不足和无法执行写操作的限制。

---

## 3. 经典 Agent 交互范式：ReAct

**ReAct (Reasoning + Acting)** 结合了“思考推理”与“采取行动”的循环机制：

```markdown
Question: 查找 2026 年最新开源的深度学习框架并总结其特点。
Thought: 我需要先搜索网络获取相关信息。
Action: search_web("2026 new open source deep learning frameworks")
Observation: [搜索返回结果...]
Thought: 已经获得了框架列表，现在我需要对核心特点进行对比整理。
Action: finish(summary_content)
```

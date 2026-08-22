# 大语言模型 (LLM) 基础与技术全景

## 1. 什么是大语言模型？

大语言模型（Large Language Models，简称 LLM）是基于深度学习架构（主要是 **Transformer**）训练的拥有数十亿至数万亿参数的自然语言处理模型。通过在海量多模态与文本数据上进行自监督预训练，LLM 展现出了强大的语言理解、逻辑推理、代码生成与创造能力。

---

## 2. LLM 的生命周期与训练阶段

现代 LLM 的构建通常经历以下四个核心阶段：

```
[海量无标注文本] 
      ⬇ 
 1. 预训练 (Pre-training) ➡ 基础模型 (Base Model)
      ⬇ 
 2. 监督微调 (SFT) ➡ 指令对齐模型 (Instruct Model)
      ⬇ 
 3. 人类反馈强化学习 (RLHF / DPO) ➡ 安全偏好对齐模型 (Chat Model)
      ⬇ 
 4. 推理与部署 (Inference & Deployment)
```

### 阶段一：预训练 (Pre-training)
- **目标**：通过预测下一个 Token（Next-token prediction）学习语言结构、世界知识与常识。
- **产物**：基础模型（Base Model，如 LLaMA-Base）。

### 阶段二：监督微调 (Supervised Fine-Tuning, SFT)
- **目标**：使用高质量的“指令-回答”问答对数据，让模型理解人类的指令提问方式并给出规范回答。
- **产物**：指令模型（Instruct Model）。

### 阶段三：对齐 (Alignment: RLHF / DPO)
- **目标**：使模型的输出符合人类价值观（有用性 Helpful、真实性 Honest、无害性 Harmless - 3H原则）。
- **常用技术**：
  - **RLHF**（基于人类反馈的强化学习）：PPO 算法
  - **DPO**（直接偏好优化）：无需显式训练 Reward Model，直接利用偏好对比数据优化策略。

---

## 3. 核心概念速查

- **Token 与 Tokenizer**：模型处理文本的最小单元，1 个 Token 大约相当于 0.75 个英文单词或 0.5~1 个中文字符。
- **Context Window（上下文窗口）**：模型一次能接收和处理的最大 Token 数量（如 8K, 32K, 128K, 1M+）。
- **Temperature（温度）**：控制输出多样性的超参数（0~2）。数值越低输出越确定保守；数值越高输出越具发散创造性。
- **Top-p (Nucleus Sampling)**：从累积概率达到 p 的最高概率 Token 集合中采样，平衡创造性与合理性。

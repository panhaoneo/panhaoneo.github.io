+++
title = '使用claude和chatgpt的一些值得记录的prompt'
date = 2026-03-12T16:27:25+08:00
draft = false
+++


## 基层skill

### 1.关于如何开始项目

claude基于我提供的描述，生成了规范的skill，每次根据对话看是否需要启动这个框架。

详细描述如下：

```
关于如何使用你更好的完成项目，我看到两个方法，
方法一：Shopify的CEO有个习惯，每次用AI之前，他会先写一份"上下文文档"，不是提示词，是上下文：

① 项目的背景是什么
② 之前尝试过什么
③ 什么是成功，什么是失败
④ 谁会受影响
⑤ 有哪些约束条件

他说这个习惯不只让AI输出更好，还让他自己思考更清晰。
上下文不止是给AI的说明书，也是你对问题理解程度的外化。

方法二:Redis 作者 antirez 用 Claude Code 写了一个 Z80/ZX Spectrum 模拟器

不是写 CRUD，是硬件模拟。这才是 Claude Code 的正确打开方式。

他的方法很有意思：

1. 先写一份 Markdown 规格说明，把设计要求写清楚

2. 让 Claude Code 上网搜 Z80 技术文档，提取成 markdown

3. 删掉这个 session（防止代码污染）

4. 新开 session，只用收集的文档，禁止联网，让 AI 自主编码

结果：Z80 + ZX Spectrum + CP/M 模拟器全部完成。

关键教训：

- 人负责设计决策，AI 负责实现

- 好的 prompt 规格说明 = 好的结果

- Clean Room 方法论值得学习

源码：github.com/antirez/ZOT

原文：antirez.com/news/160

你学习一下，然后给我总结一套可行的方法流程

The 4D Framework for AI Fluency, developed through research collaboration between Professor Rick Dakan (Ringling College of Art and Design) and Professor Joseph Feller (University College Cork), identifies four core competencies that, when combined, can help you make the most of your AI interactions:

Delegation: Deciding on what work should be done by humans, what work should be done by AI, and how to distribute tasks between them. Includes understanding your goals, AI capabilities, and making strategic choices about collaboration.

Description: Effectively communicating with AI systems. Includes clearly defining outputs, guiding AI processes, and specifying desired AI behaviors and interactions.

Discernment: Thoughtfully and critically evaluating AI outputs, processes, behaviors and interactions. Includes assessing quality, accuracy, appropriateness, and determining areas for improvement.

Diligence: Using AI responsibly and ethically. Includes making thoughtful choices about AI systems and interactions, maintaining transparency, and taking accountability for AI-assisted work.

在文档开头新增了 4D Framework 的理论基础表格，明确每项能力对应哪些阶段；核心原则里也把 4D 的语言织进去；快速参考卡增加了"4D 能力"一列，让每个阶段的意图更清晰。
```

生成的skill参考：
```

---

name: ai-project-methodology

description: 结构化 AI 项目方法论，适用于任何有一定复杂度的开发任务。当用户提到"开始一个新项目"、"帮我做一个系统/工具/脚本"、"我想构建 X"、"新开一个 session"、或者直接描述一个需要多步骤实现的功能需求时，必须触发此 skill。也适用于用户说"帮我理清思路"、"我不知道从哪里开始"、"帮我规划一下"等场景。不要等用户明确说"用方法论"——只要任务有一定规模，就主动应用此流程。

---

# AI 项目方法论（五阶段流程）

综合 Shopify CEO 上下文文档习惯 + antirez Clean Room 方法论 + 4D Framework（Dakan & Feller），适用于任何有一定复杂度的 AI 辅助开发任务。

## 理论基础：4D Framework

Rick Dakan（Ringling College）与 Joseph Feller（UCC）的研究框架，定义了 AI 协作的四项核心能力，是本方法论的底层逻辑：

| 能力 | 含义 | 对应阶段 |

|------|------|---------|

| **Delegation**（任务分配） | 决定哪些工作由人做、哪些交给 AI | Phase 1、3 |

| **Description**（清晰表达） | 有效向 AI 传达意图、规格、约束 | Phase 3、4 |

| **Discernment**（批判评估） | 批判性评估 AI 输出的质量与准确性 | Phase 4、5 |

| **Diligence**（负责任使用） | 对 AI 辅助工作保持透明度与问责 | 贯穿全程 |

## 核心原则

- **人负责设计决策（Delegation），AI 负责实现**

- 上下文文档是写给自己的，规格说明是写给 AI 的——合并为一份文档，分两个 section（Description 的基础）

- Session 有边界，不要让一个 session 承担整个项目生命周期

- 对 AI 输出始终保持 Discernment，规格是评估的标尺

- 最终对产出负责的是人，不是 AI（Diligence）

---

## 五个阶段

### Phase 1：上下文文档（必做，动手前完成）

帮用户写或引导用户填写以下结构：

```markdown

## 背景与约束

- 项目背景：这是什么，解决什么问题

- 已尝试过的方案：之前做了什么，结果如何

- 成功标准：怎么算做好了

- 失败标准：什么情况算失败

- 约束条件：技术栈、不能碰的东西、性能要求、截止时间

- 受影响方：谁会用这个，谁受影响

## 技术规格（Phase 3 完成后填写）

- 模块划分

- 接口定义

- 关键设计决策（及理由）

- 边界条件与异常处理

```

**注意**：写上下文文档的过程本身就是思维整理。如果用户写不出某个字段，说明这里还没想清楚，需要先讨论。

---

### Phase 2：知识收集（涉及陌生领域时执行）

**触发条件**：项目涉及用户或 AI 不熟悉的技术（特定协议、硬件规范、第三方 API、行业标准等）。

**操作**：

1. 单独开一个 session，只做知识收集

2. 联网搜索相关技术文档，整理成 markdown

3. 这个 session 结束后丢弃，只保留输出的文档

**为什么要单独 session**：防止半成品代码和探索性对话污染后续执行上下文。

---

### Phase 3：规格说明（设计在 AI 动手前完成）

这是 Phase 1 文档的"技术规格"section。**由用户来写，不是 AI 来写**。

Claude 的角色：

- 提问帮助用户想清楚模块边界

- 指出规格里的歧义或缺失

- 不要在规格未完成时开始实现

关键问题清单：

- [ ] 输入输出格式是否明确？

- [ ] 各模块之间的接口是否定义清楚？

- [ ] 错误处理逻辑是否覆盖？

- [ ] 有没有需要特别注意的边界条件？

---

### Phase 4：执行 Session（Clean Room）

**新开一个 session**，带入以下内容：

- Phase 1 的完整文档（背景 + 技术规格）

- Phase 2 收集的参考文档（如有）

- 明确告知 AI：禁止联网，按规格实现

**用户在这个 session 里的角色**：

- 验证输出是否符合规格

- 做阶段性 code review

- **不在这里改需求**——改需求要回到文档层面

---

### Phase 5：迭代纪律

- 每个功能块完成后，评估上下文是否已经过长或偏离

- 新功能块考虑是否需要重新走 Phase 2-4

- 长项目里，定期"归档"已完成模块的规格，开新 session 继续

**Session 寿命判断**：

- 上下文超过 50+ 轮对话 → 考虑新 session

- AI 开始重复之前已修复的错误 → 必须新 session

- 需求发生重大变更 → 必须新 session，先更新文档

---

## Claude 使用此 Skill 的行为准则

1. **不要直接开始写代码**，先询问/引导完成 Phase 1

2. 如果用户跳过文档阶段，温和指出：跳过上下文文档往往导致后期返工

3. 规格不清晰时，提问而不是自己猜测和假设

4. 执行阶段严格按规格来，遇到规格外的情况暂停确认，不自作主张

5. 每个阶段结束时明确告知用户"现在可以进入下一阶段了"

---

## 快速参考卡

| 阶段 | 做什么 | 谁来做 | Session | 4D 能力 |

|------|--------|--------|---------|---------|

| Phase 1 | 上下文文档 | 用户（AI 辅助） | 当前 | Delegation |

| Phase 2 | 知识收集 | AI（联网） | 新建，用完丢弃 | Delegation |

| Phase 3 | 技术规格 | 用户（AI 提问） | 当前 | Delegation + Description |

| Phase 4 | Clean Room 实现 | AI（禁网） | 新建 | Description + Discernment |

| Phase 5 | 迭代管理 | 用户 + AI | 按需新建 | Discernment + Diligence |

```

### 2.
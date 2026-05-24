---
name: dc-analysis
description: "批量文献讨论-结论分析与创新点挖掘 - 从多篇论文摘要+讨论+结论中提取真实研究问题和真正创新方向，重点关注原文中未尝试、未解决的方向，生成问题-创新映射报告（直接保存文件，对话仅显示摘要）。需要intro-analysis输出作为主题先验知识以收束研究方向。包含讨论五步解析、问题-创新配对、真实创新头脑风暴、Mermaid可视化逻辑链。Use when user needs innovation point mining, finding real unsolved problems, or writing the novelty section of a research paper. Input: markdown file with abstracts+discussions+conclusions + introduction-analysis output for theme reference. Output: structured innovation analysis report."
---

# 讨论-结论导向创新点挖掘技能

## 核心功能

1. **创新点挖掘** - 从Abstract/Discussion/Conclusion中提取作者声明的创新、对比优势和真实研究问题
2. **讨论五步解析** - 按Hartley五步法解构每篇论文的讨论论证结构
3. **问题-创新映射** - 可视化展示"旧问题→已有创新→新问题→创新机会"的因果逻辑链
4. **真实创新头脑风暴** - 基于原文线索外推，聚焦"原文中没做、领域中没人做、确实该做"的方向

---

## 核心设计原则

### 1. 原文-分析配对原则 ⭐

**每条 `[原文声明]` 必须搭配 `[模型归纳]` 分析，二者缺一不可。**

- 禁止连续堆砌原文引用而不作分析
- `[模型归纳]` 必须基于原文推演，不得凭空编造
- 正确模式：`[原文声明]` → `[模型归纳]` → `[原文声明]` → `[模型归纳]`

### 2. 创新点提取

从三个章节语义理解作者的创新声明（非硬性关键词匹配）：

- **Abstract** → 作者的核心贡献声明（"我们做了什么新东西"）
- **Discussion** → 与前人工作的具体对比和优势（"比前人好在哪/有何不同"）
- **Conclusion** → 工作价值的拔高（"这个工作的更大意义是什么"）

**标签系统**：
- `[原文声明]` — 论文明确声明的内容
- `[模型归纳]` — 基于原文推理的分析（必须说明推理依据）
- `[创新声明]` — 作者宣称的创新贡献
- `[对比优势]` — 与前人工作的具体对比
- `[价值升华]` — 对工作意义的拔高陈述
- `[开放问题]` — 有真实问题但无已发表的创新方案
- `[模型归纳·头脑风暴]` — 基于原文线索外推的创新方向（必须附推理链）

**不确定性标记**：
- `[未明确给出]` — 论文中未提及的字段
- `[不确定]` — 信息有歧义

### 3. 讨论五步解析 (Hartley Method)

每篇论文的Discussion按五步结构解析，每步对应不同提取目标：

| 步骤 | 内容 | 提取目标 |
|------|------|---------|
| Step 1: 重述结论 | 作者认为最重要的发现 | 核心结果证据 |
| Step 2: 对比前人 | 与已有文献的异同、优劣 | `[对比优势]` 创新证据 |
| Step 3: 局限性 | 作者承认的不足 | **真实问题来源** |
| Step 4: 解决方案 | 作者建议的改进路径 | 已有改进思路 |
| Step 5: 新问题 | 研究揭露的新方向 | **开放问题来源** |

### 4. 问题-创新配对原则 ⭐

**每个识别的问题必须能追溯到对应的创新点（或标记为开放问题），每个创新点必须对应其解决的问题。**

- 问题有对应创新 → 已解决问题，记录解决方案
- 问题无对应创新 → `[开放问题]`，这是真正的创新机会
- 创新无明确问题动机 → 标记 `[创新动机未明确]`
- 旧问题→已有创新→产生的新问题 → 可视化逻辑链

### 5. 真实创新头脑风暴

**只关注"原文中没做、领域中没人做、但确实该做"的方向。**

- `[模型归纳·头脑风暴]` 必须基于原文明确线索外推
- 必须附完整推理链：原文证据 → 中间推理 → 创新方向
- 必须标注信心程度：高/中/低
- 聚焦可实现性 — 基于现有方法可缝合、可扩展的方向
- 禁止脱离原文天马行空

### 6. 主题对齐收束

- 必须提供introduction-analysis输出文件作为主题先验知识
- 分析开始前向用户展示introduction-analysis识别的主题列表
- 询问用户聚焦哪个主题深入挖掘
- 在选定主题上深度挖掘问题-创新关系
- 若introduction-analysis结果不可用，自动从dc内容检测主题并请用户确认

### 7. 可视化实质化

**所有关系图必须使用Mermaid语法，禁止纯文本/ASCII替代。**

- 问题-创新逻辑链图 → Mermaid graph（因果链条，颜色编码）
- 创新机会脑图 → Mermaid mindmap（全景展开）
- 问题依赖网络 → Mermaid graph（根因/层级/相关）
- 讨论五步流程图 → Mermaid flowchart（单篇论证结构）

### 8. 文献可追溯性

每篇文献有完整身份标识，报告末尾提供文献索引表

---

## 触发条件

- 批量论文的Abstract + Discussion + Conclusion文本
- 需要挖掘创新点、未解决问题、未来方向
- 需要写论文创新点/新颖性部分
- 需要从讨论中找出真正空白和可缝合的方向
- 已拥有intro-analysis分析结果（或可同时提供）

---

## 输入格式

### 主要输入：批量文献md文件

```markdown
---
id: unique_id (optional)
title: Paper Title
year: Year
doi: DOI
authors: Author short names List
pmid: PubMed ID (optional)
---

## Abstract
Abstract content...

## Discussion
Discussion content...

## Conclusion
Conclusion content...
```

### 辅助输入：introduction-analysis分析输出文件

提供introduction-analysis输出的md文件路径，用于主题对齐和先验知识。

**重要说明**：
- **Discussion + Conclusion是必需的**：完整分析需要两者
- **Discussion-only（无Conclusion）**：缺失价值升华信息
- **仅有Abstract**：极有限分析，仅提取创新声明
- **introduction-analysis输出**：强烈建议提供，用于主题收束

---

## 分析流程

### 第一阶段：逐篇DC深度解析

0. 文献元信息提取
1. Discussion五步结构解析（每步标注原文+位置）
2. Conclusion三段结构解析（总结/结论/展望）
3. 创新声明提取（从Abstract/Discussion/Conclusion语义识别）
4. 真实问题识别（重点：从Discussion Step 3局限性+Step 5新问题）
5. 局限性提取与分类
6. 未来方向提取
7. 每篇论文的问题-创新配对
8. **原文-分析配对检查**：每条`[原文声明]`有配套`[模型归纳]`

### 第二阶段：跨文献综合与主题挖掘

1. **主题对齐**：读取introduction-analysis输出，展示主题列表
2. **用户选择聚焦主题**：询问用户聚焦哪个主题深入
3. **选定主题深度挖掘**：
   - 该主题内所有论文的问题汇总
   - 该主题内所有创新点汇总
   - 问题-创新配对关系梳理
   - 开放问题识别（该主题内有真实问题但无创新方案）
4. 构建问题依赖网络（Mermaid graph）
5. 构建问题-创新逻辑链（Mermaid graph — 核心可视化）
6. 构建创新机会脑图（Mermaid mindmap）
7. **真实创新头脑风暴**：基于开放问题+原文线索外推

### 第三阶段：生成创新分析报告

输出格式：`[输入文件名]_dc_[YYYYMMDD].md`

**只保存文件，不在对话中显示完整内容**

对话中显示简要摘要：
```markdown
✅ 分析完成

📊 分析统计
- 文献数量：N篇
- 识别真实问题：X个（开放问题：Y个）
- 提取创新声明：Z个
- 聚焦主题：[主题名称]
- 数据来源：Abstract + Discussion + Conclusion

📁 输出文件
- 路径：[文件路径]
- 格式：Markdown (.md)

💡 核心发现
- 开放问题：[简要描述]
- 创新机会：[简要描述]
```

---

## 关键原则

1. **原文-分析配对**：每条`[原文声明]`必须配`[模型归纳]`，禁止原文堆砌
2. **讨论五步解析**：所有讨论分析参照五步结构
3. **问题-创新配对**：每个问题追溯创新，每个创新对应问题
4. **真实创新头脑风暴**：基于原文外推，不天马行空，聚焦可实现
5. **双标签系统**：所有观点标注`[原文声明]`或`[模型归纳]`
6. **保留原文表述**：原文英文用「...」包裹
7. **不确定性标记**：不确定信息必须标注
8. **主题对齐**：从introduction-analysis继承主题，收束研究方向
9. **可视化实质化**：所有图表Mermaid语法，禁止ASCII替代
10. **反幻觉优先**：绝不编造论文未声明的内容

---

## Quick Reference

**讨论五步解析与结论三段结构** → `references/discussion-structure.md`

**创新点与问题提取规则（含头脑风暴边界）** → `references/innovation-extraction.md`

**双标签系统与引用格式** → `references/citation-rules.md`

**分析流程详细说明** → `references/analysis-workflow.md`

**可视化类型详解（含逻辑链图和脑图）** → `references/visualization-types.md`

**输出格式与保存规则** → `references/output-format.md`

**反质量检查** → `references/quality-checklist.md`

**特殊情况处理** → `references/special-cases.md`

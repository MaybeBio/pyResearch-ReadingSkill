---
name: intro-analysis
description: "批量文献引言分析与综述生成 - 当用户需要进行文献综述、领域调研、或从多篇论文的引言中梳理研究脉络时使用。输入单个包含多篇论文摘要+引言的markdown文件，输出结构化的综述报告（直接保存为文件，对话中仅显示简要摘要），包含时间线、多主题深度分析、观点论战、Mermaid可视化图表。特别适用于生物医学计算、AI4S等交叉领域的文献调研工作。Use when user needs literature review, domain research, or extracting research progress from multiple paper introductions. Input: single markdown file with abstracts+introductions. Output: structured review report saved as markdown file, brief summary in dialog. Includes timeline, deep theme analysis, viewpoint debates, and Mermaid visualizations."
---

# 引言导向文献综述技能

## 核心功能

1. **文献调研** - 仅从引言完成研究开题报告背景部分
2. **多主题识别** - 自动识别所有可能的研究方向（不预设, 基于原文内容合理外推分类, 至少识别出5个主题方向）
3. **可视化梳理** - Mermaid图表展示观点依赖、论证流程、范式演进
4. **每主题深度展开** - 每个识别的主题独立深入分析（时间线、方法、缺口、观点）

---

## 核心设计原则

### 1. 原文-分析配对原则 (Citation-Analysis Pairing) ⭐

**原文引用是证据，分析归纳是价值。二者缺一不可。**

- 每条 `[原文声明]` 必须搭配 `[模型归纳]` 注释分析
- 禁止连续堆砌原文引用而不作分析
- `[模型归纳]` 必须基于原文推演，不得凭空编造
- 正确模式：`原文声明 → 模型归纳 → 原文声明 → 模型归纳`

### 2. 反幻觉机制 (Anti-Hallucination)

**双标签系统**：
- `[原文声明]` - 论文明确声明的内容
- `[模型归纳]` - 基于原文推理的分析（必须说明推理依据）

**不确定性标记**：
- `[未明确给出]` - 论文中未提及的字段
- `[不确定]` - 信息有歧义
- `[引用文献未详述]` - 二手引用信息不全

**原文引用三要素**：
1. 来源文献（完整引用格式）
2. 原文内容（保留原文英文）
3. 位置标注（具体到段/句）

### 3. 每主题深度展开 (Per-Theme Deep Dive)

**每个识别的主题必须获得独立的深度分析**，不能浅尝辄止：

- 主题定义与范围界定
- 该主题的方法论演进时间线（≥3个时间节点）
- 该主题的方法分类与比较表格
- 该主题的核心观点与争议
- 该主题的研究缺口（≥2个）
- 该主题的观点依赖图（Mermaid graph）
- 该主题的代表性文献列表

### 4. 可视化实质化 (Substantive Visualization)

**所有关系图必须使用Mermaid语法，禁止纯文本/ASCII替代。**

- 观点依赖图 → Mermaid graph（含颜色编码、关系类型标注）
- 论证流程图 → Mermaid flowchart
- 观点演进 → Mermaid sequence diagram
- 范式转换 → Mermaid state diagram
- 主题关系 → Mermaid mindmap
- 时间线 → Mermaid timeline

### 5. 文献可追溯性

每篇文献必须有完整身份标识，报告末尾提供文献索引表

---

## 触发条件

- 批量论文的摘要+引言文本
- 需要进行文献综述、领域调研、研究脉络梳理
- 需要从引言中提取历史背景、研究现状、观点演进
- 需要可视化观点之间的复杂关系

---

## 输入格式

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

## Introduction
Introduction content...
```

**重要说明**：
- **Introduction是必需的**：完整分析需要Introduction
- **仅有Abstract也可接受**：可提取研究问题、方法、贡献，但会缺失历史脉络、研究缺口等深度信息

---

## 分析流程

### 第一阶段：独立解析每篇文献

0. 文献元信息提取
1. 研究定位与第一性原理
2. 历史脉络提取
3. 研究现状分类
4. 研究缺口识别（重点 — 识别四类缺口）
5. 核心观点提取
6. 关键参考文献整理
7. **原文-分析配对**：每条 `[原文声明]` 后生成配套 `[模型归纳]` 分析

### 第二阶段：跨文献综合分析

1. **自动识别研究主题**（不预设）— 从引言内容自动聚类
2. **每个主题深度展开** — 每个主题独立包含：
   - 主题定义、方法论时间线、方法分类表、核心争议、研究缺口、观点依赖图、代表性文献
3. 构建领域时间线（Mermaid timeline）
4. 观点追踪与论战（对比表格）
5. 观点依赖图（Mermaid graph）
6. 论证流程图（Mermaid flowchart）
7. 观点演进序列图（Mermaid sequence diagram）
8. 研究范式状态转换图（Mermaid state diagram）
9. 研究缺口综合（含缺口依赖图）

### 第三阶段：生成综述报告

输出格式：`[输入文件名]_intro_[YYYYMMDD].md`

**只保存文件，不在对话中显示完整内容**

对话中显示简要摘要：
```markdown
✅ 分析完成

📊 分析统计
- 文献数量：N篇
- 识别主题：X个
- 时间跨度：[起始年] - [结束年]
- 每个主题均已完成深度展开

📁 输出文件
- 路径：[文件路径]
- 格式：Markdown (.md)
```

---

## 关键原则

1. **原文-分析配对**：每条 `[原文声明]` 必须配 `[模型归纳]` 分析，禁止原文堆砌
2. **每主题深度展开**：每个主题独立分析，含时间线、方法表格、缺口、观点图
3. **观点溯源**：所有观点标注来源和原文引用
4. **双标签系统**：所有观点标注 `[原文声明]` 或 `[模型归纳]`
5. **保留原文表述**：原文内容保留英文，使用 `「...」` 包裹
6. **不确定性标记**：不确定信息必须标注
7. **区分层次**：明确区分"作者观点(原文id)"和"作者引用的他人观点(原文id-内部引用文献数字标注)", 两者都能溯源
8. **时间线一致性**：同事件不同年份表述时同时记录并标注差异
9. **论战清晰化**：对立观点并置展示
10. **可视化实质化**：所有图表使用Mermaid语法，禁止ASCII替代
11. **反幻觉优先**：绝不编造论文未声明的内容

---

## Quick Reference

**反幻觉机制与质量检查** → `references/quality-checklist.md`

**双标签系统与引用格式（含原文-分析配对原则）** → `references/citation-rules.md`

**可视化类型详解** → `references/visualization-types.md`

**分析流程详细说明（含每主题深度展开要求）** → `references/analysis-workflow.md`

**特殊情况处理** → `references/special-cases.md`

**输出格式与保存规则** → `references/output-format.md`
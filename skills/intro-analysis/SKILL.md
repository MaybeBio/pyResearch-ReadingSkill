---
name: intro-analysis
description: 批量文献引言分析与综述生成 - 当用户需要进行文献综述、领域调研、或从多篇论文的引言中梳理研究脉络时使用。输入单个包含多篇论文摘要+引言的markdown文件，输出结构化的综述报告（直接保存为文件，对话中仅显示简要摘要），包含时间线、观点论战、研究进展追踪。特别适用于生物医学计算、AI4S等交叉领域的文献调研工作。Use when user needs literature review, domain research, or extracting research progress from multiple paper introductions. Input: single markdown file with abstracts+introductions. Output: structured review report saved as markdown file, brief summary in dialog. Includes timeline, viewpoint debates, progress tracking. Also supports introduction writing guidance by analyzing high-quality introduction structures.
---

# 引言导向文献综述技能

## 核心功能

1. **文献调研** - 仅从引言完成研究开题报告背景部分
2. **多主题识别** - 自动识别所有可能的研究方向（不预设）
3. **可视化梳理** - 复杂逻辑关系、观点互作、依赖追踪
4. **引言写作指导** - 学习高质量引言的结构

## 核心设计原则

### 反幻觉机制 ⭐

**双标签系统**：
- `[原文声明]` - 论文明确声明的内容
- `[模型归纳]` - 基于分析的推断

**证据标注**：所有证据性论点必须有原文引用

**不确定性标记**：
- `[未明确给出]` - 论文中未提及的字段
- `[不确定]` - 信息有歧义
- `[引用文献未详述]` - 二手引用信息不全

**原文引用三要素**：
1. 来源文献（完整引用格式）
2. 原文内容（保留原文英文）
3. 位置标注（具体到段/句）

### 文献可追溯性 ⭐

每篇文献必须有完整身份标识（id, title, authors, year, journal, doi, pmid）

在报告末尾提供完整文献索引表

---

## 触发条件

- 批量论文的摘要+引言文本
- 需要进行文献综述、领域调研、研究脉络梳理
- 需要从引言中提取历史背景、研究现状、观点演进
- 需要分析引言结构、学习引言写作
- 需要可视化观点之间的复杂关系

---

## 输入格式

```markdown
---
id: unique_id
title: Paper Title
authors: Author List
year: Year
journal: Journal Name (optional)
doi: DOI (optional)
pmid: PubMed ID (optional)
---

## Abstract
Abstract content...

## Introduction
Introduction content...
```

**重要说明**：
- **Introduction是必需的**：完整分析需要Introduction
- **仅有Abstract也可接受**：可以提取研究问题、方法、贡献，但会缺失历史脉络、研究缺口等深度信息

---

## 分析流程

### 第一阶段：独立解析每篇文献

提取内容：
0. 文献元信息
1. 研究定位与第一性原理
2. 历史脉络
3. 研究现状分类
4. 研究缺口（重点）
5. 核心观点
6. 关键参考文献
7. 引言结构分析

### 第二阶段：跨文献综合分析

1. 自动识别研究主题（不预设）
2. 每个主题的详细分析
3. 构建领域时间线
4. 观点追踪与论战
5. 观点依赖图
6. 论证流程图
7. 观点演进序列图
8. 研究范式状态转换图
9. 研究缺口综合

### 第三阶段：引言写作指导

1. 漏斗式开篇模式
2. 研究缺口陈述模式
3. 解决方案呈现模式
4. 高质量引言特征

### 第四阶段：生成综述报告

输出格式：`[输入文件名]_intro_[YYYYMMDD].md`

**只保存文件，不在对话中显示完整内容**

对话中显示简要摘要格式：
```markdown
✅ 分析完成

📊 分析统计
- 文献数量：N篇
- 识别主题：X个
- 时间跨度：[起始年] - [结束年]

📁 输出文件
- 路径：[文件路径]
- 格式：Markdown (.md)

🔍 主要发现
- 核心主题1：[简要描述]
- 核心主题2：[简要描述]
```

---

## 关键原则

1. **观点溯源**：所有提取的观点、事实、引述必须标注来源和原文引用
2. **双标签系统**：每条观点必须标注 `[原文声明]` 或 `[模型归纳]`
3. **保留原文表述**：历史脉络、观点等必须保留原文英文，使用 `「...」` 包裹
4. **不确定性标记**：所有不确定信息必须标注
5. **区分层次**：明确区分"作者观点"和"作者引用的他人观点"
6. **时间线一致性**：当同一事件在不同文献中有不同年份表述时，同时记录并标注差异
7. **论战清晰化**：对立观点并置展示，包含原文引用
8. **主题自动识别**：不预设任何主题，从引言内容自动聚类
9. **可视化优先**：复杂关系优先用图表展示，图表比文字更易于理解
10. **反幻觉优先**：绝不编造论文未声明的内容

---

## Quick Reference

**反幻觉机制与质量检查** → `references/quality-checklist.md`

**双标签系统与引用格式** → `references/citation-rules.md`

**可视化类型详解** → `references/visualization-types.md`

**分析流程详细说明** → `references/analysis-workflow.md`

**特殊情况处理** → `references/special-cases.md`

**输出格式与保存规则** → `references/output-format.md`

**引言写作指导** → `references/introduction-writing.md`
---
name: method-analysis
description: "研究方案生成与方法缝合 - 输入批量文献Method章节+dc-analysis输出+可选仓库README，针对用户指定的问题（可从dc-analysis开放问题中选择或自定义），从全域文献Method中检索可缝合的方法组件，生成包含数据策略、模型架构设计、训练策略、Benchmark评估和B计划的完整课题研究方案（直接保存文件，对话仅显示摘要）。支持多方案Fork、架构Mermaid schematic、方法缝合溯源。特别适用于AI4S计算领域的研究方案设计。Use when user needs to synthesize a research proposal from literature methods, stitch together existing methods into novel solutions, or design a complete ML/DL research pipeline (data→model→training→evaluation). Input: method sections md + dc-analysis output + optional repo READMEs."
---

# 方法导向研究方案生成技能

## 核心功能

1. **问题驱动的方案生成** - 用户指定问题（从dc-analysis开放问题中选择、杂糅或自定义），以此为起点生成完整研究方案
2. **方法缝合引擎** - 从全域文献Method章节 + 仓库README中检索可复用组件，按组合/迁移/逆向/细化/扩展/评估创新等策略缝合
3. **多路径方案设计** - 每个技术环节给出2-3个可选方案Fork，对比优劣与适用场景
4. **全Pipeline覆盖** - 数据→预处理→模型架构→训练策略→Benchmark→挑战与B计划

---

## 核心设计原则

### 1. 问题驱动原则

**先确定问题再选方法，不是先看方法再想问题。**

- 列出dc-analysis全部开放问题供用户参考
- 用户用自然语言指定问题：单选/多选杂糅/完全自定义
- 问题精确化：拆解为子问题，明确每个子问题的输入/输出/约束

### 2. 方法缝合 (Method Stitching) ⭐

**从全域文献Method + 仓库README中提取可复用组件进行缝合。**

6种缝合策略（from method_analysis.md）：

| 策略 | 操作 | 适用场景 |
|------|------|---------|
| **组合** | A方法模块X + B方法模块Y = 新方案 | 两个方法的互补组件可拼接 |
| **迁移** | 领域X的方法 → 领域Y的问题 | 跨领域借鉴成熟方案 |
| **逆向** | 翻转已有假设 → 新视角 | 挑战默认前提 |
| **细化** | 加约束条件 → 细分方案 | 大问题收缩为精准切入点 |
| **扩展** | 改进已有方法的特定不足 | 针对性的局部优化 |
| **评估创新** | 自创评估指标/多角度评估 | 避开卷SOTA |

### 3. 多方案Fork

**每个关键技术环节给出2-3个可选方案：**
- 推荐方案 + 备选方案 + 激进方案
- 每个方案标注：核心思路 | 优势 | 风险 | 参考实现(PMID/DOI/仓库)
- 标注适用场景和选择条件

### 4. 全Pipeline覆盖

**完整覆盖8个环节，无遗漏：**
1. 问题定义
2. 方法全景脑图
3. 数据策略（多方案fork）
4. 模型架构设计（Mermaid schematic + 变体 + 参考仓库）
5. 训练策略（多方案对比）
6. Benchmark与评估
7. 挑战与B计划
8. 方法缝合溯源表

### 5. 原文引用反幻觉

- 所有方法引用必须基于原文Method章节或仓库README
- 每处引用标注真实PMID/DOI
- 禁止虚构模型架构细节、训练参数、实验结果
- 不确定的实现细节标注 `[未明确给出]`
- `[模型归纳·方案推演]` 标注方案组件是推理外推还是原文已有

### 6. 可实现性优先

- 方案基于现有开源仓库/框架可落地
- 标注参考仓库链接（从README输入中提取）
- 若无开源实现，标注方法的可复现性评估

---

## 触发条件

- 需要从文献Method中生成研究方案
- 需要针对特定问题设计ML/DL pipeline
- 需要方法缝合和创新方案构思
- 拥有dc-analysis分析结果（或可同时提供开放问题清单）
- 用户说"设计方案"、"研究方案"、"method"、"怎么做"、"pipeline"

---

## 输入格式

### 主要输入：Method提取md文件
```markdown
---
id: unique_id (optional)
title: Paper Title
year: Year
doi: DOI
authors: Author short names
pmid: PubMed ID (optional)
---

## Method
Method content...
```

### 辅助输入1：dc-analysis输出md（必需）
```
dc-analysis的完整输出，含开放问题清单+创新头脑风暴+主题框架
```

### 辅助输入2：仓库README汇总md（可选）
```
<<<PY_PAPERFLOW_REPO_BOUNDARY>>>
# Repository: owner/repo-name
name: owner/repo-name
description: ...
[README content]

<<<PY_PAPERFLOW_REPO_BOUNDARY>>>
# Repository: ...
```

### 用户问题（必需）
自然语言描述，可参考dc-analysis开放问题，支持多问题杂糅。

---

## 分析流程

### 第一阶段：问题定义与拆解

1. **列出dc-analysis全部开放问题**（供用户参考）：
   ```
   📋 从dc-analysis继承的Y个开放问题：
   OP-1: [问题描述]
   OP-2: [问题描述]
   ...
   ```
2. **用户指定问题**：自然语言，可参考上述开放问题，支持多问题杂糅
3. **问题精确化**：拆解为子问题，明确每个子问题的输入/输出/约束条件
4. **主题对齐**：标注问题涉及的intro-analysis主题，确定方法检索范围

### 第二阶段：全域方法检索

1. 从Method提取md中检索与问题相关的所有方法组件（不限主题标签，全域文献）
2. 从仓库README中检索可用的开源实现
3. 按Pipeline阶段归类：数据层/特征层/模型层/训练层/评估层
4. 构建**方法全景脑图**（Mermaid mindmap）：展示所有可复用组件及其来源

### 第三阶段：多路径研究方案生成

按8章结构输出，每个环节多方案Fork。

---

## 输出结构（8章）

### 1. 问题定义
- 精确问题阐述
- 子问题拆解（树形结构）
- 每个子问题的输入/输出/约束
- 主题对齐（涉及的intro-analysis主题）

### 2. 方法全景脑图
Mermaid mindmap：全域Method中可复用组件按Pipeline阶段归类，叶节点标注PMID/DOI

### 3. 数据策略
- 数据来源：具体数据库/数据集名 + 规模 + 获取方式
- 收集策略：检索策略/纳入排除标准
- 预处理Pipeline：每步骤2-3个方案fork
- 特征工程：可选方案 + 参考实现

### 4. 模型架构设计
- **核心架构Mermaid schematic**（流程图展示数据流+模块连接）
- 架构变体Fork（2-3个可选架构）
- 每个模块引用来源方法(PMID/DOI)
- 参考开源仓库（从README输入提取）

### 5. 训练策略
- 损失函数选择（多方案对比表）
- 优化器与调度器配置
- 正则化策略
- 训练技巧（数据增强/预训练/微调/早停）
- 参考训练配置（从原文提取）

### 6. Benchmark与评估
- 对比方法列表（含选择理由）
- 评估指标（含可自创指标）
- 预期性能目标
- 评估protocol（交叉验证/独立测试/消融实验）

### 7. 挑战与B计划
- 预期风险分类：方法风险/数据风险/工程风险
- 每个风险的备选路径或简化方案
- 失败判定标准与回退策略

### 8. 方法缝合溯源表
| 方案组件 | 来源论文(PMID/DOI) | 方法原文引用 | 开源仓库 | 缝合策略 | 在方案中的位置 |
|---------|-------------------|------------|---------|---------|--------------|
| ... | ... | ... | ... | 组合/迁移/... | Pipeline阶段X |

---

## 关键原则

1. **问题驱动**：先问题后方法，不颠倒
2. **方法缝合+合理外推**：组合/迁移/逆向/细化/扩展/评估创新
3. **多方案Fork**：每关键环节2-3个可选方案
4. **全Pipeline覆盖**：8章无遗漏
5. **DOI/PMID精确引用**：禁止虚构，标注 `[未明确给出]`
6. **可实现性优先**：基于开源仓库
7. **原文-分析配对**：引用Method原文+分析优劣势
8. **跨主题方法借用**：不限文献主题标签，全域检索
9. **方案推演标注**：`[模型归纳·方案推演]` 标注推理外推

---

## Quick Reference

**方法缝合规则与策略** → `references/method-stitching.md`

**Pipeline各环节设计模板** → `references/pipeline-design.md`

**三阶段分析详细流程** → `references/analysis-workflow.md`

**双标签系统与引用格式（含仓库引用）** → `references/citation-rules.md`

**可视化类型（架构schematic + 脑图 + fork表）** → `references/visualization-types.md`

**输出格式与保存规则** → `references/output-format.md`

**反质量检查** → `references/quality-checklist.md`

**特殊情况处理** → `references/special-cases.md`

# pyResearch-ReadingSkill

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://docs.anthropic.com/en/docs/claude-code)
[![Contributors](https://img.shields.io/github/contributors/nicaizht/pyResearch-ReadingSkill)

一个专注于从引言（Introduction）角度进行文献调研和写作指导的 Claude Code Skill 集合，支持批量文献引言分析、多主题自动识别、复杂关系可视化等功能，内置严格的反幻觉机制和完整的文献可追溯性。

> **English summary**: A collection of Claude Code skills focused on literature review from the Introduction perspective. Features batch introduction analysis, automatic theme detection, complex relationship visualization, built-in anti-hallucination mechanisms, and complete paper traceability. Designed for academic research, especially in biomedical computing and AI4S fields.

---

## 功能亮点

- **批量引言分析** - 从多篇论文的引言完成文献综述，无需阅读全文
- **多主题自动识别** - 不预设任何主题，从引言内容自动聚类研究方向
- **复杂关系可视化** - 6种Mermaid图表展示观点依赖、论证流程、观点演进
- **反幻觉机制** - 双标签系统 + 严格原文引用 + 不确定性标记
- **文献可追溯性** - 完整引用格式，每篇文献可精确定位
- **引言写作指导** - 通过分析高质量引言，学习顶刊写作范式

---

## 快速开始

### 前置条件

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI 已安装

### 安装

### 方式一：安装单个skill（推荐）

```bash
# 克隆整个仓库
git clone https://github.com/nicaizht/pyResearch-ReadingSkill ~/pyResearch-ReadingSkill

# 复制需要的skill到Claude skills目录
cp -r ~/pyResearch-ReadingSkill/skills/intro-analysis ~/.claude/skills/
```

### 方式二：直接复制skill文件夹

```bash
# 下载ZIP后解压，然后复制
unzip pyResearch-ReadingSkill.zip
cp -r pyResearch-ReadingSkill/skills/intro-analysis ~/.claude/skills/
```

### 方式三：符号链接（开发时推荐）

```bash
git clone https://github.com/nicaizht/pyResearch-ReadingSkill ~/pyResearch-ReadingSkill
ln -s ~/pyResearch-ReadingSkill/skills/intro-analysis ~/.claude/skills/intro-analysis
```

### 安装多个skill

如果需要安装多个skill：
```bash
cp -r ~/pyResearch-ReadingSkill/skills/* ~/.claude/skills/
```

### 验证安装

```bash
ls ~/.claude/skills/intro-analysis/SKILL.md
```

### 卸载skill

```bash
rm -rf ~/.claude/skills/intro-analysis
```

### 使用

在 Claude Code 中，直接用自然语言触发：

```
帮我分析这个文献集的引言，生成一篇领域综述。文件在 papers.md
从这些论文的引言中，提取它们提到的历史里程碑工作
分析这些引言，看看涉及哪些可能的研究方向
```

---

## 添加新skill到仓库

本仓库设计为skill集合，可在`skills/`目录下添加多个skill：

### skill目录结构

```
pyResearch-ReadingSkill/
├── skills/
│   ├── intro-analysis/          # 引言分析skill
│   │   ├── SKILL.md            # skill主文件
│   │   └── references/         # 参考文档
│   ├── your-new-skill/         # 新skill
│   │   └── SKILL.md
│   └── another-skill/
│       └── SKILL.md
├── test_data/                  # 测试数据（可选）
├── README.md
└── LICENSE
```

### 创建新skill

1. 在`skills/`下创建新文件夹
2. 创建`SKILL.md`文件，遵循Claude Code skill格式
3. （可选）添加`references/`目录存放参考文档
4. 更新本README的"核心技能"部分

### 技能开发规范

- `SKILL.md`：skill主配置文件，包含name、description、核心功能
- `references/`：存放详细文档、规则、示例等
- 保持每个skill独立，互不依赖

---

## 核心技能

### intro-analysis (引言分析技能)

**位置**: `skills/intro-analysis/SKILL.md`

**输入**: 单个markdown文件，包含多篇论文的Abstract + Introduction

**输出**: 结构化综述报告（直接保存为文件，对话中仅显示简要摘要）

**核心功能**:
1. **文献调研** - 仅从引言部分完成研究开题报告背景部分
2. **多主题识别** - 自动识别所有研究方向，不预设任何主题
3. **可视化梳理** - 6种Mermaid图表展示复杂关系
4. **引言写作指导** - 学习顶刊Introduction三步法

**安装**:
```bash
cp -r skills/intro-analysis ~/.claude/skills/
```

---

## 分析流程

```
第一阶段：独立解析每篇文献
├── 文献元信息提取（完整引用格式）
├── 研究定位与第一性原理
├── 历史脉络（时间线）
├── 研究现状分类
├── 研究缺口（四类：空白/错误/矛盾/瓶颈）
├── 核心观点
├── 关键参考文献
├── 引言结构分析（顶刊三步法）
└── 引言质量评级

第二阶段：跨文献综合分析
├── 自动识别研究主题（不预设）
├── 每个主题的详细分析
├── 构建领域时间线
├── 观点追踪与论战
├── 观点依赖图
├── 论证流程图
├── 观点演进序列图
├── 研究范式状态图
└── 研究缺口综合

第三阶段：引言写作指导
├── 漏斗式开篇模式
├── 研究缺口陈述模式
├── 解决方案呈现模式
└── 高质量引言特征

第四阶段：生成综述报告（保存到本地文件）
```

---

## 可视化类型

| 可视化类型 | 用途 | 原文引用要求 |
|-----------|------|------------|
| **mindmap** | 主题关系全景 | 主题说明包含原文 |
| **timeline** | 领域发展时间线 | 每条记录包含原文 |
| **graph** | 观点依赖网络 | 每个节点包含原文 |
| **flowchart** | 论证逻辑流程 | 每个节点包含原文 |
| **sequence** | 观点演进序列 | 每条消息包含原文 |
| **state** | 研究范式转换 | 每条转换包含原文 |

---

## 反幻觉机制

### 双标签系统

| 标签 | 含义 | 使用场景 |
|-----|------|---------|
| `[原文声明]` | 论文明确声明的内容 | 作者直接表述的观点、贡献 |
| `[模型归纳]` | 基于分析的推断 | 从内容归纳但未明确声明的 |
| `[未明确给出]` | 论文未提及的信息 | 缺失字段，不猜测 |
| `[不确定]` | 有歧义的信息 | 标注歧义原因 |
| `[引用文献未详述]` | 二手引用信息不全 | 论文引用的原始工作描述不详 |

### 原文引用三要素

所有证据性论点必须包含：
1. **来源文献** - 使用完整引用格式（作者, 年份. 标题. 期刊. DOI/PMID）
2. **原文内容** - 保留原文英文，用 `「...」` 包裹
3. **位置标注** - 具体到段/句（Introduction第X段）

**示例**:
```markdown
作者在【Introduction第3段】中指出「Deep learning has demonstrated remarkable performance in medical image analysis」（paper_1）
```

---

## 文献可追溯性

每篇文献必须有完整身份标识：

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
```

自动生成完整引用格式：
```
完整格式：作者, 年份. 标题. 期刊. DOI/PMID
示例：Smith et al., 2023. Deep Learning in Medical Imaging. Nature Medicine. doi:10.1038/s41591-023-01234-5
```

---

## 输入文件格式

### 完整格式（推荐）

```markdown
---
id: paper_1
title: Paper Title
authors: Author List
year: 2024
journal: Journal Name (optional)
doi: 10.1234/xxx (optional)
pmid: 12345678 (optional)
---

## Abstract
Abstract content...

## Introduction
Introduction content...

---
id: paper_2
title: Another Paper
authors: ...
---
```

### Abstract-only格式（支持但受限）

```markdown
---
id: paper_1
title: Paper Title
authors: Author List
year: 2024
journal: Journal Name (optional)
doi: 10.1234/xxx (optional)
---

## Abstract
Abstract content...
```

> **注意**：Abstract-only论文可以提取研究问题、方法、贡献，但无法提取历史脉络、研究缺口等深度信息。

---

## 输出格式

### 本地保存的文件

**文件命名**：
```
[输入文件名]_intro_[日期].md
例如：medical_papers_intro_20260521.md
```

**报告内容**：
- Mermaid mindmap（研究主题全景）
- Mermaid timeline（领域发展时间线）
- Mermaid graph（观点依赖图）
- Mermaid flowchart（论证流程图）
- Mermaid sequence（观点演进序列图）
- Mermaid state（研究范式演进图）
- 观点溯源标注 `(id: paper_id, Introduction第X段)` + 原文引用
- 观点论战对比表格（含原文表述和标签）
- 每个主题的深度分析
- 文献逐篇独立分析
- 引言写作指南
- 参考文献索引（完整引用格式）

### 对话中显示的简要摘要

```markdown
✅ 分析完成

📊 分析统计
- 文献数量：N篇
- 识别主题：X个
- 时间跨度：[起始年] - [结束年]
- 数据来源：仅从Introduction部分提取

📁 输出文件
- 路径：/path/to/papers_intro_20260521.md
- 格式：Markdown (.md)
- 大小：[文件大小]

🔍 主要发现
- 核心主题1：[简要描述]
- 核心主题2：[简要描述]
- 主要争议：[简要描述]

💾 查看建议
- 文件已保存，可使用任何markdown编辑器查看
- 报告包含完整的Mermaid可视化图表
- 所有观点都有原始文献引用
```

---

## 设计原则

1. **反幻觉优先** - 绝对不编造任何论文未声明的内容
2. **双标签系统** - 每条观点标注 `[原文声明]` 或 `[模型归纳]`
3. **文献可追溯** - 每个观点都有完整引用格式和原文引用
4. **不确定性标记** - 所有不确定信息标注为 `[未明确给出]` 或 `[不确定]`
5. **仅依赖引言** - 所有信息从引言提取，无需阅读全文
6. **观点溯源** - 每个观点标注出处，便于验证
7. **独立分析** - 每篇文献先独立解析，再做跨文献综合
8. **论战清晰** - 对立观点并置展示，保留原文论证逻辑
9. **主题自动识别** - 不预设任何主题，从引言内容自动聚类
10. **可视化优先** - 复杂关系优先用图表展示，每个节点都有原文引用

---

## 常见幻觉模式规避

| 模式 | 错误做法 | 正确做法 |
|-----|---------|---------|
| 期刊猜测 | "发表于Nature" | `[未明确给出]` |
| 贡献膨胀 | 增加未声明的贡献 | 仅列出论文声明的贡献 |
| 结果外推 | "达到所有基准的SOTA" | 引用确切基准和指标 |
| 作者专长 | "计算机视觉专家" | 仅陈述论文声明的内容 |
| 未来工作编造 | 发明未来方向 | 仅引用论文的Future Work |
| 方法细节填充 | 猜测架构细节 | 标注为 `[未明确给出]` |
| 归因错误 | 将观点归于错误作者 | 确认观点的真正来源 |

---

## 目录结构

```
pyResearch-ReadingSkill/
├── skills/
│   └── intro_analysis/
│       ├── SKILL.md                      # Skill 主配置
│       └── evals/
│           └── evals.json                  # 测试用例
├── test_data/
│   └── sample_papers.md                   # 示例测试数据
├── README.md                             # 本文件
├── LICENSE                                # MIT 许可证
└── (其他文件)
```

---

## 适用领域

本技能集特别适用于：
- **生物医学计算** - 医学影像、基因组学、蛋白质科学
- **AI4S 领域** - 药物发现、科学计算、交叉学科
- **学术文献综述** - 研究背景调研、开题报告
- **引言写作指导** - 学习顶刊写作范式

---

## 技能集合规划

本仓库计划包含以下skill：

- ✅ **intro-analysis** - 批量文献引言分析（已实现）
- 🚧 [待开发] abstract-analysis - 批量摘要分析
- 🚧 [待开发] full-paper-analysis - 完整论文分析
- 🚧 [待开发] comparison-review - 多论文对比综述

**贡献新skill**：欢迎提交PR添加新skill，参考`intro-analysis`的结构

---

## 注意事项

- 专注于 paper 的阅读和分析
- 与 coding 技能集相对
- 重点利用 Introduction 部分完成文献调研工作
- **所有信息必须可追溯到原始文献**

### Abstract-only 论文的处理

如果你的文献只有 Abstract 没有 Introduction：
- **可提取内容**：研究问题、方法、主要贡献、简要结果
- **不可提取内容**：历史脉络、研究现状、研究缺口、关键参考文献
- **标注方式**：会使用 `[仅有Abstract，无法提取XXX]` 标注
- **分析影响**：不会参与需要历史脉络或研究缺口的综合分析

建议：
- 优先使用有 Introduction 的论文进行深度分析
- Abstract-only 论文可以作为补充参考
- 混合使用时，skill 会自动区分处理

---

## 添加新技能

在 `skills/` 下创建新文件夹，包含 `SKILL.md` 文件即可。

---

## 安装技能

将整个 `skills/` 文件夹或单个技能文件夹复制到你的 Claude skills 路径：
- Linux: `~/.claude/skills/`

---

## License

MIT License — Copyright (c) 2026

本项目以 MIT 许可证开源。你可以自由使用、修改和分发，但需保留原始版权声明。

完整许可证文本见 [LICENSE](LICENSE) 文件。

---

## Contributing

欢迎提交 Issue 和 Pull Request。

如果你在使用中发现引用错误、分析偏差或输出格式问题，欢迎在 Issue 中附上复现步骤（测试文件链接 + 触发词 + 错误输出片段）。
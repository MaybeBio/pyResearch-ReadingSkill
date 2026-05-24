# 原文引用与双标签系统

## 双标签系统 (Dual-Label System)

| 标签 | 含义 | 使用场景 | 示例 |
|-----|------|---------|------|
| `[原文声明]` | 论文明确声明的内容 | 作者直接表述的观点、贡献 | `该方法在低数据量下表现优异 [原文声明]` |
| `[模型归纳]` | 基于分析的推断 | 从内容归纳但未明确声明的 | `可能适用于小样本场景 [模型归纳]` |

## 证据标注 (Evidence Citation)

### 行内引用格式（短句）
```markdown
作者认为「Deep learning has demonstrated remarkable performance in medical image analysis」（PMID 12345678）
```

### 引用块格式（长段落）
```markdown
> "Deep learning has demonstrated remarkable performance in medical image analysis" (DOI 10.xxx/yyy)
```

### 引用三要素

所有证据性论点必须包含：
1. **来源文献**：使用DOI或PMID作为唯一标识
2. **原文内容**：保留原文英文，用 `「...」` 包裹

---

---

## 文献引用标识规则 ⭐

**所有文献引用必须使用DOI或PMID作为唯一标识符，禁止使用paper_01、paper_X等自编临时编号。**

原因：
- 临时编号（paper_01）在不同分析session中不一致，导致引用乱码
- 临时编号容易产生幻觉——标识错位、张冠李戴
- DOI/PMID是全局唯一的学术标识，可被任何人验证
- DOI优先于PMID（DOI更持久且可直接访问）

**正确写法**：`（PMID 36416266）` 或 `（DOI 10.1093/nar/gkac1055）`
**禁止写法**：`（paper_1）` ❌

在报告末尾的参考文献索引中使用DOI作为首选标识，无DOI时使用PMID。

---

## 原文-分析配对原则 (Citation-Analysis Pairing) ⭐

### 核心规则

**原文引用是证据，分析归纳是价值。二者缺一不可。**

> 每条 `[原文声明]` 必须搭配 `[模型归纳]` 分析。禁止连续堆砌原文引用而不作分析。

### 正确模式

```
[原文声明] 作者认为「原文内容」（PMID 12345678）
    ↓ （必须紧跟）
[模型归纳] 基于上述原文的推理分析，说明推理依据
```

### 禁止模式

```
❌ 错误：原文堆砌
[原文声明] 作者A认为「...」
[原文声明] 作者B认为「...」
[原文声明] 作者C认为「...」
（连续3条原文引用，无任何分析 — 这是文献堆砌，不是文献综述）
```

### 配对规则

| 规则 | 说明 |
|-----|------|
| **1配1** | 每条 `[原文声明]` 必须有紧随的 `[模型归纳]` 分析 |
| **先原文后分析** | `[原文声明]` → `[模型归纳]`，不可逆序 |
| **分析有据** | `[模型归纳]` 必须说明从原文的哪部分推演出该结论 |
| **禁止连续堆砌** | 最多连续2条 `[原文声明]` 后必须插入 `[模型归纳]` |
| **同主题多文献** | 可将多篇相关原文并列引用，后跟综合 `[模型归纳]` |

### 正确示例

```markdown
**[原文声明]** 作者A指出「Deep learning requires large labeled datasets」（PMID 12345678）

**[模型归纳]** 这表明数据标注成本是深度学习在医学影像中应用的核心瓶颈，该文献将此作为其研究动机的基础前提。

**[原文声明]** 作者B进一步指出「Data annotation in medical imaging is particularly expensive due to the need for expert radiologists」（PMID 87654321）

**[模型归纳]** 该文献将通用瓶颈具体化到医学领域，指出医学影像标注的特殊困难在于专家成本。与前一文献形成递进关系：从"标注稀缺"到"医学标注更加稀缺"。
```

---

## 分析深度层级

### Level 1: 简单总结

对单条原文的直接归纳。

**格式**：`[模型归纳]` + 一句话总结原文要点

**示例**：
```markdown
[原文声明] 「Our method achieves 95% accuracy on benchmark A」（PMID 11111111）
[模型归纳] 该方法在benchmark A上取得了competitive performance。
```

---

### Level 2: 跨文献关联

将多条原文关联、对比或互补。

**格式**：`[模型归纳]` + 关联分析（一致/矛盾/递进/补充）

**示例**：
```markdown
[原文声明] 文献指出「Method X excels in scenario A」（PMID AAAA）
[原文声明] 另一文献指出「Method X fails in scenario B」（PMID BBBB）
[模型归纳] 两篇文献对Method X的评价存在矛盾——在场景A表现优异但在场景B表现差，暗示Method X可能存在过拟合场景A的风险。该矛盾尚未在已有文献中得到明确讨论。
```

---

### Level 3: 深层推理

基于原文进行跨文献的综合推理，形成新的理解。

**格式**：`[模型归纳]` + 深层推理 + 推理依据说明

**示例**：
```markdown
[原文声明] 文献A指出「IDR binding is entropy-driven」（PMID AAAA）
[原文声明] 文献B指出「AlphaFold predicts local structure that may reflect bound-state conformations」（PMID BBBB）
[原文声明] 文献C指出「IDP conformations depend on amino acid composition」（PMID CCCC）

[模型归纳] 综合上述三点可以推演出一个框架：氨基酸序列 → 编码构象偏好 → 决定结合熵 → AlphaFold局部结构反映结合态。这意味着AlphaFold的低pLDDT区域可能并非"无结构"，而是编码了结合前的构象熵储备。该推演基于：（1）PMID AAAA的熵驱动机制，（2）PMID BBBB的结构预测观察，（3）PMID CCCC的序列-构象关系。但此框架尚未在文献中明确整合。
```

---

### 引用格式规范

**格式**：`（PMID 12345678）` 或 `（DOI 10.xxx/yyy）` — 仅需唯一ID。

**示例**：
```markdown
[原文声明] 作者指出「原文内容」（PMID 12345678）
[原文声明] 另一作者指出「原文内容」（DOI 10.xxx/yyy）
```
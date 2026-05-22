# 原文引用与双标签系统

## 双标签系统 (Dual-Label System)

| 标签 | 含义 | 使用场景 | 示例 |
|-----|------|---------|------|
| `[原文声明]` | 论文明确声明的内容 | 作者直接表述的观点、贡献 | `该方法在低数据量下表现优异 [原文声明]` |
| `[模型归纳]` | 基于分析的推断 | 从内容归纳但未明确声明的 | `可能适用于小样本场景 [模型归纳]` |

## 证据标注 (Evidence Citation)

### 行内引用格式（短句）
```markdown
作者认为「Deep learning has demonstrated remarkable performance in medical image analysis」（paper_1, Introduction第2段）
```

### 引用块格式（长段落）
```markdown
> "Deep learning has demonstrated remarkable performance in medical image analysis" (paper_1, Introduction, Para 2-5)
```

### 引用三要素

所有证据性论点必须包含：
1. **来源文献**：使用完整引用格式
2. **原文内容**：保留原文英文，用 `「...」` 包裹
3. **位置标注**：具体到段/句

---

---

## 原文-分析配对原则 (Citation-Analysis Pairing) ⭐

### 核心规则

**原文引用是证据，分析归纳是价值。二者缺一不可。**

> 每条 `[原文声明]` 必须搭配 `[模型归纳]` 分析。禁止连续堆砌原文引用而不作分析。

### 正确模式

```
[原文声明] 作者认为「原文内容」（paper_id, 位置）
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
**[原文声明]** 作者A指出「Deep learning requires large labeled datasets」（paper_1, Introduction第2段）

**[模型归纳]** 这表明数据标注成本是深度学习在医学影像中应用的核心瓶颈，paper_1将此作为其研究动机的基础前提。

**[原文声明]** 作者B进一步指出「Data annotation in medical imaging is particularly expensive due to the need for expert radiologists」（paper_2, Introduction第1段）

**[模型归纳]** paper_2将paper_1的通用瓶颈具体化到医学领域，指出医学影像标注的特殊困难在于专家成本。这与paper_1的观点形成递进关系：从"标注稀缺"到"医学标注更加稀缺"。
```

---

## 分析深度层级

### Level 1: 简单总结

对单条原文的直接归纳。

**格式**：`[模型归纳]` + 一句话总结原文要点

**示例**：
```markdown
[原文声明] 「Our method achieves 95% accuracy on benchmark A」（paper_1, Introduction第4段）
[模型归纳] 该方法在benchmark A上取得了competitive performance。
```

---

### Level 2: 跨文献关联

将多条原文关联、对比或互补。

**格式**：`[模型归纳]` + 关联分析（一致/矛盾/递进/补充）

**示例**：
```markdown
[原文声明] paper_1指出「Method X excels in scenario A」（paper_1, Introduction第3段）
[原文声明] paper_2指出「Method X fails in scenario B」（paper_2, Introduction第4段）
[模型归纳] paper_1和paper_2对Method X的评价存在矛盾——在场景A表现优异但在场景B表现差，暗示Method X可能存在过拟合场景A的风险。该矛盾尚未在已有文献中得到明确讨论。
```

---

### Level 3: 深层推理

基于原文进行跨文献的综合推理，形成新的理解。

**格式**：`[模型归纳]` + 深层推理 + 推理依据说明

**示例**：
```markdown
[原文声明] paper_1指出「IDR binding is entropy-driven」（paper_1, Introduction第2段）
[原文声明] paper_2指出「AlphaFold predicts local structure that may reflect bound-state conformations」（paper_2, Introduction第4段）
[原文声明] paper_3指出「IDP conformations depend on amino acid composition」（paper_3, Introduction第1段）

[模型归纳] 综合上述三点可以推演出一个框架：氨基酸序列 → 编码构象偏好 → 决定结合熵 → AlphaFold局部结构反映结合态。这意味着AlphaFold的低pLDDT区域可能并非"无结构"，而是编码了结合前的构象熵储备。该推演基于：（1）paper_1的熵驱动机制，（2）paper_2的结构预测观察，（3）paper_3的序列-构象关系。但此框架尚未在文献中明确整合。
```

---

### 位置标注规范

| 位置 | 格式 | 示例 |
|-----|------|------|
| Introduction第X段 | `（paper_1, Introduction第X段）` | `（paper_1, Introduction第2段）` |
| Abstract | `（paper_1, Abstract）` | `（paper_1, Abstract）` |
| Results第X段 | `（paper_1, Results第X段）` | `（paper_1, Results第3段）` |
| Conclusion | `（paper_1, Conclusion）` | `（paper_1, Conclusion段）` |
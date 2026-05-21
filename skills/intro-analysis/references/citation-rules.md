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

### 位置标注规范

| 位置 | 格式 | 示例 |
|-----|------|------|
| Introduction第X段 | `（paper_1, Introduction第X段）` | `（paper_1, Introduction第2段）` |
| Abstract | `（paper_1, Abstract）` | `（paper_1, Abstract）` |
| Results第X段 | `（paper_1, Results第X段）` | `（paper_1, Results第3段）` |
| Conclusion | `（paper_1, Conclusion）` | `（paper_1, Conclusion段）` |
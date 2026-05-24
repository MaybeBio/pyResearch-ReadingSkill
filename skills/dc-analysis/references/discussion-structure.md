# 讨论五步解析与结论三段结构

## Discussion 五步解析 (Hartley Method)

对每篇论文的Discussion，按五步法将内容归类到每一步骤，每步对应不同的信息提取目标。

### Step 1: 重述结论和成果

**提取目标**：作者认为最重要的发现是什么

**信号提示**：
- "our results show" / "we found that" / "this study demonstrates"
- "the results indicate" / "our data suggest"
- "we observed that" / "the analysis revealed"

**提取格式**：
```
[原文声明] 「作者的核心发现陈述」(PMID XXXXXXXX)
[模型归纳] 该发现的意义和在论文论证中的位置
```

### Step 2: 对比此次结果与以前结果

**提取目标**：与已有文献的异同、创新优势证据

**信号提示**：
- "compared with" / "in contrast to" / "unlike previous studies"
- "our method outperforms" / "superior to" / "achieves better"
- "consistent with" / "in line with" / "similar to" (一致)
- "different from" / "as opposed to" / "whereas" (不同)
- "extends" / "improves upon" / "goes beyond" (推进)

**提取格式**：
```
[对比优势] 「与X方法相比，我们的方法在Y方面更优」(PMID XXXXXXXX)
[模型归纳] 该对比优势的具体含义、对比对象的特征、优势的量化/定性依据
```

### Step 3: 列出局限性

**提取目标**：**真实问题的主要来源** — 作者诚实承认的不足

**信号提示**：
- "limitation" / "limited by" / "caveat"
- "however, our study" / "it should be noted that"
- "our study has several limitations"
- "the results should be interpreted with caution"
- "we cannot rule out" / "further validation is needed"

**提取格式**：
```
[原文声明] 「作者承认的局限性原文」(PMID XXXXXXXX)
[模型归纳] 该局限性的严重程度、对结论的影响范围、是否影响核心主张
```

**局限性分类**：
- **方法论局限**：方法本身的不足（精度、假设、简化）
- **数据局限**：样本量、数据质量、覆盖范围
- **范围局限**：泛化性、适用边界
- **概念局限**：理论框架的不足

### Step 4: 提出针对局限性的解决方案

**提取目标**：作者自己建议的改进路径

**信号提示**：
- "could be addressed by" / "future studies should"
- "to overcome this limitation"
- "a promising direction would be"
- "further work could" / "we suggest that"

**提取格式**：
```
[原文声明] 「作者建议的解决方案」(PMID XXXXXXXX)
[模型归纳] 该方案的可行性评估、是否已有初步探索
```

### Step 5: 提出新问题并建议进一步研究

**提取目标**：**开放问题的核心来源** — 研究揭露的、尚未解决的新方向

**信号提示**：
- "raises the question" / "remains unclear" / "remains to be determined"
- "future research should" / "further investigation is needed"
- "opens up" / "paves the way for" / "warrants further study"
- "it is unknown whether" / "the mechanism remains elusive"
- "an important open question" / "a key unanswered question"

**提取格式**：
```
[开放问题] 「作者提出的新问题原文」(PMID XXXXXXXX)
[模型归纳] 该问题的开放性程度、与该领域其他问题的关系、潜在的创新切入点
```

---

## Conclusion 三段结构

### Part 1: 概括研究内容

**提取目标**：用什么方法研究了什么问题

**信号提示**：
- "in this study, we" / "we investigated" / "using X method"
- "this work presents" / "here we show"

### Part 2: 主要结论

**提取目标**：得到了什么结果、说明了什么

**信号提示**：
- "our results indicate" / "we conclude that" / "the main finding"
- "this demonstrates" / "we have shown that"

### Part 3: 展望

**提取目标**：工作价值拔高 + 未来方向

**信号提示**：
- "this work provides" / "paves the way for" / "opens up a new avenue"
- "sheds new light on" / "has implications for"
- "future directions include" / "further research could"

**提取格式**：
```
[价值升华] 「作者拔高工作价值的陈述」(PMID XXXXXXXX)
[模型归纳] 该价值升华的具体所指、是否有充分证据支撑
```

---

## 解析规则

### 当Discussion未明确分节时
- 使用信号短语和主题转换识别步骤边界
- 段落级别主题建模归类内容
- 不确定的标注为 `[步骤归属不确定]`

### 当Discussion和Conclusion合并时
- 用五步+三段框架解析合并章节
- 标注哪些内容属于讨论、哪些属于结论
- 标记为 `[讨论-结论合并]`

### 讨论质量评级
- **优秀**：五步清晰，深度分析，具体对比，诚实局限
- **一般**：3-4步存在，有部分对比，承认局限
- **较差**：仅有重述，无对比，局限肤浅

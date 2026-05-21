# 可视化类型详细说明

## 6种Mermaid图表类型

### 1. Mindmap（主题关系全景）

**用途**：展示研究领域主题的层级关系和分类

**语法**：
```mermaid
mindmap
  root((领域名称))
    主题A
      子主题A1
      子主题A2
    主题B
      子主题B1
    主题C
      子主题C1
      子主题C2
```

**原文引用要求**：主题说明中包含原文引用

**示例**：
```mermaid
mindmap
  root((医学影像AI))
    深度学习
      CNN<br/>「CNN achieved SOTA」<br/>(paper_1, Intro Para 2)
      Transformer<br/>「Transformer emerging」<br/>(paper_2, Intro Para 3)
    联邦学习
      隐私保护<br/>「Privacy concerns」<br/>(paper_3, Intro Para 1)
      通信效率<br/>「Communication bottleneck」<br/>(paper_3, Intro Para 4)
    数据增强
      合成数据<br/>「Synthetic data helps」<br/>(paper_4, Intro Para 2)
```

---

### 2. Timeline（领域发展时间线）

**用途**：展示历史脉络、里程碑事件的时间演进

**语法**：
```mermaid
timeline
    title 领域研究演进时间线
    1990s : 早期探索<br/>「首次提出X方法」(Smith et al., 1995, paper_1)
    2005 : 里程碑<br/>「确立Y范式」(Jones et al., 2005, paper_2)
    2018-2020 : 快速发展<br/>「提出Z架构」(Lee et al., 2019, paper_3)
```

**原文引用要求**：每条时间线记录包含原文引用

**示例**：
```mermaid
timeline
    title 医学影像AI发展时间线
    1990-2000 : 早期探索<br/>「Traditional image processing methods dominated medical imaging」<br/>(paper_1, Intro Para 2)
    2012 : 深度学习突破<br/>「AlexNet demonstrated the potential of deep learning in computer vision」<br/>(paper_2, Intro Para 3)
    2015-2018 : 医学应用爆发<br/>「Deep learning achieved state-of-the-art performance in medical image analysis」<br/>(paper_3, Intro Para 1)
    2020-2024 : 多模态与大模型<br/>「Large-scale multimodal models emerged」<br/>(paper_4, Intro Para 2)
```

---

### 3. Graph（观点依赖网络）

**用途**：展示观点之间的依赖、反驳、扩展关系

**语法**：
```mermaid
graph TD
    %% 基础观点节点
    A[「观点A」<br/>(paper_1, Intro Para 2)]:::base
    B[「观点B」<br/>(paper_2, Intro Para 3)]:::base

    %% 依赖关系
    C[「观点C」<br/>(paper_3, Intro Para 4)] --> A
    C --> B

    %% 反驳关系
    D[「观点D」<br/>(paper_4, Intro Para 5)] -.->|反驳| C

    %% 样式定义
    classDef base fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    classDef derived fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef counter fill:#ffebee,stroke:#b71c1c,stroke-width:2px

    class A,B base
    class C derived
    class D counter
```

**原文引用要求**：每个节点包含原文引用

**关系类型**：
- `A --> B`：直接依赖
- `A -.引出.-> B`：引出关系
- `A -.反驳.-> B`：反驳关系
- `A -.扩展.-> B`：扩展关系
- `A -.基于.-> B`：基于关系

**样式分类**：
- `base`：基础观点（蓝色）
- `derived`：衍生观点（橙色）
- `counter`：反驳观点（红色）

---

### 4. Flowchart（论证流程图）

**用途**：展示单个或多个文献的论证逻辑链

**语法**：
```mermaid
flowchart TD
    Start[「问题陈述」<br/>(paper_1, Intro Para 1)] --> Background1[「历史背景1」<br/>(paper_1, Intro Para 2)]
    Background1 --> Background2[「历史背景2」<br/>(paper_2, Intro Para 3)]
    Background2 --> Gap1[「研究缺口1」<br/>(paper_1, Intro Para 4)]
    Gap1 --> CounterArgument[「反方观点」<br/>(paper_2, Intro Para 5)]
    CounterArgument --> Gap2[「研究缺口2」<br/>(paper_1, Intro Para 5)]
    Gap2 --> Solution[「提出方案」<br/>(paper_1, Intro Para 6)]
    Solution --> Contribution[「贡献总结」<br/>(paper_1, Intro Para 7)]
```

**原文引用要求**：每个节点包含原文引用

---

### 5. Sequence（观点演进序列图）

**用途**：展示观点随时间的演进和文献间的对话

**语法**：
```mermaid
sequenceDiagram
    participant Paper2015 as Paper A<br/>(Smith et al., 2015)
    participant Paper2018 as Paper B<br/>(Jones et al., 2018)
    participant Paper2021 as Paper C<br/>(Lee et al., 2021)
    participant Paper2024 as Paper D<br/>(Zhang et al., 2024)

    Paper2015->>Paper2018: 提出「观点X」<br/>(Intro Para 3)
    Note over Paper2015,Paper2018: 原文: "We propose X..."
    Paper2018->>Paper2021: 支持「观点X」<br/>扩展至场景Y<br/>(Intro Para 4)
    Note over Paper2018,Paper2021: 原文: "Building on X, we..."
    Paper2021-->>Paper2024: 质疑「观点X」<br/>提出「反驳观点Z」<br/>(Intro Para 5)
    Note over Paper2021,Paper2024: 原文: "However, X fails to..."
    Paper2024->>Paper2024: 综合观点X和Z<br/>提出「新观点W」<br/>(Intro Para 6)
    Note over Paper2024: 原文: "Combining X and Z..."
```

**原文引用要求**：每条消息包含原文引用

---

### 6. State（研究范式状态转换图）

**用途**：展示研究范式的转换和演进

**语法**：
```mermaid
stateDiagram-v2
    [*] --> 传统方法: 1990-2010<br/>(paper_1, Intro Para 2)
    传统方法 --> 深度学习: 2012 AlexNet突破<br/>(paper_1, Intro Para 3)
    深度学习 --> 联邦学习: 2016-2018 隐私需求<br/>(paper_2, Intro Para 4)
    联邦学习 --> 多模态融合: 2020-2021<br/>(paper_3, Intro Para 5)
    多模态融合 --> 大模型: 2022-2024<br/>(paper_4, Intro Para 6)

    note right of 深度学习
        主流范式<br/>「性能优异但缺数据」<br/>[原文声明]
        (paper_1, Intro Para 3)
    end note

    note left of 联邦学习
        解决数据孤岛<br/>「但通信开销大」<br/>[原文声明]
        (paper_2, Intro Para 5)
    end note
```

**原文引用要求**：每条转换包含原文引用

---

## 复杂表格设计原则

### 多维度对比表

| 观点主题 | 观点表述（原文） | 标签 | 支持文献 | 反对/质疑文献 | 依赖观点 | 证据 |
|---------|-----------------|------|---------|--------------|---------|------|
| X方法有效 | 「X method achieves state-of-the-art performance on scenario A」 | [原文声明] | paper_a, paper_c | paper_d | - | (paper_a, Intro Para 3) |
| X方法局限 | 「X method fails to generalize to scenario B」 | [原文声明] | paper_d | - | - | (paper_d, Intro Para 4) |
| 可能适用 | 「May have potential in low-resource settings」 | [模型归纳] | - | - | 观点1 | 实验数据有限 |

### 设计原则

1. **多维度对比**：不只列出支持/反对，还要显示依赖关系、演进趋势
2. **关系编码**：使用符号、颜色、边框区分不同类型的关系
3. **可追溯性**：每个观点都有来源标注和原文引用
4. **层次清晰**：主观点→子观点→论证细节的层次结构
5. **标签明确**：每条观点都有 `[原文声明]` 或 `[模型归纳]` 标签

---

## 可视化选择指南

| 场景 | 推荐图表类型 | 原因 |
|-----|------------|------|
| 展示研究领域分类和层级 | mindmap | 直观显示主题结构和子主题关系 |
| 展示历史发展脉络 | timeline | 时间序列清晰，便于追踪演进 |
| 展示观点之间的复杂关系 | graph | 支持节点间多种关系类型（依赖、反驳、扩展） |
| 展示论证逻辑链条 | flowchart | 线性流程清晰，便于理解推理过程 |
| 展示文献间的观点演进 | sequence | 时间顺序明确，便于追踪观点的传承和变化 |
| 展示研究范式的转换 | state | 状态变化清晰，便于理解范式转移 |

---

## 图表使用注意事项

1. **原文引用**：所有图表节点都必须包含原文引用和位置标注
2. **标签标注**：所有观点必须标注 `[原文声明]` 或 `[模型归纳]`
3. **图例说明**：每个图表都应有清晰的图例说明
4. **简洁明了**：避免节点过多，每张图控制在20个节点以内
5. **语法正确**：确保Mermaid语法正确，避免渲染失败
6. **可读性**：节点文字简洁，关键信息用原文引用支撑
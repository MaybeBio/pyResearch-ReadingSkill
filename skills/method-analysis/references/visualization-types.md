# 可视化类型详解 (method-analysis)

## 7种Mermaid图表 + 3种表格

---

### 1. 问题拆解树 (Mermaid graph) ⭐

**用途**：展示问题多层次拆解为子问题树的层级结构。深度≥3层。标注用户原始问题+桥梁开放问题的嫁接关系。

```mermaid
graph TD
    Q["🟢 用户原始问题<br/>[用户问题陈述]"]:::user
    Q --> B1["🔗 桥梁 OP-X<br/>[嫁接的开放问题]"]:::bridge
    Q --> B2["🔗 桥梁 OP-Y<br/>[嫁接的开放问题]"]:::bridge
    B1 --> S1["子问题1<br/>[描述]"]:::sub
    B1 --> S2["子问题2<br/>[描述]"]:::sub
    B2 --> S3["子问题3<br/>[描述]"]:::sub
    S1 --> S1a["子问题1.1"]:::deep
    S1 --> S1b["子问题1.2"]:::deep
    S3 --> S3a["子问题3.1"]:::deep

    classDef user fill:#c8e6c9,stroke:#2e7d32,stroke-width:3px
    classDef bridge fill:#fff9c4,stroke:#f57f17,stroke-width:2px,stroke-dasharray:5 5
    classDef sub fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef deep fill:#f5f5f5,stroke:#757575,stroke-width:1px
```

---

### 2. 方法全景脑图 (Mermaid mindmap) ⭐

**用途**：展示全域Method + README中可复用组件按Pipeline阶段归类。

```mermaid
mindmap
  root((方法全景<br/>方案组件总览))
    数据层
      DIBS数据库
        700+ IDP-protein复合物<br/>PMID 39763873
      PED构象集合
        NMR/MD ensemble<br/>PMID 37904608
    特征层
      pLM Embedding
        ESM-2 ProtT5<br/>PMID 39763873
      手工特征
        氨基酸组成+PSSM<br/>PMID 41959048
    模型层
      partner-dependent
        Disobind outer product<br/>PMID 39763873
      动态感知
        DynamicGT几何变换器<br/>PMID 41435823
      迁移学习
        TIDGN预训练+微调<br/>PMID 40360271
    训练层
      损失函数
        BCE / Focal Loss
      优化器
        AdamW / SGD+Momentum
    评估层
      标准指标
        AUC MCC F1
      自创指标
        构象合理性得分
```

---

### 3. 架构Mermaid Schematic ⭐

**用途**：展示推荐方案的模型架构数据流和模块连接。

```mermaid
flowchart TD
    Input["输入: IDR序列 + Partner序列<br/>(PMID XXXXXXXX)"]:::input
    EncA["IDR Encoder<br/>ESM-2 Embedding<br/>(PMID 39763873)"]:::encoder
    EncB["Partner Encoder<br/>ESM-2 Embedding<br/>(PMID 41959048)"]:::encoder
    Cross["交叉注意力模块<br/>Cross-Attention<br/>(PMID 41435823)"]:::core
    Pool["Global Pooling<br/>加权平均"]:::pool
    Head["预测头<br/>MLP → Sigmoid<br/>(PMID 39763873)"]:::head
    Out["输出: 结合位点概率图"]:::output

    Input --> EncA
    Input --> EncB
    EncA --> Cross
    EncB --> Cross
    Cross --> Pool
    Pool --> Head
    Head --> Out

    classDef input fill:#e1f5fe,stroke:#01579b
    classDef encoder fill:#e8f5e9,stroke:#2e7d32
    classDef core fill:#fff3e0,stroke:#e65100,stroke-width:3px
    classDef pool fill:#f3e5f5,stroke:#4a148c
    classDef head fill:#ffebee,stroke:#b71c1c
    classDef output fill:#e8f5e9,stroke:#2e7d32
```

---

### 4. 方案Fork对比图 (Mermaid graph)

**用途**：展示关键环节的多个可选方案及其取舍关系。

```mermaid
graph TD
    Decision["🔀 架构选择"]:::decision
    PlanA["方案A: 双塔+交叉注意力<br/>精度优先<br/>GPU: 24GB+"]:::plan_a
    PlanB["方案B: 单塔+拼接<br/>效率优先<br/>GPU: 8GB+"]:::plan_b
    PlanC["方案C: 全Transformer<br/>探索优先<br/>GPU: 40GB+"]:::plan_c
    
    Decision --> PlanA
    Decision --> PlanB
    Decision --> PlanC

    classDef decision fill:#fff9c4,stroke:#f57f17,stroke-width:3px
    classDef plan_a fill:#c8e6c9,stroke:#2e7d32
    classDef plan_b fill:#e1f5fe,stroke:#01579b
    classDef plan_c fill:#ffcdd2,stroke:#b71c1c
```

---

### 5. 方案-风险-Fork逻辑链 (Mermaid graph)

**用途**：展示高风险的备选路径。

```mermaid
graph LR
    Main["主方案: 方案A"]:::main
    Risk["⚠️ 风险: 交叉注意力<br/>O(n²)复杂度可能不可行"]:::risk
    ForkB["Fork: 切换到方案B<br/>concat替代attention"]:::fork
    ForkC["Fork: 稀疏注意力<br/>O(n log n)"]:::fork
    Fallback["回退: 线性注意力<br/>O(n)"]:::fallback

    Main --> Risk
    Risk --> ForkB
    Risk --> ForkC
    ForkC -.->|仍不可行| Fallback

    classDef main fill:#c8e6c9,stroke:#2e7d32,stroke-width:3px
    classDef risk fill:#ffcdd2,stroke:#b71c1c
    classDef fork fill:#e1f5fe,stroke:#01579b
    classDef fallback fill:#fff3e0,stroke:#e65100
```

---

### 6. 训练策略对比表

| 组件 | 方案A（推荐） | 方案B（备选） | 选择条件 |
|------|------------|------------|---------|
| Loss | BCE | Focal Loss | 正负比>10:1选Focal |
| Optimizer | AdamW lr=1e-4 | SGD+Momentum | 大数据集选SGD |
| Scheduler | Cosine Annealing | ReduceLROnPlateau | 不确定epoch数选后者 |
| Regularization | Dropout 0.3 | Dropout 0.5 | 小模型加dropout |

---

### 7. 方案分支Fork树 ⭐（新增）

**用途**：展示每个子问题的多个解决方案分支，每分支可再fork产生子方案。递归展开直至触及可实现性边界。

```mermaid
graph TD
    SP1["子问题1: 序列编码"]:::sub
    SP1 --> FA["方案A: pLM embedding<br/>ESM-2/ProtT5<br/>PMID 39763873, 41959048<br/>仓库: facebookresearch/esm"]:::plan
    SP1 --> FB["方案B: 手工特征<br/>AA组成+PSSP+物化<br/>PMID 38018910"]:::plan
    SP1 --> FC["方案C: 混合特征<br/>pLM + 手工concat<br/>[模型归纳·方案推演]"]:::plan
    FA --> FA1["子方案A1: Frozen ESM-2<br/>仅微调下游MLP<br/>仓库: isblab/disobind"]:::subplan
    FA --> FA2["子方案A2: Fine-tune ESM-2<br/>全参数调优<br/>仓库: HFChenLab/PhantoIDP"]:::subplan
    FA1 --> FA1a["子方案A1a: 残基级<br/>每个残基独立embedding<br/>仓库: HFChenLab/PhantoIDP"]:::deep
    FA1 --> FA1b["子方案A1b: 粗粒化<br/>AvgPool1d k=5<br/>仓库: isblab/disobind"]:::deep

    classDef sub fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef plan fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
    classDef subplan fill:#e1f5fe,stroke:#01579b,stroke-width:1.5px
    classDef deep fill:#f3e5f5,stroke:#4a148c,stroke-width:1px
```

---

### 8. 交叉互作矩阵图 (Mermaid graph) ⭐（新增）

**用途**：展示不同方法/仓库之间的交叉组合关系。行=方法A的组件，列=方法B的组件，交叉点=可行的组合方案。

```mermaid
graph LR
    subgraph 方法A_Disobind
        A1["OuterProduct<br/>交互块"]:::comp_a
        A2["SE Loss<br/>稀疏训练"]:::comp_a
        A3["Coarse-graining<br/>k=5"]:::comp_a
    end
    subgraph 方法B_PhantoIDP
        B1["GCN Encoder<br/>图编码"]:::comp_b
        B2["VAE生成<br/>构象采样"]:::comp_b
        B3["FAPE Loss<br/>SE3等变"]:::comp_b
    end
    subgraph 方法C_DynamicGT
        C1["动态感知<br/>bound+unbound"]:::comp_c
        C2["几何Transformer<br/>图注意力"]:::comp_c
    end
    subgraph 交叉组合
        X1["🔀 A1+B1→交互图编码<br/>[方案推演]"]:::cross
        X2["🔀 A2+B3→等变稀疏Loss<br/>[方案推演]"]:::cross
        X3["🔀 A1+C2→几何交互块<br/>[方案推演]"]:::cross
        X4["🔀 B2+C1→条件动态生成<br/>[方案推演]"]:::cross
    end
    A1 --> X1; B1 --> X1
    A2 --> X2; B3 --> X2
    A1 --> X3; C2 --> X3
    B2 --> X4; C1 --> X4

    classDef comp_a fill:#c8e6c9,stroke:#2e7d32
    classDef comp_b fill:#e1f5fe,stroke:#01579b
    classDef comp_c fill:#fff3e0,stroke:#e65100
    classDef cross fill:#ffcdd2,stroke:#b71c1c,stroke-width:2px,stroke-dasharray:5 5
```

---

### 7. 方法缝合溯源表

| 方案组件 | 来源论文(PMID/DOI) | 原文引用 | 开源仓库 | 缝合策略 | Pipeline位置 |
|---------|-------------------|---------|---------|---------|------------|
| 双塔embedding | PMID 39763873 | 「原文描述」 | Disobind | 组合 | 模型层→Encoder |
| ESM-2特征 | PMID 41959048 | 「原文描述」 | IDBSpred | 组合 | 特征层 |
| 交叉注意力 | PMID 41435823 | 「原文描述」 | DynamicGT | 迁移 | 模型层→交互 |

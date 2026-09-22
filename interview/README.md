# AI Infra 面试需求轴

本目录以 [AIInfraGuide 官方仓库](https://github.com/caomaolufei/AIInfraGuide)的 `docs/interview/*.md` 为主要读取入口，整理其中的公司面经、综合题库和面试问题，并将它们映射到四阶段知识主线；[部署后的面试宝典](https://caomaolufei.github.io/AIInfraGuide/interview/)只用于公开 URL 与渲染结果核对。当前固定源码版本统计为 181 篇面经、65 家公司/分组和 7 个梯队；这是网站收录统计，不直接等同于行业频率。

它不是独立背题库：

- `notes/` 负责解释知识体系；
- `examples/` 负责必要的代码阅读；
- `interview/` 负责真实问题、考察意图、回答骨架和递进追问；
- `roadmap/progress.md` 负责记录当前知识与面试验收状态。

## 目录

- `source-index.md`：固定源码版本、来源索引、页面元数据、综合题库主题和核查状态。
- `core-question-map.md`：从 10 篇综合面经固定正文中提取、语义去重并映射到四阶段的第一版具体题卡索引。
- `00-prerequisites/`：编程、数学、Transformer、PyTorch、GPU 与集合通信。
- `01-cuda-operators/`：CUDA、GPU 架构、算子手撕、Triton 和性能分析。
- `02-distributed-training/`：显存账本、并行策略、精度、MoE 和训练系统。
- `03-inference-serving/`：KV Cache、引擎、量化、推测解码、调度和 Benchmark。

## 题目分级

- `core`：主线核心机制，或能明显区分是否真正理解；必须掌握。
- `important`：常见工程追问或重要扩展；应掌握。
- `supplementary`：公司、岗位或版本特定细节；按需学习。

除非来源样本足够，不能把个别面经题目直接称为“行业高频”。

## 状态

- `unseen`：尚未学习；
- `learning`：正在建立回答；
- `can-outline`：能给出回答骨架，但追问不稳定；
- `mastered`：能结构化回答并处理关键追问；
- `review`：需要复习。

## 每题模板

```markdown
## 题目

- ID：
- 级别：core / important / supplementary
- 状态：unseen / learning / can-outline / mastered / review
- 所属阶段：
- 来源：
- 原始分类、公司或岗位：

### 考察意图

### 回答骨架

1. 直接结论或定义
2. 机制与数据流
3. 必要推导
4. Trade-off 与边界
5. 如何验证

### 常见错误

### 递进追问

### 关联笔记、代码与资料
```

回答骨架不是逐字背诵稿，应允许根据问题上下文调整。

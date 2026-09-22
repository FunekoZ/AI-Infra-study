# AI Infra Study

个人 AI Infra **对话式、理解导向的系统学习仓库**。知识主线与真实需求轴都以 [AIInfraGuide 官方仓库](https://github.com/caomaolufei/AIInfraGuide) 源码为主要读取入口，并通过[学习路线页面](https://caomaolufei.github.io/AIInfraGuide/guides/ai-infra%E5%AD%A6%E4%B9%A0%E8%B7%AF%E7%BA%BF/)和[面试宝典](https://caomaolufei.github.io/AIInfraGuide/interview/)抽样核对公开部署结果。

默认形式：

> 我提问 → Claude 定位当前主线 → 回答并按需提供带注释教学代码 → 判断是否应回归主线 → 给出一个明确下一步。

本仓库不要求实际运行代码，但会在知识点确有需要时构建小型代码文件，帮助理解 PyTorch、CUDA、分布式训练和推理系统中的必要代码。代码会注明 shape、dtype、device 假设、关键数据流、简化之处以及“未经本环境运行验证”。

## 外部基准读取方式

默认采用 **GitHub source-first、deployed website verification、primary-source fact-checking**：

- 从 AIInfraGuide 官方仓库的 Markdown、frontmatter、collection schema 和页面分组代码批量恢复路线与面试原文；
- 每轮正式同步记录上游 `main` 的 commit SHA 和核对日期，题目引用保留源文件路径、题号和公开页面 URL；
- 部署网站只做公开链接、导航、统计和渲染结果的抽样核对，不再逐页抓取作为主要输入；
- 技术机制、公式、版本和性能结论仍回到论文、标准、官方文档或对应项目官方仓库核查；
- 临时浅克隆放入忽略提交的 `.cache/AIInfraGuide/`，本仓库只提交提炼后的路线、题卡和来源快照。

当前固定版本、源文件路径、统计复核和增量更新流程见 [resources/ai-infra-guide-source.md](resources/ai-infra-guide-source.md)。

## 学习主线

1. **前置知识**：Python、C/C++、Linux、数学、Transformer、PyTorch、GPU 与集合通信。
2. **CUDA 与算子优化**：GPU 架构、内存层次、Kernel、Reduce、GEMM、Softmax、FlashAttention、Triton 和性能分析。
3. **分布式训练**：优化器显存、DDP、FSDP、ZeRO、TP、PP、SP、MoE、混合精度和重计算。
4. **推理与部署**：Prefill/Decode、KV Cache、PagedAttention、Continuous Batching、量化、Speculative Decoding、Prefill/Decode 解耦和 Benchmark 方法论。

完整路线见 [roadmap/learning-path.md](roadmap/learning-path.md)，当前唯一进度指针见 [roadmap/progress.md](roadmap/progress.md)。

## 双轴学习：知识主线与真实面试需求

本仓库不把面试准备放到学习结束后才突击，而是把 AIInfraGuide 官方仓库 `docs/interview/` 中的公司面经和综合题库嵌入每个主题，并通过[部署后的面试宝典](https://caomaolufei.github.io/AIInfraGuide/interview/)抽样核对公开入口。当前固定源码版本统计为 181 篇面经、65 家公司、7 个梯队；这些是该版本的收录统计，不代表行业总体频率：

- **知识主线**保证概念依赖和系统结构完整；
- **面试需求轴**校准真实岗位关注点、回答深度、定量能力和工程 trade-off；
- 当前主题完成前，需要同时通过知识理解与代表性面试题验收；
- 面经用于发现需求，不被视为绝对技术事实；答案仍需由论文、官方资料、可靠讲解或推导核查；
- 不背逐字答案，而是掌握“定义/问题 → 机制 → 推导 → trade-off → 边界 → 验证”的回答骨架。

## 长期复盘

已解决的问题，以及花费较久、容易遗忘的知识点，记录在 [notes/review-index.md](notes/review-index.md)。每条记录保留原始问题、最短结论、突破点、复习自检和原网站的页面/章节/题目定位，方便隔一段时间重新复习。

相关索引与阶段题库放在 `interview/`。

## 对话学习原则

- 每次回答先说明当前位于网站路线的哪个阶段和主题。
- 基础、旁支和跨阶段问题都可以回答，但先判断它是否阻塞主线。
- 必要前置采用“最小充分解释”：补到足以理解当前主题后立即回归。
- 任意时刻默认只维护一个主线和至多一个临时分支。
- 每次只给一个下一步，并说明目标、原因和完成标准。
- 阅读过讲解或代码不等于掌握；能够复述、推导、比较或解释关键代码后，才记为已掌握。

详细规则见 [CLAUDE.md](CLAUDE.md)。

## 教学代码

教学代码保存于 `examples/<stage>/`，与学习路线阶段一一对应。

- 代码服务于阅读和概念映射，不要求执行。
- 每个文件聚焦一个知识点，包含充分中文注释。
- 不构建无关脚手架、部署工程或大型实验框架。
- 若未实际执行，会明确标记为“仅供阅读，未经本环境运行验证”。

## 资料使用

资料不限于原始论文和官方文档，也可使用经核查的高质量网络讲解，包括网站作者推荐的知乎专栏、个人技术文章、源码导读和视频。

使用优先级：

1. 原始论文、标准、官方文档、官方仓库；
2. 大学课程、研究机构、业内专家和有良好引用的技术文章；
3. 经交叉核查的知乎专栏、博客、社区教程和视频。

二手资料用于直觉和中文解释时，会核查引用、版本、公式和关键结论；无法充分核实时会明确不确定性。需要逐节精读或反复引用的资料可按需保存到 `resources/`，不会一次性批量下载。

## 精简目录

```text
.
├── README.md
├── CLAUDE.md
├── roadmap/                    # 路线与当前进度
├── notes/                      # 四阶段主题笔记与长期复盘索引
│   ├── review-index.md         # 已解决问题、难点和原网站定位
├── examples/                   # 四阶段带注释教学代码
├── interview/                  # 网站面试宝典、面经索引与阶段题库
└── resources/
    ├── resources.yaml          # 资料元数据、来源层级和核查状态
    ├── papers/                 # 按需下载的论文
    └── docs/                   # 按需保存的文档或文章
```

初期不保留独立的实验、Benchmark 和全局素材目录；未来确有实际实验需求时再按需建立，避免仓库过早膨胀。

## 主题完成标准

一个主题通常需要做到：

- 能说明它解决什么问题以及瓶颈在哪里；
- 能描述关键数据流；
- 能推导主要公式、shape、复杂度、显存或通信量；
- 能比较相关方案的适用条件与 trade-off；
- 能解释必要教学代码中的输入输出和关键语句；
- 能回答关键误区检查题；
- 能对对应的核心面试题给出结构化回答，并承接机制或定量追问；
- 能说明真实系统中如何验证，但不要求亲自执行。

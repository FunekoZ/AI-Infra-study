# 面试材料来源索引

> 主要读取入口：[AIInfraGuide 官方仓库](https://github.com/caomaolufei/AIInfraGuide)的 `docs/interview/*.md`
>
> 公开入口：[AIInfraGuide 面试宝典](https://caomaolufei.github.io/AIInfraGuide/interview/)
>
> 当前固定版本：`main@a3b63eeb81d6d36a3c42c8cfc5a1bdd96e36bab1`，核对日期 2026-09-22。详细源文件、统计口径和内容指纹见 [AIInfraGuide 上游来源快照](../resources/ai-infra-guide-source.md)。10 篇综合面经已拆成第一版题卡；其他公司叶子面经继续按主题增量整理。目录标题只能证明页面存在，具体题目必须回到固定版本正文。

## 收录规模

对固定 commit 的 `docs/interview/*.md` frontmatter 直接统计：

- **181 篇面经**；
- **65 家公司**；
- **7 个梯队**。

这些数字是网站当前收录统计，不代表整个行业的公司覆盖率或题目频率。

## 核心入口

| 标题 | 类型 | URL | 核查状态 | 说明 |
|---|---|---|---|---|
| AIInfraGuide 面试宝典 | 面试总目录 | https://caomaolufei.github.io/AIInfraGuide/interview/ | 部署抽样已核对 | 公开 URL、导航和渲染结果核对入口；不作为批量正文读取入口。 |
| AI Infra 学习路线 | 知识路线 | https://caomaolufei.github.io/AIInfraGuide/guides/ai-infra%E5%AD%A6%E4%B9%A0%E8%B7%AF%E7%BA%BF/ | 源码与部署已核对 | 四阶段知识主线、推荐资料和实践能力要求；源文件为 `docs/guides/AI Infra学习路线.md`。 |
| AIInfraGuide 官方仓库 | 仓库 | https://github.com/caomaolufei/AIInfraGuide | 固定 commit 已核对 | 当前主要读取入口；版本、路径、统计和内容指纹见 `resources/ai-infra-guide-source.md`。 |
| CUDA 手撕算子 · 面试练习 | 外部专题练习 | https://kkcocoa.github.io/cuda-operator-interview/ | 入口已确认 | 学习路线推荐的 CUDA 面试练习，不是面试宝典首页的独立栏目。 |

## 源码目录对应的部署分组

| 梯队 | 篇数 | 公司/分组数 | 首页描述 | 学习映射倾向 |
|---|---:|---:|---|---|
| T0 大厂 | 53 | 4 | 系统设计、深层性能优化、大规模分布式训练与推理经验 | 四阶段综合，重点阶段 2、3 |
| T1 大厂/独角兽 | 32 | 11 | 工程实现、框架使用和项目实践 | 阶段 1、2、3 |
| T2 AI 独角兽 | 9 | 5 | 前沿技术理解、模型优化与创新方案 | 阶段 1、2、3 |
| T3 芯片/硬件 | 22 | 14 | 硬件底层、CUDA 与算子开发、编译器优化 | 重点阶段 1 |
| T4 车企/自驾 | 24 | 9 | 边缘部署、模型压缩和端侧推理优化 | 重点阶段 1、3 |
| T5 其他 | 31 | 21 个子栏目 | 基础知识、项目匹配程度与学习能力 | 阶段 0 及综合基础 |
| 综合面经 | 10 | 1 个综合分组 | 多方向通用面试题库 | 四阶段综合 |

## 公司与机构覆盖

### T0 大厂

- 百度：17 篇
- 阿里巴巴：16 篇
- 字节跳动：13 篇
- 腾讯：7 篇

### T1 大厂/独角兽

- 快手：9 篇
- 小米：5 篇
- 蚂蚁：4 篇
- 美团：4 篇
- 华为：2 篇
- 京东：2 篇
- OPPO：2 篇
- 拼多多、B站、网易、vivo：各 1 篇

### T2 AI 独角兽

- MiniMax：4 篇
- 旷视科技：2 篇
- 阶跃星辰、商汤、智谱：各 1 篇

### T3 芯片/硬件

- 三星、太初：各 3 篇
- 壁仞科技、飞腾、沐曦、英伟达：各 2 篇
- 北极雄芯、寒武纪、后摩智能、摩尔线程、遂原科技、燧原科技、原粒半导体、中兴：各 1 篇

网站把“遂原科技”和“燧原科技”列为两个栏目，本索引按页面原样保留，尚未自行合并。

### T4 车企/自驾

- 蔚来：6 篇
- 卓驭分组：5 篇，其中包含页面列出的“大疆车载”条目
- 理想汽车、小鹏汽车：各 3 篇
- 文远知行、元戎启行：各 2 篇
- 辉羲智能、小马智行、易控智驾：各 1 篇

### T5 其他

- 小厂综合：5 篇
- 海康威视、科大讯飞：各 3 篇
- 荣耀、智源研究院：各 2 篇
- 贝壳、传音、格灵深瞳、好未来、经纬恒润、联想、米哈游、南湖研究院、上海 AI 实验室、识渊科技、数坤科技、虾皮、小光子、中科类脑、中科曙光、TeleAI：各 1 篇

## 综合面经入口

综合栏目共 10 篇，其中首页明确命名了 7 份“综合面经题库”：

1. [AI Infra 一面](https://caomaolufei.github.io/AIInfraGuide/interview/ai-infra-一面)
2. [AI Infra 校招 (1)](https://caomaolufei.github.io/AIInfraGuide/interview/ai-infra-校招-1)
3. [AI Infra 综合面经题库 (1)](https://caomaolufei.github.io/AIInfraGuide/interview/ai-infra-综合面经题库-1)
4. [AI Infra 综合面经题库 (2)](https://caomaolufei.github.io/AIInfraGuide/interview/ai-infra-综合面经题库-2)
5. [AI Infra 综合面经题库 (3)](https://caomaolufei.github.io/AIInfraGuide/interview/ai-infra-综合面经题库-3)
6. [AI Infra 综合面经题库 (4)](https://caomaolufei.github.io/AIInfraGuide/interview/ai-infra-综合面经题库-4)
7. [AI Infra 综合面经题库 (5)](https://caomaolufei.github.io/AIInfraGuide/interview/ai-infra-综合面经题库-5)
8. [AI Infra 综合面经题库 (6)](https://caomaolufei.github.io/AIInfraGuide/interview/ai-infra-综合面经题库-6)
9. [AI Infra 综合面经题库 (7)](https://caomaolufei.github.io/AIInfraGuide/interview/ai-infra-综合面经题库-7)
10. [AI Infra 面经 (1)](https://caomaolufei.github.io/AIInfraGuide/interview/ai-infra-面经-1)

### 综合面经正文主题（已核对）

| 页面 | 明确覆盖的主题 | 主要阶段 |
|---|---|---|
| AI Infra 一面 | Roofline、扩卡瓶颈、GEMM、profiling、FlashAttention、C++ coredump、GQA Attention | 阶段 0/1/2/3 |
| AI Infra 校招 (1) | CUDA 层级与内存、Stream、矩阵乘、Softmax、布局转换、数组题；页面明确面向异构计算、AI 框架、HPC、部署、算子岗位 | 阶段 0/1 |
| 综合题库 (1) | Hopper TMA、FA2/FlashDecoding、MLA、PD、DiT/dLLM、蒸馏、torchrun、LoRA、LRU/树/内存池 | 四阶段综合 |
| 综合题库 (2) | FlashAttention、CPU cache、transpose、Weight-only/Marlin、Megatron SP、ZeRO、NVSHMEM/NVLink、MHA/FA V1 | 阶段 0/1/2/3 |
| 综合题库 (3) | global/shared memory、训练耗时估算、Prefill/Decode、overlap、Megatron/NCCL/NVSHMEM、PD、Muon、DeepSeek、长序列、Hopper | 阶段 1/2/3 |
| 综合题库 (4) | 项目深挖、kernel fusion、CuTe/CUDA、Warp Specialization、千卡 NCCL timeout、RL MoE、推理上线、Agent 生成 kernel | 阶段 1/2/3 + 项目表达 |
| 综合题库 (5) | GIL/IPC、AllReduce 成本、view/contiguous、TP 行列切分、Graph Fusion | 阶段 0/1/2 |
| 综合题库 (6) | CUDA Graph、launch、block/grid、stream、Bank Conflict、fence、调试、UM/zero-copy、Volta、PTX/SASS、CUDA/C++ coding | 重点阶段 1 |
| 综合题库 (7) | 训练/推理加速、分布式框架、DeepSpeed、资源与时间估算、慢训练排查、通信、梯度累积、量化、loss 抖动 | 阶段 2/3 |
| AI Infra 面经 (1) | C++、HPC、GPU/Cache/访存、OpenCL、fusion/TVM、深度学习/量化、Conv、计算图、Pooling/NMS | 阶段 0/1/3 |

综合页面的上述主题和第一版具体题卡均由固定 commit 的正文核对；去重结果见 [core-question-map.md](core-question-map.md)。后续只需在上游对应 blob SHA 变化时重拆这些页面。

## 官方仓库结构与数据口径

- 固定版本、主要源文件、统计复核和内容指纹：[AIInfraGuide 上游来源快照](../resources/ai-infra-guide-source.md)
- 面经原文：https://github.com/caomaolufei/AIInfraGuide/tree/main/docs/interview
- 面试 collection schema：https://github.com/caomaolufei/AIInfraGuide/blob/main/src/content/config.ts
- 首页源码：https://github.com/caomaolufei/AIInfraGuide/blob/main/src/pages/interview/index.astro
- 动态文章路由：https://github.com/caomaolufei/AIInfraGuide/blob/main/src/pages/interview/%5B...slug%5D.astro
- 分组逻辑：https://github.com/caomaolufei/AIInfraGuide/blob/main/src/utils/companyGrouping.ts

固定 commit 中有 181 个 `docs/interview/*.md` 文件；该数量与核对时部署页面统计一致。

### 元数据分布

根据公开 Markdown frontmatter：

- 面试类型：实习 76、校招 38、社招 1、未知 66；
- 轮次字段：一面 84、二面 24、三面 1、一二面 4、一二三面 4、未标注 64。

“未知”或“未标注”只表示元数据没有规范填写，不能推断正文中一定没有岗位或轮次信息。页面中统一或集中出现的发布日期也不能自动当作真实面试发生日期。

### 正文反映的横向能力

公开正文不只有四阶段技术题，还广泛包含：

- 项目经历与项目深挖；
- C++、Python、操作系统、网络、算法与数据结构；
- CUDA/算子手写和优化解释；
- 分布式训练、推理部署与性能排障；
- 系统设计、场景题、开放题和工程实践；
- 综合素质、职业动机和 HR 问题。

仓库标题文本中“项目经历”“基础知识”“编程题”等标题出现很多，但同一篇可能有多轮或重复章节，因此标题出现次数不能当作独立题数、行业频率或评分权重。四阶段技术路线之外，还必须保留项目表达、代码能力、系统设计/排障与沟通动机这些横向验收。

## 当前可确认与不可确认的边界

固定源码版本可以确认：

- 梯队、公司/机构、篇数、frontmatter 元数据和叶子页面 slug；
- 综合 10 篇中的 185 条编号原题，以及 [第一版语义去重映射](core-question-map.md)；
- 部分条目声明的实习、校招、社招及面试轮次；
- 页面生成时对 `draft` 的过滤与梯队/公司的分组顺序。

部署网站抽样可以确认：

- 学习路线、面试首页和代表性叶子页面的公开 URL 可访问；
- 核对时页面显示 181 篇面经、65 家公司、7 个梯队；
- 标题、slug、导航和 Markdown 渲染与固定源码样本一致。

当前仍不能确认：

- 尚未逐篇读取的公司叶子面经中的完整题目映射；
- 某题的真实行业出现频率或公司长期招聘标准；
- 来源没有明确写出的完整 JD、真实面试日期和上下文；
- 面经叙述中的技术结论是否准确。

因此，初始化索引已完成；后续不再横向扫完整站，而是在进入每个主题前，按关键词读取对应公司叶子正文并增量合并到已有题簇。

## 逐篇核对字段

每个叶子页面按以下字段登记：

- 页面标题与准确 URL；
- 梯队、公司/机构、招聘类型和轮次；
- 时间与岗位（仅来源明确时）；
- 原始题目或忠实转述；
- 映射阶段与主题；
- 是否为概念题、计算题、系统设计题、代码题、项目追问或行为面试；
- 技术事实核查状态；
- 与其他页面的重复题；
- 已知上下文缺失与局限。

## 使用边界

- 面经是个人回忆样本，不代表公司统一题库或长期招聘标准。
- 同题多来源只建立一个主条目，同时记录出现来源。
- 未读正文的页面不能贡献具体题目或“高频”结论。
- 题目原文可以保留，技术答案必须独立核查。

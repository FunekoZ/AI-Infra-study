# 综合面经核心题卡映射（第一版）

> 来源范围：AIInfraGuide `main@a3b63eeb81d6d36a3c42c8cfc5a1bdd96e36bab1` 中 `tier: 综合` 的 10 个 Markdown，共 185 条编号原题。
>
> 本文件只做语义去重、阶段映射和学习优先级整理，不改写成逐字答案。固定版本、源文件 blob SHA 和重新同步规则见 [AIInfraGuide 上游来源快照](../resources/ai-infra-guide-source.md)。

## 去重与引用规则

- **去重单位**：考察同一机制、数据流或实现目标的题目归为一个题簇；版本差异、边界条件和递进实现保留为同簇中的来源变体，不因措辞相似而丢失。
- **主阶段**：该题应被正式学习和验收的阶段；桥接阶段只说明它还会连接到哪里，不提前打乱主线。
- **级别**：`core` / `important` / `supplementary` 只表示本仓库学习价值，不宣称行业频率。
- **定位格式**：`源文件 §小节 #题号`；公开页面 URL 由文件 slug 对应生成。
- **事实边界**：面经证明“题目出现过”，技术答案仍需由论文、官方资料或独立推导核查。

## 当前 Transformer 主题的验收题

10 篇综合材料中没有原题精确要求“从 `X ∈ R^(B×S×D)` 推导完整 Q/K/V、score、output shape 与 `O(S²)`”。这些内容属于本地路线的**知识验收**，不能伪装成综合面经原题。

当前主题采用下面的真实题目链：

| 顺序 | ID | 题目与用途 | 来源 | 状态 |
|---:|---|---|---|---|
| 1 | `CQ-0-ATTN-IMPL` | 实现 Multi-Head Attention；用于验收投影、拆头、score、mask、softmax、value aggregation、合头与输出 shape | `AI-Infra-综合面经题库-2.md` §PyTorch 编程题 #1 | `unseen` |
| 2 | `CQ-0-ATTN-IMPL` 递进 | 手写包含 GQA 的 Attention；用于追问 K/V 头共享、head 映射、广播和 KV shape | `AI-Infra-一面.md` #7 | `unseen` |
| 3 | `CQ-1-FLASH-BASE` 后续桥接 | 介绍并实现 FlashAttention V1；只有标准 Attention 已稳定后才进入阶段 1 的 I/O 优化 | `AI-Infra-一面.md` #5；`AI-Infra-综合面经题库-2.md` §基础知识 #1、§PyTorch 编程题 #2 | `unseen` |

为覆盖当前知识验收，还从公司叶子面经选取四条真实补充题：

| ID | 题目 | 来源 | 作用 |
|---|---|---|---|
| `CQ-0-TRANSFORMER-FLOW` | 阐述 Decoder-only 结构、QKV 生成过程和位置编码嵌入时机 | `飞腾-AI-Infra-实习-一面.md` §推理与算子优化 #4 | Decoder-only 全链路主问 |
| `CQ-0-ATTN-SHAPE` | 推导注意力矩阵维度，并说明多头、多 batch 如何并行 | `腾讯-AI-Infra.md` §推理优化 #6–8 | shape 与并行布局验收 |
| `CQ-0-ATTN-MASK` | 手写 MHA，并说明 Masked 矩阵在哪一步引入 | `联想-AI-Infra-实习-一面.md` §编程题 #8 | causal mask 与代码映射 |
| `CQ-0-ATTN-SCALE` | 为什么点积结果除以 `sqrt(d)`，不缩放会怎样 | `科大讯飞-AI-Infra-校招.md` §基础知识 #2 | scale 机制追问 |

**当前完成标准**：能在约 2 分钟口述 Decoder-only Block 与 Attention 数据流；从 `X ∈ R^(B×S×D)` 推导 MHA 各张量 shape；解释 scale、causal mask 和 softmax 维度；再说明改成 GQA 时哪些 shape 和共享关系变化。当前均为 `unseen`，尚未因建立题卡而标记掌握。

## 第一版全量题簇

### 阶段 0：前置知识

| ID | 去重题簇 | 桥接 | 级别 | 综合来源 |
|---|---|---|---|---|
| `CQ-0-ATTN-IMPL` | 手写标准 MHA，并递进到 GQA Attention | 1、2、3 | core | `AI-Infra-综合面经题库-2.md` §PyTorch 编程题 #1；`AI-Infra-一面.md` #7 |
| `CQ-0-TENSOR-STORAGE` | `repeat` vs `expand`；`view` vs `contiguous`，理解 head reshape、合并和广播的存储语义 | 1 | core | `AI-Infra-综合面经题库-1.md` §基础知识 #9；`AI-Infra-综合面经题库-5.md` §基础知识 #4 |
| `CQ-0-CPP-VALUE-LIFETIME` | 指针/引用、右值引用、move/forward、拷贝构造、new/malloc 与对象生命周期 | 1 | important | `AI-Infra-面经-1.md` §C++ #1、#4–7、#17 |
| `CQ-0-CPP-OBJECT-TYPE` | static、虚函数、多态、对象布局、模板、cast、CRTP | 1 | important | `AI-Infra-面经-1.md` §C++ #2、#9–10；`AI-Infra-综合面经题库-6.md` §C++ 基础 #14–15、#17–18 |
| `CQ-0-CPP-RAII-STL` | 智能指针、vector、lambda、线程安全单例与 RAII | 1 | important | `AI-Infra-面经-1.md` §C++ #3、#11–12、#16；`AI-Infra-综合面经题库-6.md` §C++ 基础 #16、#19–20、§C++ 编程 #5 |
| `CQ-0-CPP-BUILD-ABI` | 编译流程、动静态库、C/C++ 互调、大小端 | 1 | supplementary | `AI-Infra-面经-1.md` §C++ #18–19、#21 |
| `CQ-0-CONCURRENCY-IPC` | 内存模型、锁/条件变量/死锁、进程线程、GIL 与 IPC | 横向排障 | important | `AI-Infra-面经-1.md` §C++ #8、#13–15、#20；`AI-Infra-综合面经题库-5.md` §基础知识 #2–3 |
| `CQ-0-TORCHRUN-OPS` | torchrun 参数与 Linux 批量进程管理 | 2 | supplementary | `AI-Infra-综合面经题库-1.md` §基础知识 #10 |
| `CQ-0-ML-NORM-REGULARIZATION` | BatchNorm、Dropout、Softmax 基础 | 1、3 | supplementary | `AI-Infra-面经-1.md` §深度学习 #1、#8、#11 |
| `CQ-0-CV-MODEL-BASICS` | 轻量卷积、检测模型、池化、反卷积/空洞卷积、GIoU/NMS | 1、3 | supplementary | `AI-Infra-面经-1.md` §深度学习 #2–5、#9–10、#12 |

### 阶段 1：CUDA 与算子优化

| ID | 去重题簇 | 桥接 | 级别 | 综合来源 |
|---|---|---|---|---|
| `CQ-1-GPU-EXECUTION` | Grid/Block/Thread、SM/SP、launch 参数与 GPU 执行架构 | 0 | core | `AI-Infra-校招-1.md` §基础知识 #1、#3–4；`AI-Infra-综合面经题库-6.md` §CUDA 基础 #2、#9–12；`AI-Infra-面经-1.md` §高性能计算 #1 |
| `CQ-1-MEMORY-CACHE` | CUDA 内存层次、CPU/GPU cache、局部性、Unified/Zero-Copy | 0、3 | core | `AI-Infra-校招-1.md` §基础知识 #2、#6；`AI-Infra-综合面经题库-2.md` §基础知识 #2；`题库-3.md` §基础知识 #1；`题库-6.md` §CUDA 基础 #7；`AI-Infra-面经-1.md` §高性能计算 #2–4 |
| `CQ-1-STREAM-LAUNCH-SYNC` | Stream、同步/异步、CUDA Graph、default stream、threadfence | 0 | core | `AI-Infra-校招-1.md` §基础知识 #5；`AI-Infra-综合面经题库-6.md` §CUDA 基础 #1、#3、#5 |
| `CQ-1-SMEM-BANK-TRANSPOSE` | Shared Memory、同步、Bank Conflict 与矩阵转置 | 0 | core | `AI-Infra-校招-1.md` §基础知识 #7；`题库-2.md` §基础知识 #3；`题库-6.md` §CUDA 基础 #4、§CUDA 编程 #3；`AI-Infra-面经-1.md` §高性能计算 #13 |
| `CQ-1-ROOFLINE-PROFILING` | Roofline、计算/访存瓶颈判断与 kernel 优化维度 | 横向排障 | core | `AI-Infra-一面.md` #1；`AI-Infra-校招-1.md` §基础知识 #8；`AI-Infra-面经-1.md` §高性能计算 #5–6、#10 |
| `CQ-1-GEMM-SHAPE-TILING` | GEMM 是否计算受限、shape 特化、tiling 与矩阵乘 kernel | 0 | core | `AI-Infra-一面.md` #3；`AI-Infra-校招-1.md` §编程题 #1；`题库-1.md` §CUDA 编程 #2；`AI-Infra-面经-1.md` §编程题 #5 |
| `CQ-1-REDUCTION-SOFTMAX` | Reduction 与高效 Softmax kernel | 0、3 | core | `AI-Infra-校招-1.md` §编程题 #2；`AI-Infra-综合面经题库-6.md` §CUDA 编程 #1–2 |
| `CQ-1-TENSOR-INDEXING` | 布局转换、broadcast elementwise、直方图、Embedding pooling、GPU 排序 | 0 | important | `AI-Infra-校招-1.md` §编程题 #3–4；`题库-1.md` §CUDA 编程 #1、#3；`题库-6.md` §CUDA 基础 #8 |
| `CQ-1-FUSION` | kernel/graph fusion 的方式、收益与退化边界 | 3 | important | `AI-Infra-综合面经题库-4.md` §基础知识 #2–4；`题库-5.md` §编程题 #8；`AI-Infra-面经-1.md` §高性能计算 #11 |
| `CQ-1-HARDWARE-COMPILER` | Hopper TMA、Warp Specialization、PTX/SASS、Agent 生成 kernel、TVM | 2、3 | supplementary | `题库-1.md` §基础知识 #1；`题库-3.md` §基础知识 #14；`题库-4.md` §基础知识 #5、#9；`题库-6.md` §CUDA 基础 #12；`AI-Infra-面经-1.md` §高性能计算 #14 |
| `CQ-1-OPENCL` | OpenCL 流程、分支掩码、kernel 参数与基础实现 | 0 | supplementary | `AI-Infra-面经-1.md` §高性能计算 #7–9、§编程题 #5 |
| `CQ-1-VISION-OP-CODING` | Pooling、IoU、NMS、Conv2D、插值、LayerNorm 等算子实现 | 横向代码 | supplementary | `题库-6.md` §CUDA 编程 #4–5、§C++ 编程 #1–4；`AI-Infra-面经-1.md` §高性能计算 #12、§深度学习 #12、§编程题 #1–4 |
| `CQ-1-FLASH-BASE` | FlashAttention 核心原理及 V1 实现 | 0、3 | core | `AI-Infra-一面.md` #5；`题库-2.md` §基础知识 #1、§PyTorch 编程 #2 |
| `CQ-1-FLASH-ADV` | FA2 的 Q 外循环选择与 Flash Decoding combine kernel | 3 | important | `AI-Infra-综合面经题库-1.md` §基础知识 #2 |

### 阶段 2：分布式训练

| ID | 去重题簇 | 桥接 | 级别 | 综合来源 |
|---|---|---|---|---|
| `CQ-2-COLLECTIVE-COST` | AllReduce 通信量、NCCL 原语、NVSHMEM/NVLink 与拓扑 | 0、1 | core | `题库-5.md` §基础知识 #3；`题库-3.md` §基础知识 #11–12；`题库-2.md` §基础知识 #9 |
| `CQ-2-SCALE-BOTTLENECK` | 卡数扩展与多机多卡通信瓶颈、证据及缓解 | 1、3 | core | `AI-Infra-一面.md` #2；`题库-7.md` §基础知识 #6 |
| `CQ-2-ZERO-DEEPSPEED` | ZeRO Stage 1/2、DeepSpeed 与多机训练框架 | 0 | core | `题库-2.md` §基础知识 #8；`题库-7.md` §基础知识 #2–3 |
| `CQ-2-MEGATRON-PARALLELISM` | Megatron SP/TP、通信优化与长序列并行 | 0、3 | core | `题库-2.md` §基础知识 #7；`题库-3.md` §基础知识 #5、#13；`题库-5.md` §基础知识 #5 |
| `CQ-2-TRAIN-THROUGHPUT` | token 训练耗时估算、资源效率与梯度累积 | 3 | important | `题库-3.md` §基础知识 #2；`题库-7.md` §基础知识 #4、#7 |
| `CQ-2-OPTIMIZER-STABILITY` | Muon/AdamW 使用边界与 loss 震荡排查 | 0 | important | `题库-3.md` §基础知识 #7；`题库-7.md` §基础知识 #10 |
| `CQ-2-FINETUNE-DISTILL` | 知识蒸馏与 LoRA Adapter | 0、3 | important | `题库-1.md` §基础知识 #6、§PyTorch 编程 #1；`AI-Infra-面经-1.md` §深度学习 #6 |
| `CQ-2-MOE-SPECIALS` | RL MoE、DeepSeek-V3 与稀疏注意力变体 | 3 | supplementary | `题库-4.md` §基础知识 #7；`题库-3.md` §基础知识 #9–10 |

### 阶段 3：推理与部署

| ID | 去重题簇 | 桥接 | 级别 | 综合来源 |
|---|---|---|---|---|
| `CQ-3-PREFILL-DECODE-PD` | Prefill/Decode 优化、overlap、PD 分离、KV 传输与上线前调优 | 2 | core | `题库-3.md` §基础知识 #3–4、#6、#8；`题库-1.md` §基础知识 #4；`题库-4.md` §基础知识 #8 |
| `CQ-3-ATTN-DECODE` | MLA decode 计算访存比与 dLLM/AR 推理差异 | 2 | important | `题库-1.md` §基础知识 #3、#8 |
| `CQ-3-QUANTIZATION` | Weight-Only、Marlin、量化访存与推理收益 | 1、2 | core | `题库-2.md` §基础知识 #6；`题库-7.md` §基础知识 #8；`AI-Infra-面经-1.md` §深度学习 #7 |
| `CQ-3-DIFFUSION-FLOW` | DiT/dLLM、Diffusion timestep、Flow Matching 与采样伪代码 | 1 | supplementary | `题库-1.md` §基础知识 #5、#7；`题库-2.md` §基础知识 #4–5、§PyTorch 编程 #3 |

### 横向能力轴

| ID | 去重题簇 | 桥接 | 级别 | 综合来源 |
|---|---|---|---|---|
| `CQ-HX-PROJECT-DEEP-DIVE` | 项目背景、本人贡献、瓶颈、方案选择与量化结果 | 1、2、3 | core | `题库-4.md` §项目经历 #1；`题库-5.md` §项目经历 #1；`题库-7.md` §基础知识 #9 |
| `CQ-HX-DIAGNOSTIC` | 性能瓶颈、C++ 越界/coredump、CUDA 调试、NCCL timeout、慢训练排查 | 0、1、2、3 | core | `AI-Infra-一面.md` #4、#6；`题库-4.md` §基础知识 #6；`题库-6.md` §CUDA 基础 #6；`题库-7.md` §基础知识 #5 |
| `CQ-HX-ACCELERATION-SURVEY` | 给定模型、硬件与负载后比较训练/推理加速方案 | 2、3 | important | `题库-7.md` §基础知识 #1 |
| `CQ-HX-CODE-CACHE` | 内存池与 LRU | 0、1 | supplementary | `题库-1.md` §算法 #1、#3 |
| `CQ-HX-CODE-NUMBER-ARRAY` | float 比较、Hamming Weight、整数幂、原地奇偶分区 | 0、1 | supplementary | `题库-1.md` §算法 #2、#6；`题库-5.md` §编程题 #7；`AI-Infra-校招-1.md` §编程题 #5 |
| `CQ-HX-CODE-SORT-STRING` | 快排、有序数组中位数、排列、Top-K、字符串位置 | 0、1 | supplementary | `题库-2.md` §算法 #1–3、#7–8 |
| `CQ-HX-CODE-GRAPH-TREE` | 岛屿、层序、最大路径和与 Path Sum | 0 | supplementary | `题库-1.md` §算法 #4–5；`题库-2.md` §算法 #4–5 |
| `CQ-HX-CODE-DP-INTERVAL` | 区间覆盖与双指键盘动态规划 | 0、1 | supplementary | `题库-1.md` §算法 #7；`题库-2.md` §算法 #6、#9 |

## 叶子面经的后续递进候选

以下题目已由固定源码确认，但不属于上述 10 篇综合来源；它们只在学到相应阶段时增量加入，不提前展开：

- `百度-AI-Infra-二面-2.md` §Transformer 与模型结构 #1、#3–4：token 到 logits、MHA/MQA/GQA 的 KV Cache 与效率、为何只缓存 K/V；
- `快手-AI-Infra-实习-一面-3.md` §基础知识 #2：MHA/MQA/GQA、KV 广播、MLA 与 GQA 的对应关系；
- 其余公司叶子面经继续按当前主题查询，不一次性复制为大型题库。

## 维护规则

1. 上游 commit 不变时，不重复抓取网页或重拆全部题目；
2. 更新上游后先比较 [来源快照](../resources/ai-infra-guide-source.md) 中的 10 个 blob SHA；
3. 只对变化文件重新提取和语义去重；
4. 新来源若与已有题簇同义，只追加出现记录；确有不同机制或边界才创建新 ID；
5. 每个主题开始前从本文件和对应阶段目录选择少量代表题，完成后再更新 `unseen / learning / can-outline / mastered / review`；
6. 本文件建立题目需求，不代表任何题已经学会。

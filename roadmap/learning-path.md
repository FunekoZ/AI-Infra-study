# AI Infra 系统学习路线

> 外部基准：[AIInfraGuide 官方仓库](https://github.com/caomaolufei/AIInfraGuide)中的路线与面试源码为主要读取入口，[学习路线公开页](https://caomaolufei.github.io/AIInfraGuide/guides/ai-infra%E5%AD%A6%E4%B9%A0%E8%B7%AF%E7%BA%BF/)与[面试宝典公开页](https://caomaolufei.github.io/AIInfraGuide/interview/)用于部署一致性核对（当前固定上游版本：`main@a3b63eeb81d6d36a3c42c8cfc5a1bdd96e36bab1`；核对日期：2026-09-22；路线 frontmatter `pubDate`：2026-03-26）。
>
> 本文件保留网站的四阶段范围与先后关系，并将代码和实验要求转换为知识理解、推导及教学代码阅读能力。项目可以创建带充分注释的学习代码，但默认不要求实际运行。

## 双轴路线：知识依赖 × 面试需求

本路线同时受两类内容约束：

- **知识依赖轴**：以下四个阶段决定概念先后关系，避免靠背题形成碎片知识；
- **面试需求轴**：[面试宝典](https://caomaolufei.github.io/AIInfraGuide/interview/)收录的公司面经与综合题库决定每个主题应掌握到什么深度。首页当前显示 181 篇面经、65 家公司、7 个梯队；该数字仅表示网站收录范围；
- **横向能力轴**：项目深挖、C++/Python/算法、系统设计与排障、工程表达和职业动机贯穿各阶段，不因无法唯一归入某阶段而忽略。

面试材料不会被放在路线末尾作为一次性冲刺，而是嵌入每个主题：学习概念前用题目识别真实需求，学习后用代表题和递进追问验收。面经中的技术说法需再用论文、官方资料、可靠讲解或独立推导核查。

## 横向能力验收

以下能力从阶段 0 开始建立，并在后续每个主题中反复使用：

- **项目深挖**：能说明目标、个人贡献、原始瓶颈、方案选择、指标、失败尝试、trade-off 和可改进点；
- **通用代码能力**：能阅读并解释必要的 C++/Python、数据结构和系统接口，不要求无边界刷题；
- **性能排障**：按“症状 → 指标 → 假设 → 验证 → 改动 → 回归”组织回答；
- **系统设计**：先明确模型、硬件、负载、规模和 SLO，再做方案选择；
- **沟通与动机**：能说明为何选择 AI Infra、为何选择某方向，以及如何处理不确定信息。

横向能力不替代四阶段主线，也不能因为某份面经出现行为题就让当前技术主线无限分叉。按主题和目标岗位逐步验收。

## 总体方法

AI Infra 的核心是在约束下协调以下维度：

- **计算**：算力利用率、Tensor Core、Kernel 效率；
- **通信**：集合通信量、拓扑、通信与计算重叠；
- **显存**：权重、梯度、优化器状态、activation、KV Cache；
- **精度**：FP32、BF16、FP16、FP8、INT8、INT4 的数值范围与误差；
- **服务质量**：TTFT、TPOT、吞吐、P50/P95/P99 和 Goodput；
- **复杂度**：实现、调试、部署、调度和运维成本。

学习任何优化时回答五个问题：

1. 它解决什么问题？
2. 原始瓶颈在哪里？
3. 数据如何流动，方案如何工作？
4. 它牺牲了什么，又改善了什么？
5. 若在真实系统中验证，应观察哪些指标并控制哪些变量？

## 知识与代码阅读验收原则

网站中的实践任务按其能力目标转换为知识理解与代码阅读验收。一个主题通常需要做到：

- 能准确复述核心概念及其关系；
- 能口述或画出关键数据流；
- 能推导主要公式、shape、复杂度、显存或通信量；
- 能比较相关方案的 trade-off 与适用条件；
- 能阅读并解释必要的带注释教学代码或关键源码片段；
- 能分析给定案例中的主要瓶颈；
- 能说明真实实验应怎样验证，但默认不要求实际执行；
- 能通过针对常见误区的检查问题；
- 能对该主题的代表性面试题给出结构化回答，并承接机制、计算或边界追问。

面试题本身不是独立知识点。题目应映射到对应阶段，并在 `interview/` 中记录来源、考察意图、回答骨架、追问和关联资料。

## 阶段 0：前置知识

### 目标

建立理解 CUDA、分布式训练和推理系统所需的最小知识基础，不追求在所有前置方向上成为专家。

### 主题

- **Python**：对象模型、装饰器、生成器、多进程、多线程和性能分析的基本语义；以能读懂后续材料为准。
- **C/C++**：指针、内存管理、编译与链接；以能理解 CUDA Host 代码和系统项目为准。
- **Linux**：进程、环境变量、文件系统、Shell、服务器和开发环境的基本概念。
- **数学**：矩阵乘法、转置、分块矩阵、概率分布、期望/方差、Softmax、交叉熵、链式法则和反向传播。
- **Transformer**：Q/K/V、Self-Attention、FFN、位置编码、RoPE、Pre/Post-Norm 和 Decoder Block。
- **PyTorch 抽象**：Tensor、autograd、`Module`、`Parameter`、训练循环、checkpoint 和 Profiler 分别承担什么职责。
- **GPU 与通信**：NVLink/NVSwitch、PCIe、InfiniBand/RoCE、NCCL、AllReduce、AllGather 和 ReduceScatter。

### 理论验收

- [ ] 口述 Decoder-only Transformer Block 的数据流，标出 residual、normalization、Attention 和 FFN。
- [ ] 从 `X ∈ R^(B×S×D)` 推导多头 Q/K/V、attention score 和输出 shape。
- [ ] 解释 scale、causal mask、softmax 和 value aggregation 的作用。
- [ ] 推导标准 Self-Attention 对序列长度的时间与中间矩阵复杂度。
- [ ] 根据 `hidden_dim`、层数、FFN 维度和词表大小估算 Transformer 参数量。
- [ ] 解释 forward、loss、backward、optimizer update 和 checkpoint 的逻辑关系。
- [ ] 读懂 CUDA Host 侧的分配、拷贝、Kernel 启动与释放概念流程。
- [ ] 根据拓扑图判断 GPU、CPU 和 NIC 之间的主要数据路径。
- [ ] 画出或口述 AllReduce、AllGather、ReduceScatter 数据流，并推导 Ring AllReduce 通信量约为 `2(N-1)/N × 数据量`。

### 面试导向验收

具体题型必须与 AIInfraGuide 固定源码版本的 `interview/source-index.md` 和阶段题卡对应：

- 从输入 shape 出发，白板推导 Self-Attention、多头拆分和输出 shape；
- 解释为什么除以 `sqrt(d_k)`、causal mask 放在哪里、softmax 为什么沿指定维度；
- 估算 Transformer 参数量、Attention 计算量和中间激活规模；
- 解释 forward、backward、autograd、optimizer 与 checkpoint 的关系；
- 比较线程与进程、Python GIL 对何类任务有影响；
- 解释 GPU、CPU、显存、PCIe/NVLink 与集合通信的基本关系；
- 推导或解释 AllReduce、AllGather、ReduceScatter 的数据流和通信量。

验收不要求背统一措辞，而要求能先给清晰主回答，再应对至少一个“为什么”或 shape/复杂度追问。

### 推荐顺序

1. Transformer 整体数据流与 shape；
2. 参数量、计算量和 Attention 复杂度；
3. 反向传播与 PyTorch 训练抽象；
4. GPU 架构和存储层次初步直觉；
5. 集合通信与硬件拓扑。

## 阶段 1：CUDA 与算子优化

### 目标

理解 GPU 执行与存储层次，形成“先判断计算或访存瓶颈，再分析优化”的系统直觉。

### 主题

- SM、CUDA Core、Tensor Core；HBM、L2/L1、Shared Memory、Register。
- Grid、Block、Thread、Warp、Occupancy。
- Coalesced Access、Bank Conflict、Warp Shuffle。
- Reduce、GEMM、Softmax 和算子融合。
- FlashAttention V1/V2/V3、Flash-Decoding、FlashInfer、PagedAttention Kernel。
- Triton、`torch.compile`、Graph Break；了解 TVM/XLA。
- Nsight Systems 与 Nsight Compute 的分析视角。

### 代码阅读配套轨道：`learn-cuda`（非替代课程）

将 [gau-nernst/learn-cuda](https://github.com/gau-nernst/learn-cuda/tree/8c4d1b887a25727b320bc3ace19b63e2db6f8b44) 作为阶段 1 的高密度代码阅读资料，而不是新的独立阶段或官方事实来源。推荐顺序：

1. `01_vector_addition`：PyTorch C++/CUDA extension、输入检查、grid/block、kernel 边界和输出生命周期；
2. `03_sum`：树形归约、thread coarsening、warp shuffle 与向量化加载；
3. `02_matmul_simt`：层次化 tiling、Shared Memory、寄存器复用、coalescing 与 Triton 对照；
4. `04_softmax`：数值稳定、online softmax、split-N 与 atomic 代价；
5. `07_attention`：从基础 Attention kernel 到 FlashAttention 风格的分块、流水线和访存优化；
6. `10_p2p`：放到 GPU 拓扑/NCCL 前后作阶段 2 桥接；`11_gemv`、`12_megakernel` 放到推理阶段学习 decode/GQA/KV Cache 后再选读；
7. `02_matmul_sm80`、`sm100`、`sm120`、`05_fp6`、`08/09` 和 `02_matmul_cdna3` 作为硬件或低精度专项，不列为基础必修。

仓库无明确许可证，且代码和 benchmark 依赖特定 GPU、CUDA/PyTorch 版本；本项目只保存固定 commit、目录映射和自己的解释，不复制上游源代码或把 README 性能数字当作路线结论。

### 理论验收

- [ ] 解释 GPU 存储层次为何导致 Memory Wall，以及 latency、bandwidth 和 capacity 的关系。
- [ ] 给定数据量和有效带宽，估算经 NVLink 或 PCIe 传输的理论时间下界，并指出被忽略的开销。
- [ ] 比较 global atomic、Shared Memory tree reduction 和 Warp Shuffle Reduce 的数据流与瓶颈。
- [ ] 解释矩阵转置为何可能产生非合并访问和 Bank Conflict，以及 padding 为什么有效。
- [ ] 推导 tiled GEMM 如何用 Shared Memory 提高数据复用，并分析 tile 过大的代价。
- [ ] 推导 online softmax 的状态更新逻辑。
- [ ] 说明 FlashAttention 的分块、mask、online softmax 与 HBM I/O 降低机制。
- [ ] 区分 Nsight Systems 的全链路时间线视角与 Nsight Compute 的 Kernel 级视角。
- [ ] 给定症状，判断算子更可能是 Memory Bound、Compute Bound 还是受 launch/同步影响。

### 代码阅读验收

- [ ] 能从 `01_vector_addition` 解释 PyTorch extension 到 CUDA kernel 的 Host—Device 数据流，并指出 dtype、contiguous 和边界假设；
- [ ] 能比较 `03_sum` 中树形归约、Shared Memory 和 Warp Shuffle 的同步、访存及 occupancy 代价；
- [ ] 能从 `02_matmul_simt` 解释 block/warp/thread tiling、寄存器累加、Shared Memory 复用和 Bank Conflict；
- [ ] 能从 `04_softmax` 与 `07_attention` 连接 online softmax、mask、tile、流水线和 HBM I/O；
- [ ] 能用 `02_matmul_simt/matmul_triton.py` 对比 CUDA 的 thread/block 抽象与 Triton 的 program/mask/autotune 抽象；
- [ ] 能明确代码版本、GPU 架构、dtype、shape 和 benchmark 环境假设；未实际运行时不得声称代码或性能已经验证。

### 面试导向验收

具体题型必须与 AIInfraGuide 固定源码版本的 `interview/source-index.md` 和阶段题卡对应：

- 解释 warp、SM、occupancy、coalesced access 和 Bank Conflict，并判断给定访存模式；
- 手写或口述 Reduce、Transpose、GEMM、Softmax 的朴素方案及逐步优化；
- 分析一个 Kernel 是 Memory Bound 还是 Compute Bound，需要看哪些指标；
- 解释 Shared Memory tiling、Warp Shuffle 和算子融合为什么可能加速，以及何时反而退化；
- 推导 Online Softmax，并解释 FlashAttention 为什么是 exact attention、如何减少 HBM I/O；
- 比较 CUDA、Triton 和编译器自动生成算子的适用场景；
- 根据时间线或 profiler 症状区分 CPU、launch、同步、通信和 Kernel 内部瓶颈。

### Trade-off 检查点

- Tiling 和 fusion 减少 HBM 流量，但增加寄存器、Shared Memory 压力与实现复杂度。
- 更大 tile 可能提高复用，也可能降低 occupancy。
- 编译器自动优化降低开发成本，但动态 shape、Graph Break 和生成代码质量会限制收益。

## 阶段 2：分布式训练

### 目标

能建立显存和通信账本，并依据模型结构、集群拓扑与规模解释并行策略选择。

### 主题

- MHA → MQA → GQA → MLA；MoE 与 Expert Parallelism。
- SGD、Momentum、Adam/AdamW、LAMB、LARS 的状态开销。
- DP、DDP、FSDP、ZeRO-1/2/3。
- TP、PP、SP 与 3D 并行。
- BF16、FP16、FP8；梯度累积与 Activation Checkpointing。
- Megatron-LM、DeepSpeed、PyTorch FSDP。

### 理论验收

- [ ] 为一个 7B 模型逐项计算参数、梯度、master weights、优化器状态和 activation 的显存，明确 dtype 与口径。
- [ ] 解释 DDP 的梯度同步时机、bucket 和通信计算重叠思想。
- [ ] 比较 ZeRO-1/2/3 的切分对象、显存收益和通信代价。
- [ ] 解释 FSDP 前向与反向中的参数 AllGather 和梯度 ReduceScatter。
- [ ] 为 8 节点 × 8 GPU 设计 TP/PP/DP 组合，并说明为什么某些通信适合留在机内。
- [ ] 用指数位和尾数位解释 BF16、FP16 与 FP32 的范围和精度差异。
- [ ] 比较 activation checkpointing 的显存收益与重计算代价。
- [ ] 解释 MoE 的稀疏计算收益、路由、负载均衡和 All-to-All 通信问题。

### 面试导向验收

具体题型必须与 AIInfraGuide 固定源码版本的 `interview/source-index.md` 和阶段题卡对应：

- 逐项计算训练显存，并解释不同文章为什么可能得到不同 bytes/parameter；
- 比较 DP、DDP、FSDP、ZeRO 各阶段的切分对象、collective 和通信时机；
- 给定模型与集群拓扑设计 TP/PP/DP/SP 组合，说明机内与跨机布局；
- 分析 PP bubble、micro-batch、梯度累积和通信计算重叠；
- 比较 FP16、BF16、FP8 的范围、精度、稳定性和硬件要求；
- 解释 activation checkpointing 的显存—计算交换；
- 解释 MoE routing、负载均衡、Expert Parallelism 和 All-to-All 瓶颈；
- 面对 OOM、扩展效率差或通信占比高的场景给出定位顺序，而不是直接罗列技术名词。

### 口径注意

参考页面对 AdamW 混合精度训练的 7B 显存示例存在约 84 GB 与约 56 GB 两种数字。学习时不得直接背结论，应明确是否包含：

- FP16/BF16 参数；
- FP16/BF16 梯度；
- FP32 master weights；
- FP32 一阶、二阶动量；
- activation、临时 buffer 和 allocator 开销。

## 阶段 3：推理与部署

### 目标

能从工作负载与 SLO 出发判断推理瓶颈，理解引擎和优化方法的适用范围，并读懂 Benchmark 结论。

### 主题

#### 推理基础

- Prefill 通常偏 Compute Bound；Decode 通常更受 KV Cache 搬运和显存带宽限制。
- KV Cache 的 shape、生命周期、碎片和容量估算。
- TTFT、TPOT、吞吐、P50/P95/P99 和 Goodput。

#### 推理引擎

- PagedAttention、Continuous Batching、Prefix Cache/RadixAttention、Chunked Prefill。
- vLLM、SGLang、TensorRT-LLM 的定位与取舍。

#### 量化

- W8A8/SmoothQuant、GPTQ/AWQ INT4 weight-only、KV Cache 量化和 FP8。
- 权重与带宽收益同量化误差、解包/反量化和 Kernel 利用率之间的关系。

#### Speculative Decoding

- Draft/Target、rejection sampling、Medusa、EAGLE-2 和 block verification。
- 接受率、batch size、采样温度与验证开销。

#### Prefill/Decode 解耦

- 混合 batching 的干扰、KV 迁移、GPU 池配比、网络和调度成本。
- DistServe、Splitwise，以及以 SLO 为约束的 Goodput。

### 理论验收

- [ ] 拆解 `tokenize → prefill → decode → sampling → detokenize` 并分析各阶段的瓶颈候选。
- [ ] 从 `layers × 2(K,V) × batch × kv_heads × sequence × head_dim × bytes` 推导 KV Cache 容量。
- [ ] 解释为什么 Prefill 和 Decode 的 arithmetic intensity 与并行特征不同。
- [ ] 画出或口述 PagedAttention 的逻辑块、物理块、页表、分配与回收流程。
- [ ] 解释 Continuous Batching、Prefix Cache 和 Chunked Prefill 分别解决什么问题。
- [ ] 比较 W8A8、INT4 weight-only、KV Cache 量化和 FP8 的目标、收益与风险。
- [ ] 推导 Speculative Decoding 保持目标分布的核心逻辑，并说明何时收益会变负。
- [ ] 分析 Prefill/Decode 混部的干扰，以及解耦带来的 KV 迁移和资源空转风险。
- [ ] 能读懂一份推理报告中的 TTFT、TPOT、P50/P95、吞吐、显存和 GPU 利用率，并识别不公平比较。

### 面试导向验收

具体题型必须与 AIInfraGuide 固定源码版本的 `interview/source-index.md` 和阶段题卡对应：

- 比较 Prefill 与 Decode 的计算特征、并行性和主要瓶颈；
- 给定模型、batch、序列长度与 dtype 推导 KV Cache 容量；
- 解释 PagedAttention、Continuous Batching、Prefix Cache 和 Chunked Prefill 分别解决什么问题；
- 比较 vLLM、SGLang、TensorRT-LLM 时先明确工作负载和 SLO；
- 比较 W8A8、INT4 weight-only、KV Cache 量化和 FP8，并解释低 bit 为什么不一定更快；
- 解释 Speculative Decoding 的正确性、接受率和负收益条件；
- 分析 Prefill/Decode 混部干扰、解耦收益、KV 迁移和资源空转；
- 设计或审查推理 Benchmark，解释 TTFT、TPOT、吞吐、P95/P99 与 Goodput；
- 给定 OOM、TTFT 高、TPOT 高或尾延迟高的症状，按证据给出定位和优化顺序。

### 优化分析顺序

1. 先判断是否受显存容量限制；
2. 再定位 TTFT；
3. 然后分析 TPOT 与吞吐；
4. 最后讨论 P95/P99 尾延迟及不同 SLO 下的 Goodput。

## 推荐资料节奏

### 基础阶段

- 《Attention Is All You Need》；
- The Illustrated Transformer；
- PyTorch 官方基础资料；
- NVIDIA NCCL 与 Deep Learning Performance Guide。

### CUDA 与分布式阶段

- CUDA C++ Programming Guide；
- [learn-cuda 代码阅读配套仓库](https://github.com/gau-nernst/learn-cuda/tree/8c4d1b887a25727b320bc3ace19b63e2db6f8b44)（按 `01 → 03 → 02_simt → 04 → 07` 阅读，固定版本与许可证边界见 `resources/learn-cuda-source.md`）；
- Triton 官方 Tutorials（先完成基础教程，再阅读仓库中的 Triton 对照实现）；
- Online Softmax、FlashAttention 系列；
- Megatron-LM 与 ZeRO；
- PyTorch DDP/FSDP、DeepSpeed 官方资料。

### 推理阶段

- vLLM/PagedAttention、SGLang、Orca；
- SmoothQuant、GPTQ、AWQ、KIVI；
- Speculative Sampling、Medusa、EAGLE-2；
- DistServe、Splitwise 与推理系统综述。

按当前主题需要选择资料，不预先批量下载或精读全部内容。

## 仓库落点

| 内容 | 位置 |
|---|---|
| 知识笔记与推导 | `notes/<stage>/` |
| 带注释教学代码 | `examples/<stage>/` |
| 面试宝典、面经索引与阶段题库 | `interview/` |
| 当前主线、分支和下一步 | `roadmap/progress.md` |
| 资料元数据 | `resources/resources.yaml` |
| 按需下载的论文 | `resources/papers/` |
| 按需保存的文档与文章 | `resources/docs/` |

## 完成定义

一个主题只有同时满足以下条件，才可标记为“已掌握”：

- 能用自己的话解释问题、原理和数据流；
- 关键公式、shape、复杂度、显存或通信量能够独立推导；
- 能解释该主题必要教学代码或关键源码片段中的数据流与核心语句；
- 能比较收益、代价、适用边界和失败场景；
- 能通过该主题的关键误区自检；
- 能对该主题的核心面试题给出结构化主回答，并处理至少一个递进追问；
- 如需长期保存，已有与来源对应的主题笔记、教学代码或面试题条目；
- 能说明真实系统中如何验证，但默认不要求亲自执行实验。

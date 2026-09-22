# learn-cuda 上游来源与融合方案

> 本文件记录对 `learn-cuda` 的版本核对、内容评估和本仓库的采用边界；不复制上游源代码。

## 上游版本

- **仓库**：https://github.com/gau-nernst/learn-cuda
- **分支**：`main`
- **固定 commit**：`8c4d1b887a25727b320bc3ace19b63e2db6f8b44`
- **commit 时间**：2026-09-07T07:59:32Z
- **上游最近 push（核对时 API 元数据）**：2026-09-22T13:34:52Z；与当前 HEAD commit 时间不同，不将 push 时间当作 commit 时间
- **核对日期**：2026-09-22
- **本地缓存**：`.cache/learn-cuda/`，已由仓库级 `.gitignore` 忽略
- **许可证状态**：当前固定 commit 未发现 `LICENSE`、`COPYING` 或 `NOTICE` 文件；在作者明确授权前，不复制其代码或 README 原文到本仓库

固定版本用于复现目录、README 说明和引用位置。重新采用新版本时，先比较 commit 和目录变化，再更新本文件与课程映射。

## 仓库事实

上游 README 将仓库定位为 **Learn CUDA with PyTorch**，提供 CUDA C++/PyTorch C++ extension、Triton 和部分 CuTe DSL 的对照代码与性能分析笔记。当前树约含 119 个跟踪文件，其中包括约 44 个 `.cu`、33 个 `.py` 和 14 个 `.md` 文件；它更像作者持续迭代的代码阅读/实验仓库，不是带统一章节、测试和课程验收的教材。

主要主题目录：

| 上游目录 | 内容 | 本项目定位 |
|---|---|---|
| `01_vector_addition/` | PyTorch C++/CUDA extension 的最小向量加法 | CUDA Host—extension—kernel 数据流入口 |
| `02_matmul_simt/` | CUDA Core 上的 block/thread/warp tiling、共享内存、寄存器与 Triton matmul | GEMM、访存和层次化 tiling |
| `02_matmul_sm80/` | `ldmatrix`、`mma`、inline PTX、CuTe DSL | Ampere Tensor Core 进阶，可选 |
| `02_matmul_sm100/` | TMA、tensor memory、`tcgen05`、warp specialization | Blackwell 专项，可选 |
| `02_matmul_sm120/` | SM120 相关矩阵乘 | 硬件版本专项，可选 |
| `02_matmul_cdna3/` | CDNA3 矩阵乘 | AMD 路径专项，可选 |
| `03_sum/` | reduction tree、thread coarsening、warp shuffle、vectorized load | Reduce 与并行归约 |
| `04_softmax/` | 稳定 Softmax、online Softmax、atomic 与 split-N | Softmax 数值稳定性和并行化 |
| `05_fp6/` | FP6 表示和 FP32/FP16/BF16 转换原理 | 低精度表示桥接，非当前前置 |
| `06_box_blur/` | 二维 block/thread 示例 | 访存与二维 kernel 辅助例子 |
| `07_attention/` | 从基础版本逐步改进的 Attention kernel | FlashAttention 阅读桥接 |
| `08_row_scaled_mm/` | row-scaled INT8/FP8 matmul | 量化/缩放矩阵乘专项 |
| `09_block_scaled_mm_sm120/` | MXFP8 block-scaled matmul | 低精度硬件专项 |
| `10_p2p/` | GPU P2P、IPC、memory coherence/order | GPU 拓扑与通信前置 |
| `11_gemv/` | CUDA 与 Triton GEMV、persistent kernel、benchmark | Decode/小 batch 访存路径桥接 |
| `12_megakernel/` | Triton/CUDA 的 MLP、GQA/decode Attention 与端到端小模型尝试 | 阶段 3 的可选综合阅读 |

仓库 README 还给出 `ncu`、`compute-sanitizer`、PyTorch Profiler 和 Perfetto 的使用提示；这些与本项目阶段 1 的 profiler 验收直接互补。

## 适合怎样融入本学习路线

结论：**有必要纳入，但作为阶段 1 的配套代码阅读/可选实验轨道，不替代 CUDA Programming Guide、Triton 官方教程、论文或 AIInfraGuide 路线，也不把它安排到当前 Transformer 主线之前。**

推荐依赖顺序：

1. 先完成当前阶段 0 的 Decoder-only Transformer、Attention shape 和基本 PyTorch 抽象；
2. 进入阶段 1 后，先读 GPU execution/memory hierarchy 的本地笔记和官方资料；
3. 用 `01_vector_addition` 建立 extension—kernel—tensor 的最小映射；
4. 依次阅读 `03_sum`、`02_matmul_simt`、`04_softmax`，把归约、tiling、访存和数值稳定性连起来；
5. 再读 `07_attention`，将标准 Attention、online Softmax 和 FlashAttention 的理论映射到 kernel 数据流；
6. 基础 CUDA 稳定后，用 `02_matmul_simt/matmul_triton.py` 和 `11_gemv/triton_v1.py` 对比 CUDA 与 Triton 的抽象边界；
7. 读 `10_p2p` 作为阶段 0 GPU/通信与阶段 2 分布式训练之间的桥接；
8. `02_matmul_sm80/SM100/SM120`、`05_fp6`、`08/09` 和 `12_megakernel` 只作为后续专项或综合复习，不设为主线必修。

## 采用边界与风险

- README 中的 benchmark 来自 4070 Ti SUPER、5090、A100、H200 或 Modal 等特定环境，并依赖 CUDA 12.9/13.0、PyTorch 2.10/2.11 等版本；数字只作为实验上下文，不能直接写入本项目的性能结论。
- 部分代码面向 Ampere/Blackwell/AMD 特定指令和工具链，可能无法在其他 GPU、驱动或 CUDA 版本编译；阅读时先看架构和 dtype 假设。
- 仓库没有统一测试入口，部分 README 明确包含 TODO、经验性观察或作者个人判断；技术事实需回到 NVIDIA 文档、PTX/CUTLASS 文档、论文或独立推导核查。
- 根目录 `pyproject.toml` 仅包含 Ruff 配置，未提供统一依赖锁、容器、Makefile/CMake 或 CI；运行依赖分散在各 lesson 的脚本和 README 中。
- 主要验证环境是 Linux + NVIDIA CUDA/PyTorch JIT extension；README 对 Windows 只给出 include path 需要调整的提示，不能视为 Windows 可复现支持。
- 当前未发现明确开源许可证；本仓库只保存链接、固定 commit、目录摘要和学习映射，不复制上游代码、benchmark 输出或 README 长段落。
- 本项目默认不要求配置、编译、运行或复现 benchmark；阅读代码时将“预期数据流”和“实际验证方法”分开记录。

## 本项目的验收映射

将上游代码转化为以下理解验收，而不是照抄代码：

- 能从 `01_vector_addition` 解释 PyTorch extension 的输入检查、指针取得、grid/block 配置、kernel 边界判断和输出生命周期；
- 能比较 `03_sum` 的朴素归约、共享内存树归约、warp shuffle 和向量化加载，指出同步、访存和 occupancy 代价；
- 能从 `02_matmul_simt` 解释 block/warp/thread tiling、Shared Memory 复用、寄存器累加、coalescing 和 Bank Conflict；
- 能从 `04_softmax` 解释 max-subtraction、online 状态、split-N 与 atomic 的收益和代价；
- 能将 `07_attention` 的版本演进连接到 Attention 的 Q/K/V tile、online Softmax、流水线和 HBM I/O；
- 能用 `matmul_triton.py` 说明 Triton 的 program id、pointer arithmetic、mask、`tl.dot`、autotune 和 layout 抽象，并与 CUDA thread/block 模型比较；
- 能说明 `10_p2p` 中 peer access、IPC、进程地址有效性、coherence/order 与 NCCL 的关系；
- 能识别 `12_megakernel` 中 decode/GQA/融合的系统目标，但不提前把推理 serving 专题拉入阶段 1。

完成这些阅读验收后，才把对应阶段标记为 `待自检` 或 `已掌握`；仅浏览仓库不改变学习状态。

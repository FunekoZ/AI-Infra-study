# CUDA 与算子优化笔记

主题范围：GPU 架构、存储层次、CUDA 编程模型、Reduce、GEMM、Softmax、FlashAttention、Triton 与性能分析。

建议按以下实验驱动顺序新增笔记：

1. CUDA execution model 与 memory hierarchy；
2. Reduce 三种实现；
3. Transpose 与 Bank Conflict；
4. Tiled GEMM；
5. Online Softmax 与 FlashAttention；
6. Nsight Systems/Compute 分析方法。

### 配套代码阅读轨道：`learn-cuda`

[Learn CUDA with PyTorch](https://github.com/gau-nernst/learn-cuda/tree/8c4d1b887a25727b320bc3ace19b63e2db6f8b44) 作为本阶段的外部代码 companion，固定到 `main@8c4d1b887a25727b320bc3ace19b63e2db6f8b44`。建议在官方 CUDA/Triton 资料和本地概念笔记之后，按 `01_vector_addition → 03_sum → 02_matmul_simt → 04_softmax → 07_attention` 阅读；`10_p2p`、`11_gemv`、`12_megakernel` 放到通信或推理阶段选读，SM-specific 和低精度目录作为专项材料。

该仓库没有在固定 commit 中发现明确许可证，且 benchmark 绑定特定 GPU、CUDA/PyTorch 版本；本仓库只保留链接、版本和阅读映射，不复制上游代码，不把其性能数字当作已验证事实。详细目录、风险和验收映射见 [`resources/learn-cuda-source.md`](../../resources/learn-cuda-source.md)。

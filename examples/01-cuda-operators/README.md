# CUDA 与算子教学代码

按需保存 CUDA/Triton、Reduce、Transpose、GEMM、Softmax 和 Attention 算子的阅读示例。可以并列朴素版和优化版，但不声称已经编译或获得性能结果。

外部代码阅读 companion：[learn-cuda 固定版本](https://github.com/gau-nernst/learn-cuda/tree/8c4d1b887a25727b320bc3ace19b63e2db6f8b44)。本仓库不复制其源代码；需要建立教学代码时，先根据其思路独立重写最小示例，并记录 shape、dtype、device、架构假设和未运行声明。推荐阅读映射与许可证边界见 [`resources/learn-cuda-source.md`](../../resources/learn-cuda-source.md)。

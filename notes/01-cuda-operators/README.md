# CUDA 与算子优化笔记

主题范围：GPU 架构、存储层次、CUDA 编程模型、Reduce、GEMM、Softmax、FlashAttention、Triton 与性能分析。

建议按以下实验驱动顺序新增笔记：

1. CUDA execution model 与 memory hierarchy；
2. Reduce 三种实现；
3. Transpose 与 Bank Conflict；
4. Tiled GEMM；
5. Online Softmax 与 FlashAttention；
6. Nsight Systems/Compute 分析方法。

相关教学代码按需放入 `examples/01-cuda-operators/`。代码可以展示朴素实现与优化思路，但默认仅供阅读，不声称已经编译、运行或达到任何性能数字。网站面试宝典和手撕题映射到 `interview/01-cuda-operators/`，用于检验是否能从代码、访存和硬件角度解释优化。

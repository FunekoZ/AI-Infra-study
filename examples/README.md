# 教学代码

本目录保存为理解 AI Infra 知识而编写的带注释代码，不以构建可运行工程为目标。

## 目录映射

- `00-prerequisites/`：Python、C/C++、Transformer、PyTorch 抽象与集合通信基础。
- `01-cuda-operators/`：CUDA、Triton、Reduce、GEMM、Softmax 与 Attention 算子。
- `02-distributed-training/`：DDP、FSDP、ZeRO、TP、PP、SP 与 MoE。
- `03-inference-serving/`：KV Cache、PagedAttention、batching、量化与推理调度。

## 文件要求

- 一个文件聚焦一个知识点。
- 文件顶部写明路线位置、学习目标和“默认不要求运行”。
- 对 shape、dtype、device、内存布局和关键数据流提供充分中文注释。
- 注释解释设计原因和真实系统中的差异，不只翻译语法。
- 未实际执行时明确标记“仅供阅读，未经本环境运行验证”。
- 不添加与理解无关的工程脚手架。

# 分布式训练笔记

主题范围：优化器显存、DDP、FSDP、ZeRO、TP、PP、SP、MoE、混合精度与 activation checkpointing。

建议优先建立两个账本：

1. **显存账本**：参数、梯度、master weights、优化器状态、activation 与临时 buffer；
2. **通信账本**：collective 类型、消息大小、频率、参与 rank、链路带宽与是否能和计算重叠。

任何容量或通信量结论都需注明 dtype、并行规模、实现口径和单位。需要展示 DDP、FSDP、ZeRO 或并行策略接口时，将带注释示例放入 `examples/02-distributed-training/`，默认仅供代码阅读。对应的显存计算、并行方案设计和故障定位面试题放入 `interview/02-distributed-training/`。

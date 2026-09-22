# 前置知识面试题

本阶段收录经 AIInfraGuide 固定源码版本核对的问题，范围包括编程与系统基础、数学、Transformer、PyTorch、GPU 基础和集合通信。第一版跨阶段题簇见 [../core-question-map.md](../core-question-map.md)；本目录后续只保存进入学习或需要详细回答骨架的阶段题卡，避免复制整份索引。

当前主题首先关注：

- Decoder-only Transformer Block 数据流；
- Q/K/V 与多头 Attention shape；
- scale、causal mask、softmax 和 value aggregation；
- Attention 参数量、计算量与 `O(S²)`；
- GPU/通信基础为什么会成为后续 AI Infra 优化前提。

当前代表题已确定为：Decoder-only 全链路、Attention shape、scale、causal mask、MHA 实现和 GQA 递进。它们在 [../core-question-map.md](../core-question-map.md) 中保留源文件、题号与 `unseen` 状态；尚未开始作答，不因完成索引而视为掌握。

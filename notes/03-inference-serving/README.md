# 推理与部署笔记

主题范围：Prefill/Decode、KV Cache、PagedAttention、Continuous Batching、Prefix Cache、量化、Speculative Decoding、Prefill/Decode 解耦与 Benchmark。

建议首先完成：

1. 推理数据流与指标定义；
2. KV Cache shape 和容量推导；
3. 单一引擎的固定负载 baseline；
4. 一次只改变一个变量的优化实验。

学习指标时关注 TTFT、TPOT、端到端 Token/s、P50/P95、峰值显存、GPU 利用率和 Goodput（若有明确 SLO）。需要理解调度、KV Cache 或量化接口时，将带注释示例放入 `examples/03-inference-serving/`，不要求实际部署或压测。对应的容量计算、系统设计和性能定位题放入 `interview/03-inference-serving/`。

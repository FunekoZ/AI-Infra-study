# 学习进度

> 初始化日期：2026-09-20
>
> 本文件是跨会话的唯一进度指针。状态约定：`未开始` / `学习中` / `待自检` / `已掌握` / `补充中` / `待复盘`。

## 当前学习状态

- **最后更新**：2026-09-22
- **路线依据**：[AIInfraGuide 官方仓库](https://github.com/caomaolufei/AIInfraGuide)源码为主要读取入口；[学习路线](https://caomaolufei.github.io/AIInfraGuide/guides/ai-infra%E5%AD%A6%E4%B9%A0%E8%B7%AF%E7%BA%BF/)与[面试宝典](https://caomaolufei.github.io/AIInfraGuide/interview/)用于部署一致性核对
- **路线最近核对**：2026-09-22（固定版本 `main@a3b63eeb81d6d36a3c42c8cfc5a1bdd96e36bab1`；路线 frontmatter `pubDate`：2026-03-26；公开入口与代表性页面已抽样核对）
- **学习模式**：对话驱动、理解优先；可创建带充分注释的教学代码，但默认不要求实际运行
- **当前阶段**：第零层——前置知识
- **当前模块**：Transformer 基础
- **当前主题**：Decoder-only Transformer 整体数据流与 Self-Attention
- **当前状态**：未开始
- **当前目标**：建立后续 CUDA、分布式训练和推理优化共同依赖的 Transformer 计算与数据流基础，并能回答 AIInfraGuide 面试材料中对应的代表性问题。
- **当前知识验收**：尚未开始 Decoder Block、Q/K/V shape、Attention 数据流与复杂度推导。
- **当前面试验收**：已从固定源码版本的 10 篇综合面经中提取并语义去重第一版题簇，确定当前主题主问 `CQ-0-ATTN-IMPL`（MHA 实现）、GQA 递进，以及 Decoder-only、shape、mask、scale 四条叶子题补充；状态均为 `unseen`，尚未开始作答验收。
- **已掌握内容与证据**：尚无具体技术主题通过知识与面试双重验收；仓库学习协议、双轴路线和面试目录已建立。
- **长期复盘记录**：`notes/review-index.md` 已建立，当前无具体条目；后续只记录真实解决的问题和较难掌握的知识点。
- **未解决问题**：尚未系统梳理 Decoder Block、Q/K/V shape、Attention 复杂度及其与 AI Infra 瓶颈的关系；公司叶子面经改为随主题增量读取，不再阻塞开始学习。
- **活动临时分支**：无
- **主线回归点**：第零层 → Transformer 基础 → Decoder-only Transformer 数据流
- **分支退出条件**：无活动分支
- **唯一下一步**：开始 M1 第一项：理解并口述 Decoder-only Transformer 从 token embedding 经过 Pre-Norm、Masked Self-Attention、residual、FFN 到输出 hidden states 的整体数据流，同时标注每一步 `(B, S, D)` shape。
- **完成标准**：不看资料画出或口述一个 Decoder Block；说明两条 residual 路径、normalization 位置、Attention 与 FFN 的输入输出；能回答 `CQ-0-TRANSFORMER-FLOW` 的主问题，暂不要求本轮完成 Q/K/V 拆头细节。
- **关联笔记、代码、面试与资料**：`notes/00-prerequisites/`、`examples/00-prerequisites/`、`interview/core-question-map.md`、`interview/source-index.md`、`resources/ai-infra-guide-source.md`、`resources/learn-cuda-source.md`、`resources/resources.yaml`

## 当前概览

| 阶段 | 状态 | 理论重点 | 笔记入口 |
|---|---|---|---|
| 0. 前置知识 | 未开始 | Transformer、数学、PyTorch 抽象、GPU 与集合通信基础 | `notes/00-prerequisites/` |
| 1. CUDA 与算子优化 | 未开始 | GPU 架构、内存层次、Kernel 与经典算子原理 | `notes/01-cuda-operators/` |
| 2. 分布式训练 | 未开始 | 显存与通信账本、并行策略和数值格式 | `notes/02-distributed-training/` |
| 3. 推理与部署 | 未开始 | KV Cache、调度、量化、推测解码与服务指标 | `notes/03-inference-serving/` |

## 当前里程碑

### M0：学习协议、知识框架与需求索引

- [x] 建立基础目录。
- [x] 整理网站路线和知识验收标准。
- [x] 建立资料元数据索引。
- [x] 固定“提问—回答—回归判断—下一步”的对话协议。
- [x] 建立临时分支与主线回归机制。
- [x] 建立知识主线与面试需求双轴规则。
- [x] 建立已解决问题与难点知识的长期复盘索引及原网站定位字段。
- [x] 系统核对网站面试宝典首页、梯队、公司与综合题库入口。
- [x] 读取 10 篇综合面经正文并核对主题范围。
- [x] 采用 GitHub source-first，记录固定 commit、源文件、内容指纹与部署抽样核对规则。
- [x] 将综合面经拆解为去重后的第一版具体题卡。
- [x] 读取当前 Transformer 主题所需的代表性公司叶子面经正文并提取具体题目。
- [x] 将已核实综合题目去重后映射到四阶段与横向能力轴。
- [ ] 随每个主题增量读取对应公司叶子面经，并合并到已有题簇。

### M1：Transformer 计算基础

- [ ] 说明 Decoder-only Transformer 的整体数据流。
- [ ] 推导 Q/K/V 和多头 Attention 的 shape。
- [ ] 解释 scale、mask、softmax 和 value aggregation 的作用。
- [ ] 推导标准 Self-Attention 对序列长度的复杂度。
- [ ] 说明 Attention 为什么会成为算子优化、分布式训练和推理系统的共同核心。
- [ ] 对本主题代表性面试题给出结构化回答并处理至少一个递进追问。
- [ ] 通过针对关键误区的知识与面试双重自检。

### M2：CUDA/Triton 代码阅读轨道（阶段 1 预登记）

- [x] 评估 `gau-nernst/learn-cuda` 的范围、版本、环境假设与许可证边界。
- [x] 将其定位为阶段 1 的代码 companion，而不是当前主线、独立阶段或官方事实来源。
- [x] 固定 `main@8c4d1b887a25727b320bc3ace19b63e2db6f8b44`，建立目录到路线的阅读映射。
- [ ] 进入阶段 1 后按 `01_vector_addition → 03_sum → 02_matmul_simt → 04_softmax → 07_attention` 完成代码阅读验收。
- [ ] 基础 Triton 官方教程完成后，对比 `matmul_triton.py` 的 program、mask、pointer arithmetic 和 autotune。
- [ ] 在阶段 2/3 按需选读 `10_p2p`、`11_gemv` 与 `12_megakernel`，不提前展开。

## 学习日志

按时间倒序记录。结论需标注为“资料结论”“原文推导”“面经样本”或“个人解释”。

### 2026-09-22：纳入 `learn-cuda` 代码阅读轨道

- **类型**：后续阶段资料与验收映射；不改变当前 Transformer 主线。
- **资料结论**：固定核对 `gau-nernst/learn-cuda main@8c4d1b887a25727b320bc3ace19b63e2db6f8b44`。仓库覆盖 PyTorch CUDA extension、SIMT/Tensor Core GEMM、Reduce、Softmax、Attention、Triton 对照、P2P、GEMV 和 LLM megakernel，但属于作者持续迭代的代码/benchmark worklog，不是完整课程或官方事实来源。
- **采用方式**：阶段 1 按 `01_vector_addition → 03_sum → 02_matmul_simt → 04_softmax → 07_attention` 阅读；高级硬件、低精度、P2P、GEMV 和 megakernel 延后到相应阶段选读。
- **边界**：固定 commit 未发现明确许可证，不复制其代码；README 性能数字受 GPU、功耗、CUDA/PyTorch 和 shape 影响，不作为本项目既成性能结论；默认不要求运行。
- **进度变化**：只完成未来课程融合和来源登记，阶段 1 仍为 `未开始`，当前唯一下一步仍是 Decoder-only Transformer Block 数据流。

### 2026-09-22：完成正式学习前的外部基准与题卡初始化

- **类型**：学习基础设施优化，不代表技术主题已掌握。
- **完成**：将 AIInfraGuide 调整为 GitHub 源码优先、部署网站抽样核对、技术事实回到一级来源；固定 `main@a3b63eeb81d6d36a3c42c8cfc5a1bdd96e36bab1`，建立忽略提交的 `.cache/AIInfraGuide/`、来源快照、统计复核和 10 篇综合面经 blob 指纹。
- **面经样本**：从 10 篇综合面经的 185 条编号原题建立第一版语义去重题簇并映射到四阶段与横向能力轴；读取当前 Transformer 主题需要的代表性叶子题，区分“路线知识验收”和“真实面经原题”。
- **部署核对**：学习路线、面试首页与代表性叶子页面返回 HTTP 200；首页显示 181 篇面经、65 家公司、7 个梯队，与固定源码统计一致。
- **进度变化**：M0 初始化完成到足以开始学习；Transformer 技术状态仍为 `未开始`，没有新增 `已掌握` 内容，也不创建复盘条目。
- **下一步**：开始 Decoder-only Transformer Block 整体数据流与 `(B, S, D)` shape。

### 2026-09-21：增加长期复盘记录规则

- **类型**：笔记规范调整。
- **完成**：新增 `notes/review-index.md`，要求保存已经解决的问题、花费较久才掌握的知识点、突破点、易忘细节、复习自检和原网站页面/章节/题目定位；同步更新 `CLAUDE.md`、`README.md` 和笔记规范。
- **进度变化**：没有新增技术知识；当前复盘索引为空，不虚构学习成果。

### 2026-09-21：确认面试宝典准确入口

- **类型**：外部基准核对。
- **完成**：根据用户提供的 `https://caomaolufei.github.io/AIInfraGuide/interview/` 核对面试宝典首页与官方仓库；确认页面显示 181 篇面经、65 家公司、7 个梯队，仓库 `docs/interview/` 有 181 个 Markdown 文件；整理梯队、公司、综合题库和 10 篇综合面经的正文主题。
- **边界**：综合 10 篇已核对主题范围但尚未全部拆成去重题卡；其余公司页面只凭目录不能证明具体问题或行业频率，仍需逐篇读取。
- **进度变化**：面试来源总目录已建立，下一步进入具体题目提取与四阶段映射。

### 2026-09-21：纳入面试宝典与真实需求轴

- **类型**：路线完整性修正。
- **完成**：确认原框架遗漏了参考网站的面试宝典、面经和面试题；建立 `interview/`，规定题目来源、分级、回答骨架、追问与四阶段映射；主题完成标准改为知识与面试双重验收。
- **进度变化**：技术主线仍在 Transformer 基础，但唯一下一步暂时调整为先完成网站面试内容索引，避免继续基于不完整路线学习。
- **下一步**：核对网站及官方仓库中的面试页面和源文件，完成第一版映射后回到 Transformer 主线。

### 2026-09-21：调整为理解导向并允许教学代码

- **类型**：学习模式与仓库结构调整。
- **完成**：允许按知识点创建带充分中文注释的教学代码，但默认不要求运行；将可信资料扩展到经交叉核查的知乎专栏、博客、源码导读和视频；决定移除初期冗余的 `labs/`、`benchmarks/` 与全局 `assets/`，代码统一按阶段放入 `examples/`。
- **进度变化**：具体技术主线不变，仍在第零层 Transformer 基础。
- **下一步**：理解 Decoder-only Transformer 数据流与 Self-Attention shape；讲解过程中按需创建对应教学代码。

### 2026-09-21：确立对话式学习与主线控制

- **类型**：学习协议调整。
- **完成**：取消环境配置和实际 Benchmark 作为默认任务；加入资料按需下载、最小充分解释、临时分支和主线回归机制。
- **后续修订**：同日进一步明确可以创建仅供阅读的带注释教学代码，因此本项目并非“纯理论”或“无代码”。
- **进度变化**：原“PyTorch 环境准备”不再是主线任务；主线重置到第零层的 Transformer 基础。
- **下一步**：理解 Decoder-only Transformer 数据流与 Self-Attention shape。

### 2026-09-20：仓库初始化

- **类型**：仓库初始化。
- **完成**：依据项目规范和参考学习路线建立目录、路线、资料清单及模板。
- **说明**：尚未开始具体理论主题。

## 待回答问题

| 问题 | 所属位置 | 状态 | 结论链接 |
|---|---|---|---|
| Decoder-only Transformer 中数据如何流经 Attention 与 FFN？ | 第零层 / Transformer | 待学习 | — |
| Q、K、V 和 attention score 的 shape 如何推导？ | 第零层 / Transformer | 待学习 | — |
| 为什么标准 Self-Attention 随序列长度呈二次复杂度？ | 第零层 / Transformer | 待学习 | — |

## 阶段复盘模板

```markdown
### YYYY-MM-DD：主题或里程碑

- 主线位置：
- 已掌握内容：
- 仍存在的误区：
- 关键公式或数据流：
- 代表性面试题及状态：
- 递进追问薄弱点：
- 计算/通信/显存/精度/延迟/吞吐/复杂度 trade-off：
- 活动分支及回归状态：
- 唯一下一步：
```

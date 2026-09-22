# 资料目录

资料元数据统一登记在 [resources.yaml](resources.yaml)。

- [ai-infra-guide-source.md](ai-infra-guide-source.md)：AIInfraGuide 固定 commit、主要源文件、统计复核、内容指纹和重新同步流程。
- [learn-cuda-source.md](learn-cuda-source.md)：learn-cuda 固定 commit、目录评估、阶段映射、版本假设和代码复用边界。
- `papers/`：来源可信且允许保存的论文原文。
- `docs/`：来源可信且允许本地保存的官方文档、课程材料或网络文章。

AIInfraGuide 等持续更新的外部代码仓库默认浅克隆到 `.cache/<repository>/`，该目录不提交 Git；本仓库只保存来源 URL、分支、commit SHA、核对日期和提炼后的结构化索引。这样既能批量检索 Markdown/frontmatter，也避免复制整站内容或让上游历史污染学习仓库。

默认只登记链接；需要逐节精读、核对公式或多轮反复引用时再下载。下载后填写 `local_path`，并保持原始文件不被修改。模型权重、数据集和大型构建产物不放入此目录，也不提交 Git。

## 来源层级

- `primary`：论文、标准、官方文档、官方博客、官方仓库或作者材料。
- `secondary`：大学课程、研究机构、业内专家文章、权威技术报告或有可靠引用的源码导读。
- `community`：知乎专栏、个人博客、社区教程和视频等网络讲解。

`community` 来源经核查后可以用于讲解，不因并非第一出处而排除。核查时关注作者背景、引用链、版本、公式与一级来源是否一致，以及事实和观点是否分开。关键技术事实不应只依赖一个未经核实的社区来源。

建议为新增资料记录：

- `source_tier`：来源层级；
- `verification`：`unverified` / `cross-checked` / `primary-source`；
- `notes`：核查依据、适用范围和已知局限。

阅读状态约定：

- `unread`：尚未阅读；
- `reading`：阅读中；
- `read`：已完成初读；
- `reviewed`：已结合笔记或教学代码复盘。

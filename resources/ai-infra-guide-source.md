# AIInfraGuide 上游来源快照

> 本文件记录本仓库对外部学习基准所采用的可复现版本口径，不复制上游正文。

## 当前固定版本

- **上游仓库**：https://github.com/caomaolufei/AIInfraGuide
- **分支**：`main`
- **commit SHA**：`a3b63eeb81d6d36a3c42c8cfc5a1bdd96e36bab1`
- **commit 时间**：2026-09-22T16:45:52+08:00
- **核对日期**：2026-09-22
- **获取方式**：官方仓库浅克隆；正文和元数据从固定 commit 的源文件读取
- **部署抽样**：2026-09-22 通过公开 URL 核对，学习路线、面试首页和 `AI Infra 一面` 均返回 HTTP 200；面试首页显示 181 篇、65 家、7 个梯队
- **本地缓存约定**：`.cache/AIInfraGuide/`，不提交 Git

固定 commit 的目的，是让路线、题目数量和引用位置能够复现；它不表示上游以后不再更新。重新同步时，应先比较新旧 commit，再只更新发生变化的本地索引和题卡。

## 主要源文件

| 用途 | 上游路径 | 本地使用方式 |
|---|---|---|
| 学习路线 | `docs/guides/AI Infra学习路线.md` | 恢复阶段、顺序、推荐资料和检验标准 |
| 面经正文 | `docs/interview/*.md` | 提取原题、frontmatter、公司、梯队、面试类型和轮次 |
| 内容 schema | `src/content/config.ts` | 核对字段定义、枚举、默认值和 `draft` 语义 |
| 面试首页 | `src/pages/interview/index.astro` | 核对公开入口的页面描述 |
| 文章路由 | `src/pages/interview/[...slug].astro` | 核对公开 slug 与 `draft` 过滤逻辑 |
| 分组逻辑 | `src/utils/companyGrouping.ts` | 核对梯队顺序和公司分组方式 |

## 当前统计复核

对固定 commit 中 `docs/interview/*.md` 的 frontmatter 直接统计：

- Markdown 文件：181；
- 唯一公司/分组：65；
- 梯队：7 个；
- 分布：T0 53、T1 32、T2 9、T3 22、T4 24、T5 31、综合 10；
- 面试类型：实习 76、校招 38、社招 1、未知 66；
- 轮次：一面 84、二面 24、三面 1、一二面 4、一二三面 4、未标注 64。

这些数字只描述该 commit 收录的样本，不能外推为行业总体频率。

## 内容指纹

以下 blob SHA 用于判断已完成第一版拆题的 10 篇综合面经是否发生正文变化：

| 上游源文件 | blob SHA |
|---|---|
| `docs/interview/AI-Infra-一面.md` | `9f1570fe4de3f6dc0d55e265cbdc58183cfbdd2c` |
| `docs/interview/AI-Infra-校招-1.md` | `726d45e9610dbb4861acea73b47205553a321212` |
| `docs/interview/AI-Infra-综合面经题库-1.md` | `b94bc3883fe94c6b1e5d72bb33493c628725a074` |
| `docs/interview/AI-Infra-综合面经题库-2.md` | `dab00f85d067253d38d6f8a7fc21f382c581b674` |
| `docs/interview/AI-Infra-综合面经题库-3.md` | `411f0b8a36e2582456bb2f452e3c979606d91488` |
| `docs/interview/AI-Infra-综合面经题库-4.md` | `57d37c4ef14013b5cb6c40e64b4771161c1eb8ff` |
| `docs/interview/AI-Infra-综合面经题库-5.md` | `df46de7255d88f06d61244dbd6af77b1ac7bf155` |
| `docs/interview/AI-Infra-综合面经题库-6.md` | `13f2516af8c70c361a1876139824edeeabea927f` |
| `docs/interview/AI-Infra-综合面经题库-7.md` | `7a68e0492ec63be4f43c7c862ceb30618204c0b6` |
| `docs/interview/AI-Infra-面经-1.md` | `40959b249835765ea53576817825cb7f929e6032` |

## 网站核对职责

部署网站不再承担批量内容读取，只抽样检查：

1. 学习路线和面试宝典公开入口可访问；
2. 源文件对应的 slug、标题与页面导航一致；
3. 页面统计与固定源码版本是否一致；
4. Markdown 渲染是否遗漏题号、标题或关键公式；
5. 如有差异，是否来自尚未部署、`draft` 过滤或分支/commit 不一致。

## 重新同步流程

1. 更新 `.cache/AIInfraGuide/`，记录新的 `main` commit；
2. 比较本文件记录的 commit 与 blob SHA；
3. 只重读变化过的路线、面经和页面逻辑文件；
4. 更新 `roadmap/learning-path.md`、`interview/source-index.md`、题卡和 `resources/resources.yaml`；
5. 抽样核对部署网站；
6. 在 `roadmap/progress.md` 记录核对日期、差异和是否影响唯一下一步。

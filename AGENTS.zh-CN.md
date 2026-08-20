# AGENTS.md（中文版）

## 项目结构与模块组织

本仓库是一个基于 Markdown 的知识库。

未经处理的参考资料存放在只读目录 `raw/` 下，并按来源类型组织：

- `raw/articles/`、`raw/docs/`、`raw/repos/`、`raw/transcripts/`

整理后的内容存放在 `wiki/` 下：

- `wiki/index.md` — 以内容为导向的总索引
- `wiki/log.md` — 仅追加的重大更新变更日志
- `wiki/concepts/` — 主题/技术页面
- `wiki/comparisons/` — 一对一比较评估
- `wiki/entities/` — 人物、项目、公司、工具
- `wiki/decisions/` — 架构/工具决策及其理由
- `wiki/sources/` — 每个已摄取原始文件对应一篇结构化笔记

轻量级导航层位于 `mocs/`（Maps of Content，内容地图）下：

- `mocs/Home.md` — 唯一入口，链接到所有领域 MOC
- `mocs/<Domain> MOC.md` — 每个主题一个（例如 “RAG MOC”“Agent Frameworks MOC”）

MOC 只包含链接和单行说明，不包含详细内容。这样可以降低阅读路径的成本。

## 角色

你负责维护这个知识库。用户提供原始材料并提出问题。`raw/` 是只读的事实依据，绝不能编辑。你可以自由创建、重写和重组 `wiki/` 与 `mocs/` 中的内容。

## 页面 Frontmatter

每个 `wiki/` 和 `mocs/` 页面都必须以下列内容开头：

```yaml
---
title: Page Title
type: concept | comparison | entity | decision | source | moc
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [raw-file-1, raw-file-2]
tags: [tag1, tag2]
---
```

## MOC 创建与维护规则

不预先规划 MOC，而是随着内容增长逐步生成。

1. 本仓库第一次执行摄取时创建 `mocs/Home.md`。它只列出领域 MOC 和一个简短的 “Recently Active” 部分，绝不列出页面级细节。
2. 创建新的 `wiki/concepts/`、`wiki/comparisons/`、`wiki/entities/` 或 `wiki/decisions/` 页面时，检查是否已有 `mocs/<Domain> MOC.md` 覆盖其主题。
   - 如果有，则在正确的分区（Concepts / Comparisons / Entities / Decisions）下为该页面添加单行链接。
   - 如果没有匹配的领域 MOC，并且当前已有 3 个或更多相关页面尚未归入 MOC，则创建 `mocs/<Domain> MOC.md`，并补充指向所有现有相关页面的链接。
3. 每当创建新的领域 MOC 时，都要在 `mocs/Home.md` 中添加指向它的链接。
4. 每次摄取后，更新 `mocs/Home.md` 的 “Recently Active” 部分，列出最近修改的 5 个页面（标题 + 相对链接），并移除最旧的一项。
5. MOC 绝不能包含成段说明、摘要或详细内容，只能包含一行范围说明和链接。如果 MOC 中积累了实质性内容，将这些内容移至合适的正式页面，并仅在 MOC 中保留链接。

## 摄取工作流

当用户说 “ingest this”“sync the wiki”“fold this in”，或运行 `/wiki-sync` 时触发。

1. 读取 `raw/` 下的新文件。
2. 阅读 `wiki/index.md` 和相关的 `mocs/<Domain> MOC.md`，了解现有覆盖范围并避免创建重复页面。
3. 在 `wiki/sources/<slug>.md` 中编写来源笔记（2–3 句摘要、关键主张、出处信息）。
4. 提取值得单独成页的概念、实体、比较和决策。优先更新现有页面，再创建新页面；应写“当前理解”，而不是编辑历史。由于 `log.md` 保留了变更轨迹，因此可以覆盖旧内容。
5. 如果作出或更改了技术/架构选择，则在 `wiki/decisions/` 中创建或更新页面（背景、考虑过的选项、决策、后果）。
6. 使用相对链接将每个新增或更新的页面与相关页面相互链接，例如 `[Concept](../concepts/concept-name.md)`。
7. 在 `wiki/index.md` 中为每个涉及的页面更新一条单行条目。
8. 对每个涉及的页面应用上述 MOC 创建与维护规则。
9. 如果新信息与现有页面相矛盾，不要静默覆盖；添加 `## Contradictions` 部分，列出两个版本及其来源，并标记出来交由用户解决。
10. 在 `wiki/log.md` 中追加一行：`## [YYYY-MM-DD] ingest | <source> -> <pages touched>`。
11. 在回复中总结变更（创建/更新的页面、创建/更新的 MOC、标记的矛盾）。

## 查询工作流

任何不属于摄取请求的问题都会触发此工作流。

1. 从 `mocs/Home.md` 开始，然后进入相关领域 MOC；绝不要扫描整个 wiki。
2. 只加载回答问题所需的特定页面（目标不超过 7 个）。
3. 如果 wiki 页面细节不足，则回退到其 `wiki/sources/` 笔记所引用的 `raw/` 来源。
4. 回答时使用相对链接注明参考了哪些 wiki 页面。
5. 如果问题暴露出内容缺口（没有页面或 MOC 覆盖），应明确说明，不要猜测；如果有相关材料，可以提议摄取。之后更新 wiki，让下次回答同一问题的成本更低。

## 维护工作流

定期或按要求运行。检查并报告：

- 孤立页面（没有任何入站链接，包括来自 MOC 的链接）
- 重复或近似重复的页面
- 页面和 MOC 中失效的相对链接
- 陈旧页面（超过 90 天未更新）
- 已偏离规范、开始包含说明性段落或详细内容的 MOC
- `mocs/Home.md` 中缺失的领域 MOC
- 尚未解决的 `## Contradictions` 部分
- 没有链接到结果或后续行动的决策

## 构建、测试与开发命令

本项目没有构建系统或应用运行时，直接处理 Markdown 文件即可。提交变更前运行：

```sh
git diff --check
rg --files raw wiki mocs
```

`git diff --check` 用于检测空白字符错误。`rg --files` 用于确认新内容存放在预期目录中。

## 编码风格与命名约定

- 每个页面只能有一个 `#` 标题，后续使用层级正确的 `##`/`###` 标题。
- 标题、列表和代码围栏前后留空行。
- 仓库内页面之间优先使用相对链接。
- 文件名使用具有描述性的、小写 kebab-case 格式（例如 `distributed-systems.md`）。
- `raw/` 必须逐字忠实保留来源。为清晰起见，使用自己的表达重写 `wiki/` 内容；它应是持续演进的综合整理，而不是来源副本。
- 每个 `wiki/` 页面都应先用 2–3 句自包含摘要开篇，再展开详细内容。

## 测试指南

在 Markdown 预览中检查每个变更页面。确认：

- 相对链接指向实际存在的文件。
- 标题层级正确，没有跳级。
- Frontmatter 存在且有效。
- 代码围栏均已闭合。
- 来源主张在 `wiki/sources/` 中有对应条目。
- MOC 链接有效，且 MOC 不包含说明性段落。

## 提交与 Pull Request 指南

提交主题应简短、使用祈使语气，并可包含可选的作用域，例如 `docs(concepts): explain consensus models`。每次提交应聚焦于一个主题。Pull Request 应总结内容变更、指出重要来源、列出移动或重命名的页面，并链接相关 issue。

## 安全与来源规范

未经许可，不要提交凭据、私人记录、个人数据或受版权保护的来源材料合集。将外部材料导入 `wiki/sources/` 时，记录其出处和许可信息。

## 语言政策

- `raw/` 下的材料始终逐字保留原始语言，不得在原文件中翻译。
- `wiki/` 下的整理页面（包括英文材料的来源说明）默认使用中文综合；只有明确面向英文读者的页面才使用英文。
- 非中文材料的来源说明必须记录来源语言，并保留原始标题、技术术语、专有名词、代码标识符及必要的短引文。
- 不得仅为便于检索而导入或翻译复制受版权保护的全文；应在 `wiki/` 中综合摘要，并保留稳定标识符或出处链接。
- 为保持一致，`wiki/index.md`、`wiki/log.md` 和 `mocs/` 可以使用英文标题；说明文字采用本仓库默认的中文综合语言。

## 跨模型一致性

由于可能由不同模型在不同时间执行摄取，因此始终遵守以下要求：

- 新建页面前，重新阅读 2–3 个同类型的现有 wiki 页面，以匹配其风格和内容深度。
- 严格遵循 Frontmatter schema 和页面结构，不要擅自增加字段或章节。
- 如果不确定某项内容是否属于 `decision`，默认归类为 `concept`，交由人工审核后重新分类。

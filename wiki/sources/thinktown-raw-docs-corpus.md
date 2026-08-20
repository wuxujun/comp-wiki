---
title: "Thinktown 原始文档集合"
type: source
created: 2026-08-20
updated: 2026-08-20
sources: ["raw/docs/"]
tags: ["thinktown", "raw-corpus", "source-catalog"]
---

# Thinktown 原始文档集合

本来源说明覆盖 `raw/docs/` 中的 389 份中文或中英双语材料，内容包括赛事资料、课程与产品说明、获奖案例及少量综合推荐文档。该集合主要来自 Thinktown 自有文件与分享页面，也包含微信公众号材料和缺少外部 URL 的 OCR 文本，因此最适合用来理解机构自身的产品设计与公开表述，而不是替代赛事主办方或独立第三方证据。

## 来源信息

- **原始目录：** `raw/docs/`
- **文档数量：** 389
- **总行数：** 76,194
- **语言：** 中文或中英双语
- **外部来源：** 166 份 Thinktown 文件导出、122 份 Thinktown 分享页、39 份微信公众号文章，另有 62 份未记录外部 URL
- **许可/授权状态：** 389 份均未附可验证的许可或再分发授权，按“状态未知”处理
- **编译日期：** 2026-08-20

## 集合构成

- [赛事基础资料目录](thinktown-competition-reference-sources.md)收录 121 份材料。
- [赛事分析与项目资料目录](thinktown-competition-analysis-sources.md)收录 86 份材料。
- [课程与产品资料目录](thinktown-course-and-product-sources.md)收录 129 份材料。
- [成果与案例资料目录](thinktown-achievement-and-case-sources.md)收录 47 份材料。
- [其他资料目录](thinktown-other-sources.md)收录 6 份材料。

上述分类用于检索，不是原始材料自带的正式分类；每份 raw 文档只在一个目录中出现，五类合计覆盖全部 389 份文件。

## 核心主张

- 集合展示的产品谱系包括赛事信息与推荐、竞赛备赛、PBL 与学术探索、单科学术顾问计划，以及以获奖或作品为中心的案例传播。
- 课程材料反复采用一对一指导、Pre-Talk 评估、CT/NCT 分工、阶段节点和明确交付物来描述服务流程。
- 赛事材料通常同时记录主办方、适用年级、活动形式、时间、难度、奖项和后续晋级，但不同年份与不同版本会并存。
- 成果材料将获奖、晋级、发表和录取用于证明产品价值；这些是机构公开主张，不等同于独立核验的效果评估。

## 元数据质量

360 份文件有结构化标题，238 份有结构化摘要，318 份在原始元数据中记录了外部 URL。另有 29 份没有结构化标题，部分材料是图片 OCR 后形成的单行文本，仍可检索但可读性较弱。

本轮另通过确定性文件地址回溯核验补齐 9 个 URL：这些地址均返回 HTTP 200，且响应 ETag 与对应记录 ID 一致。因此来源说明层现有 327 份记录外部 URL，仍有 62 份缺少可验证的外部发布位置。

122 份较早记录的 `subject` 字段全部写成“数学 Mathematics”，即使正文主题明显属于物理、化学、生物、历史、艺术或写作，因此该字段不能用于学科判断。本次编译保留 raw 原文不变，并以标题与正文内容进行主题识别。

## 可靠性与时效性

这些材料是了解 Thinktown 产品设计、宣传口径和公开案例的第一手来源，但对外部赛事事实通常只是二手转述。日期、报名费、价格、课时、规则、导师履历、录取与奖项数据均应视为带版本的历史记录；在作出现实决策前，需要到赛事主办方或其他权威来源重新核验。

原文中的 `has_uncertainty`、`facts`、`opinions` 等字段来自既有抽取流程，并不构成事实验证。集合还包含学生与学校信息，本 wiki 只做聚合分析，不复制个人身份信息。

## 权利与再分发边界

全部 389 份逐条来源说明均已显式记录许可状态：原始材料未附可验证的许可或再分发授权，因此统一按“状态未知”处理。本地收录用于溯源和知识整理，不构成公开转载、发布原件或再分发的授权；任何对外使用都需要另行核验权利主体、适用许可或获得明确授权。

仍缺外部发布位置的 62 份材料已列入[外部来源缺失核验队列](../../.audit/MISSING-EXTERNAL-ORIGINS.md)，其中成果与案例材料优先处理。

## 相关页面

- [Thinktown Education](../entities/thinktown-education.md)
- [Thinktown 学习产品体系](../concepts/thinktown-learning-product-system.md)
- [学术竞赛信息评估](../concepts/academic-competition-information-evaluation.md)
- [项目制与学术顾问课程设计](../concepts/project-based-and-academic-advising-design.md)
- [Thinktown 学习产品类型比较](../comparisons/thinktown-learning-product-types.md)

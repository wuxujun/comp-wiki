# Baseline Commit Plan

> 生成于 2026-08-20。此文件仅给出拟提交分组和安全门禁；尚未暂存或提交任何内容。

## 当前基线

- Canonical 内容根：`raw/`、`wiki/`、`mocs/`。
- 原始 Markdown：389 份。
- Wiki Markdown：419 份，其中 404 份位于 `wiki/sources/`，13 份为概念、比较或实体综合页。
- MOC：4 份。
- 生成计划前 Git 状态：7 个已跟踪文件有修改，841 个文件未跟踪。
- `.wiki/` 是兼容入口，不是第二套内容根。

## 提交前门禁

1. 不使用 `git add .`；按下列批次显式暂存。
2. `raw/` 仅在仓库访问级别、版权许可和个人信息政策确认后提交。
3. 逐项检查 7 个已跟踪文件的差异，避免把既有用户修改误并入错误批次。
4. 提交前运行 `git diff --check`、`rg --files raw wiki mocs` 和相对链接检查。
5. `.DS_Store`、Obsidian workspace 状态和本地 session 状态不得提交。

## 建议提交批次

### 1. Repository conventions and compatibility

建议主题：`chore(wiki): align canonical knowledge base root`

候选路径：

- `.gitignore`
- `.wiki/config.md`
- `.wiki/_index.md`
- `.wiki/schema.md`
- `.wiki/log.md`
- `AGENTS.md`、`AGENTS.zh-CN.md`：仅在确认现有修改均为预期内容后加入。

`.wiki/raw/`、`.wiki/wiki/` 和 `.wiki/output/` 的空脚手架索引暂不作为 canonical 内容提交；后续可在确认插件兼容方案后归档或移除。

### 2. Raw corpus

建议主题：`docs(raw): add Thinktown reference corpus`

候选路径：`raw/docs/`，共 389 份 Markdown。该批次默认保持待审查，不应进入公共仓库。

以下 9 份原始文件包含电子邮件地址，需要在提交前确认其公开性和必要性：

- `raw/docs/1eb81c7fe505cae30a456912fc253bd9.md`
- `raw/docs/415436d67df2c47b350eb6703da9239d.md`
- `raw/docs/9183a78ba997f574fe906c3b7d1ad811.md`
- `raw/docs/a6ef28a0430df9438988161d0510cbcb.md`
- `raw/docs/b0c2925055a16bb4542873b389a99d85.md`
- `raw/docs/b1ffd4b33f51278e04ae2d5e91bc7536.md`
- `raw/docs/b74cd45ca9d7fe03e21cd3018caeacef.md`
- `raw/docs/b8c701b192571d9139d7f48aceacf8f2.md`
- `raw/docs/bda7a0c8a9a3d853e3122c48232b219d.md`

### 3. Curated wiki

建议主题：`docs(wiki): add source notes and synthesized pages`

候选路径：

- `wiki/sources/`
- `wiki/concepts/`
- `wiki/comparisons/`
- `wiki/entities/`
- `wiki/decisions/`
- `wiki/index.md`
- `wiki/log.md`

提交前保留仍未解决的 `## Contradictions`。语言政策已明确为“`raw/` 保留原文、`wiki/` 默认中文综合”，英文来源页必须记录来源语言、稳定标识和许可边界。

### 4. Navigation

建议主题：`docs(mocs): add knowledge-base navigation`

候选路径：`mocs/`。确认 MOC 只包含范围说明、链接和一行描述，不承载正文知识。

### 5. Audit baseline

建议主题：`docs(audit): record knowledge-base baseline`

候选路径：

- `.audit/REPORT.md`
- `.audit/scan-results.json`
- `.audit/log.md`
- `.audit/BASELINE-COMMIT-PLAN.md`
- `.audit/REMEDIATION-STATUS.md`
- `.librarian/REPORT.md`
- `.librarian/scan-results.json`
- `.librarian/log.md`

## 明确排除

- `.DS_Store` 和任意子目录中的 `.DS_Store`
- `**/.obsidian/workspace*.json`
- `.wiki/.obsidian/`
- `.session-checkpoint.json`
- `.session-events.jsonl`

## 下一道决策门

在真正暂存或提交前，需要明确：仓库是否私有，以及 `raw/` 是否允许纳入 Git。未经确认，不执行 Git 暂存或提交。

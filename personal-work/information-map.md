# Personal Work Information Map

## 1. Purpose

本文件用于说明 `personal-work/` 承接哪些非项目类个人工作信息，以及 AI 在不同任务中应优先读取哪些区域。

本文件是信息分类地图，不是事实源，不替代 source、brief、pending 或 decisions。

## 2. Information Categories

| 信息类型 | 内容说明 | 建议位置 | AI 调用场景 |
|---|---|---|---|
| 公司结构 | 公司、部门、组织关系等相对稳定信息 | `personal-work/briefs/` 或后续按需建立单一事实页 | 汇报、会议准备、组织背景理解 |
| 团队人员 | 成员职责、Owner 分工、协作边界 | `personal-work/briefs/`、`personal-work/decisions.md` | 管理判断、绩效、协作复盘 |
| 部门方向 | 阶段方向、管理口径、职责边界变化 | `personal-work/decisions.md`、`personal-work/briefs/` | 周报、月报、阶段汇报、向上同步 |
| 日报 / 周报 / 月报 | 周期性工作记录与阶段总结 | `personal-work/sources/`、`personal-work/briefs/` | 日报、周报、月报生成 |
| 会议纪要 | 会议结论、待跟进事项、协作问题 | `personal-work/sources/`、`personal-work/briefs/`、`personal-work/pending.md` | 会议准备、会后跟进、复盘 |
| 管理判断 | 已形成的非项目类稳定判断 | `personal-work/decisions.md` | AI 输出前提、汇报口径、管理复盘 |
| AI 工作流 | Knowledge Vault、Claude、GPT、Cursor、Codex 协作方式 | `methods/`、`prompts/`、`personal-work/briefs/` | 方法复用、AI 协作、流程治理 |
| 跨项目协作 | 非单一项目的协作问题、资源问题、责任边界 | `personal-work/sources/`、`personal-work/briefs/`、`personal-work/pending.md`、`personal-work/decisions.md` | 协作复盘、向上反馈 |
| 项目信息 | 具体项目事实、页面、业务口径、项目 pending / decisions | `projects/{project}/` | 项目交接、页面更新、业务判断 |

## 3. Reading Rules for AI

AI 处理 personal-work 任务时，应优先判断任务类型：

### 3.1 汇报 / 日报 / 周报 / 月报

优先读取：

1. `README.md`
2. `index.md`
3. `workspace-brief.md`
4. `personal-work/information-map.md`
5. `personal-work/decisions.md`
6. `personal-work/pending.md`
7. 与本次主题相关的 `personal-work/briefs/` 或 `personal-work/sources/`
8. 必要时调用 `prompts/report-input-template.md`
9. 必要时调用 `prompts/daily-report-from-vault.md`

### 3.2 历史材料归位

优先读取：

1. `personal-work/information-map.md`
2. `inbox/README.md`
3. `prompts/historical-material-intake.md`

然后判断材料进入：

- `personal-work/sources/`
- `personal-work/briefs/`
- `personal-work/pending.md`
- `personal-work/decisions.md`
- `projects/{project}/`
- `methods/`
- `prompts/`
- `inbox/`

### 3.3 项目相关任务

如果材料明确属于具体项目，应进入：

- `projects/{project}/`

不要默认进入 `personal-work/`。

例如 BOMCASE 页面、业务、项目 pending、项目 decisions，应优先进入：

- `projects/bomcase/`

### 3.4 管理判断类任务

如果材料属于非单一项目的管理判断、部门方向、团队协作或个人工作复盘，应优先进入：

- `personal-work/decisions.md`
- `personal-work/briefs/`
- `personal-work/pending.md`

但只有已形成稳定判断时，才进入 `decisions.md`。

## 4. Boundaries

- 本文件不是事实源；
- 本文件不替代 `source`；
- 本文件不替代 `brief`；
- 本文件不替代 `pending`；
- 本文件不替代 `decisions`；
- 本文件不承接具体项目事实；
- BOMCASE 项目资料不默认进入 `personal-work/`；
- `prompts/` 只作为工具，不承载业务事实；
- `index.md` 仍只作为导航索引，不作为全量文件清单。

## 5. Current Stage

当前 personal-work 仍处于最小承接结构阶段。

已具备：

- `sources/`
- `briefs/`
- `pending.md`
- `decisions.md`

尚未根据真实材料密度拆分：

- `reports/`
- `meetings/`
- `management/`
- `performance/`
- `ai-workflow/`

是否拆分上述目录，应在多份真实材料沉淀后再判断。

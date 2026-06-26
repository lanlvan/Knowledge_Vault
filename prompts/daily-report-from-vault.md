# Daily Report From Vault Prompt

## 1. Purpose

用于基于 Knowledge Vault 生成日报、阶段汇报或轻量工作同步内容。

本 prompt 的目标不是重新整理知识库，而是在执行具体输出任务时，明确 AI 应读取哪些文件、如何使用 decisions、如何处理 pending 和历史材料有效性。

## 2. Required Reading Order

执行本 prompt 前，AI 应按以下顺序读取：

1. `README.md`
2. `index.md`
3. `workspace-brief.md`
4. `personal-work/information-map.md`
5. `personal-work/decisions.md`
6. `personal-work/pending.md`
7. `projects/bomcase/decisions.md`
8. `projects/bomcase/pending.md`
9. 与本次日报 / 汇报主题相关的 brief 或 source

## 3. Reading Rules

- `README.md` / `index.md` / `workspace-brief.md` 只作为导航与背景，不作为业务事实源。
- `decisions.md` 中 active 或进行中的判断，可作为当前输出前提。
- `pending.md` 只能作为待确认信息，不得写成已确定结论。
- `sources/` 是原始材料，不等于当前有效口径。
- 历史材料必须识别有效性状态：
  - `active`：可作为当前依据；
  - `expired`：仅作历史参考；
  - `superseded`：默认不作为当前口径；
  - `uncertain`：只能作为待确认内容。
- 如果 source 存在对应 `.correction.md`，应以 correction 中的 Corrected Understanding 为准。
- `prompts/` 只作为工具，不承载业务事实。

## 4. Task Scope Selection

按任务类型裁剪读取范围，避免无关信息干扰：

- 纯 personal-work 汇报：
  - 先读取 `personal-work/information-map.md`，判断信息分类与读取路径；
  - 优先读取 `personal-work/decisions.md`、`personal-work/pending.md`；
  - 按主题读取相关 `personal-work/briefs/` 或 `personal-work/sources/`；
  - BOMCASE 内容默认降权，除非用户明确要求或主题涉及 BOMCASE。
- BOMCASE 项目汇报：
  - 读取 `projects/bomcase/decisions.md`、`projects/bomcase/pending.md`；
  - 按主题读取相关 BOMCASE brief/source；
  - 相关 personal-work decision 只作为背景，不替代项目事实。
- 综合汇报：
  - 同时读取 `personal-work/decisions.md` 与 `projects/bomcase/decisions.md`；
  - 同时读取两侧 pending；
  - 按主题读取双方相关 brief/source。

## 5. Minimum Input Gate

生成日报 / 汇报前，至少需要用户提供：

- 输出类型；
- 时间范围；
- 重点主题。

如缺少上述信息，AI 应先要求用户补充，不直接生成正式正文。

## 6. Status Filter Checklist

默认纳入：

- `active`
- `进行中`

默认排除为当前事实：

- `expired`
- `superseded`
- `uncertain`

处理规则：

- `expired` 仅作为历史参考；
- `superseded` 默认不作为当前口径；
- `uncertain` 只能作为待确认；
- 如用户明确要求回顾历史，可引用 `expired` / `superseded`，但必须标注其历史状态。

## 7. Pre-Execution Checklist

- 是否已明确输出类型；
- 是否已明确时间范围；
- 是否已明确重点主题；
- 是否已判断任务类型：personal-work / BOMCASE / 综合；
- 是否已读取对应 decisions；
- 是否已检查 pending；
- 是否存在需要读取的 brief/source；
- 是否存在 correction；
- 是否已过滤 `expired` / `superseded` / `uncertain`；
- 是否存在不能确认但需要标注的内容。

## 8. Task Input

使用时由用户补充：

```text
本次输出类型：
日报 / 周报 / 月报 / 阶段汇报 / 会议准备 / 其他

本次时间范围：

本次重点主题：

需要特别关注的项目：

需要特别关注的个人工作判断：

需要规避的表达：
```

## 9. Output Requirements

输出时应区分：

- 今日 / 本阶段已完成事项；
- 当前推进中事项；
- 待确认问题；
- 风险或卡点；
- 需要同步或向上反馈的内容；
- 可沉淀到 Knowledge Vault 的新判断。

## 10. Constraints

- 不补充文件中没有的信息；
- 不把 pending 写成已确认；
- 不把 expired / superseded 当当前事实；
- 不把 BOMCASE 项目判断扩展成全部个人工作判断；
- 不把 personal-work 判断误写成 BOMCASE 项目事实；
- 不生成新的项目规则；
- 不改写 source；
- 不替用户自动做最终管理判断。

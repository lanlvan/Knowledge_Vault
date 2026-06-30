---
project: bomcase
type: spec
status: active
version: v0.3
updated: 2026-06-30
scope: unified_schema_v1_information_layer_extension
---

# BOMCASE Source / Brief Object Spec

## 0. Spec Scope

本规范是 BOMCASE Source / Brief Object Spec v0.3，当前用于维护 page brief / active source 的 Unified Schema v1 统一骨架，并扩展 source 信息层读取规范。

本规范约束的是统一章节结构、统一事实边界、统一读取路径；不约束页面颗粒度、字段数量、表格列结构、表达密度。

本规范不新增页面产品事实，不替代 `pending.md`、`decisions.md`、`delivery-output-handoff.md`。

## 1. Current Object Model and Facts

当前事实模型如下：

```text
page brief
→ active_source
→ active source
+ pending.md
+ decisions.md
→ Delivery Output
```

当前已落地状态：

* 5 个 page brief 已统一为 8 段骨架；
* 5 个 active source 已统一为 11 段骨架；
* Open Box 不作为结构例外，只作为高复杂度样本；
* Open Box `source_type` 仍为 `consolidated_source`；
* Home / Shop / Open Box Result / Toy Collection `source_type` 仍为 `handoff_document`；
* page brief 是摘要入口；
* active source 是事实主载体。

## 2. Fact Boundaries

事实边界定义如下：

* `pending.md` 是唯一未确认事实池；
* `decisions.md` 是稳定项目判断池；
* outputs / drafts / archive 不作为当前事实源；
* Delivery Output 读取事实必须遵循 `page brief -> active source -> pending.md -> decisions.md`；
* 不允许 brief 固化 pending 明细；
* 不允许 source 消化 pending 为确定规则；
* 不允许将 source 扩展为完整后端系统规则库。

## 3. Page Brief Frontmatter Minimum

page brief 最小 frontmatter 字段如下：

```yaml
project:
type: page_brief
status:
knowledge_role:
active_source:
updated:
```

约束：

* page brief 必须使用 `active_source`，不得回退旧 `source` 字段；
* `active_source` 必须指向唯一 active source；
* `knowledge_role` 当前最小集合为 `fact-brief` / `handoff-brief`。

## 4. Source Frontmatter Minimum

source 最小 frontmatter 字段如下：

```yaml
project:
page:
type: source
status: active
role: detailed_fact_source
source_type:
version: current
updated:
```

约束：

* `source_type` 当前允许 `consolidated_source` / `handoff_document`；
* `source_history` 为条件字段，不是所有 source 必填。

## 5. Unified Schema v1: Page Brief 8 Sections

5 个 page brief 必须采用以下一级章节：

```markdown
## 1. Source Policy
## 2. Page Objective
## 3. Page Structure Summary
## 4. Key Product Logic
## 5. Pending Awareness
## 6. Decision Boundary
## 7. Non-goals
## 8. Maintenance Notes
```

章节职责：

* `Source Policy`：声明 active source 与读取边界；
* `Page Objective`：页面目标摘要；
* `Page Structure Summary`：页面结构摘要；
* `Key Product Logic`：关键规则摘要，不替代 source 表格层；
* `Pending Awareness`：仅承接 pending 编号与影响，不写明细答案；
* `Decision Boundary`：承接已确认 decisions 边界；
* `Non-goals`：明确不覆盖范围；
* `Maintenance Notes`：维护说明与变更记录摘要。

## 6. Unified Schema v1: Active Source 11 Sections

5 个 active source 必须采用以下一级章节：

```markdown
## 1. Source Scope
## 2. Page Goal
## 3. Structure
## 4. Data / Fields
## 5. States
## 6. Interactions
## 7. Rules
## 8. Acceptance Criteria
## 9. Pending Boundary
## 10. Non-goals
## 11. Maintenance Log
```

章节职责：

* `Source Scope`：source 身份、事实范围与读取边界；
* `Page Goal`：页面目标与范围；
* `Structure`：页面结构与模块关系；
* `Data / Fields`：字段与用户可见信息项；
* `States`：状态与状态差异；
* `Interactions`：触发条件、动作与结果；
* `Rules`：跨模块规则与约束；
* `Acceptance Criteria`：可直接转测试的验收口径；
* `Pending Boundary`：未确认边界承接，不确认为事实；
* `Non-goals`：明确不覆盖内容；
* `Maintenance Log`：维护记录，不承载业务正文。

## 7. Structure vs Granularity

Unified Schema v1 的统一对象是结构，不是颗粒度：

* 允许页面复杂度差异；
* 允许字段数量差异；
* 允许业务特有子节差异；
* 不要求其它页面补到 Open Box 同等颗粒度；
* 不允许因页面复杂度差异破坏一级章节骨架、共通对象命名与事实边界。

## 8. v0.3 Information Layer Extension

### 8.1 Change Purpose

v0.3 新增信息层治理，用于处理 active source 中 F / E / Acceptance 混写的问题。

本次 v0.3：

* 只扩展读取规范；
* 不改变 source / brief 对象关系；
* 不改变 active_source 指向规则；
* 不改变 active source 11 段骨架；
* 不属于文件结构重构。

通过 `section_layer` 标注，可以明确每个章节的主要读取用途，降低 Delivery Output 把验收复述误判为新增事实、或把表达文案误判为业务规则的风险。

`section_layer` 只作为读取索引，不改变原有事实内容，不替代人工判断。

### 8.2 Layer Definitions

| Layer | Name | Definition | Deletion Impact |
|---|---|---|---|
| F | Fact / 产品事实层 | 定义产品结构、字段、规则、计算、触发条件、业务边界、跨页关系、pending / decision 承接。 | 删除后会改变产品定义。 |
| E | Expression / 表达层 | 定义用户可见文案、展示状态、视觉表达、hover / info / 按钮 / 状态 / 汇总文案、区域内小粒度呈现。 | 删除后产品定义不变，但 UI 表达受影响。 |
| F+E | 事实与表达混合 | 同一章节同时包含原创事实规则与原创表达内容；读取时必须局部拆分。 | 删除后同时影响产品定义和表达完整性。 |
| A:view | Acceptance / 验收视图 | 不引入新事实，只把已有 F / E 转成研发、UI、测试、Delivery Output 可验证的检查口径。 | 删除后不改变产品事实，但削弱验证能力。 |
| Unknown | 暂无法判断 | 临时标记；需要人工确认，不得作为 Delivery Output / handoff / Change Note 的确定事实读取依据。 | 不得自动使用。 |

### 8.3 section_layer Annotation Rule

* `section_layer` 只允许标在 `##` 或 `###` 标题下。
* 不允许插入普通段落中。
* 每个 `section_layer` 必须配套 `layer_note`。
* 同一标题下只能有一个 `section_layer`。
* `section_layer` 不改变事实内容。
* `section_layer` 不是事实源，只是读取索引。
* `section_layer` 错误时必须人工修正，不能自动推断覆盖。

示例：

```markdown
## 4. Data / Fields
<!-- section_layer: F+E -->
<!-- layer_note: 字段关系为 F，用户可见字段值和文案为 E。 -->
```

### 8.4 A:view Rule

Acceptance Criteria 默认应标为 `A:view`。

`A:view` 不引入新事实，只允许复述 F / E，并把它们转成可检查口径。`A:view` 不得作为事实修订依据，不得反向覆盖 F / E。

如果 `A:view` 与 F / E 不一致，以 F / E 为准，并标记治理风险或人工确认。如果 `A:view` 中出现 source 其它 F / E 章节没有的新规则，也必须标记为治理风险。

Delivery Output 不应优先从 `A:view` 读取事实；`stage-check` 可以使用 `A:view` 检查 F / E 覆盖度。

### 8.5 F+E Reading Rule

`F+E` 章节读取时必须局部拆分，不允许整章整体当 F，也不允许整章整体当 E。

* 规则、字段、触发条件、计算、业务边界、跨页关系，按 F 读取。
* 用户可见文案、展示状态、视觉表达、hover / info / 按钮 / 状态 / 汇总文案，按 E 读取。
* 如果局部内容无法拆分，标记人工确认。
* Delivery Output 使用 `F+E` 章节时，必须在输出中保持事实与表达的用途区别。

### 8.6 Unknown Rule

`Unknown` 只能作为临时标记。

`Unknown` 可用于两类场景：

1. 暂无法判断的信息；
2. 当前 F / E / A:view 值域无法准确覆盖的治理元信息或阅读导引。

进入 Delivery Output / handoff / Change Note 前，`Unknown` 必须人工确认。`Unknown` 不得作为确定事实读取，也不得自动推断为 F、E、F+E 或 A:view。

stage-check 必须列出 `Unknown` 章节。

如果 `Unknown` 章节影响事实更新、交付输出或 pending closure，必须人工确认。

如果某章节长期保持 `Unknown`，source structure governance 应优先安排人工复核。

### 8.7 Reading Path Rule

| Task | F | E | F+E | A:view | Unknown |
|---|---|---|---|---|---|
| Delivery Output handoff | 优先读取 | 按需读取 | 必须局部拆分读取 | 仅作校验，不作事实修订依据 | 禁止确定读取，需人工确认 |
| Delivery Output Change Note | 优先读取 | 按需读取 | 必须局部拆分读取 | 仅作影响检查，不反向覆盖 F/E | 禁止确定读取，需人工确认 |
| stage-check | 读取 | 读取 | 拆分读取 | 优先用于检查覆盖度 | 标记人工确认 |
| page-fact-update-loop | 优先更新 | 影响表达时更新 | 拆分维护 | 不作为新增事实来源 | 暂停自动更新 |
| pending-update-loop | 优先读取 | 一般不读取 | 只读取事实部分 | 不作为 pending 事实来源 | 人工确认 |
| source structure governance | 读取结构用途 | 读取表达密度 | 重点治理对象 | 检查复述风险 | 人工确认 |

### 8.8 Redundancy Judgment Rule

* F 在 `A:view` 中复述，不算事实冗余。
* E 在 `A:view` 中复述，不算表达冗余。
* F 在多个 F 章节中出现不同口径，才算事实冲突。
* E 在多个 E / F+E 章节中出现不同文案，才算表达冲突。
* `A:view` 出现未被 F/E 支撑的新内容，算治理风险。
* `A:view` 与 F/E 不一致时，以 F/E 为准，并标记治理风险或人工确认。

### 8.9 Patch Rules

* `section_layer` 只能新增在标题下方。
* 每个 `section_layer` 必须配套 `layer_note`。
* 同一标题下只能有一个 `section_layer`。
* 不得修改原有标题文本和标题层级。
* 本次 patch 只允许标注，不允许重组、删减、合并正文。
* `A:view` 不得新增产品事实。
* `Unknown` 不得被 Delivery Output 当作确定事实读取。

## 9. v0.1 Relationship

版本关系如下：

* v0.1 是最小对象规范；
* v0.2 supersedes v0.1；
* v0.3 supersedes v0.2；
* v0.2 反映 2026-06-28 已落地的 Unified Schema v1；
* v0.3 在 v0.2 的 Unified Schema v1 统一骨架基础上，新增信息层读取规范扩展；
* v0.1 / v0.2 历史语义保留用于追溯，但当前维护以 v0.3 为准。

## 10. Non-goals

v0.3 不处理：

* 新增页面产品事实；
* 新增 pending 或确认 pending；
* 新增 decisions 结论（由 `decisions.md` 维护）；
* source_type 改型；
* source / brief 对象关系改型；
* active_source 指向规则改型；
* active source 11 段骨架改型；
* 文件结构重构；
* 把 outputs / drafts / archive 作为事实源；
* 把 Delivery Output prompt 正文改写进本 spec。

## Change Log

2026-06-28 | v0.1_initial | Created minimum object spec for BOMCASE page brief and active source maintenance. No existing fact layer files changed.
2026-06-28 | v0.2_unified_schema_v1 | Upgraded to active Unified Schema v1 maintenance spec with fixed 8-section brief and 11-section source skeleton, boundary rules, and v0.1 supersede relation.
2026-06-30 | v0.3_information_layer_extension | Added information layer reading rules for section_layer, A:view, F+E local reading, Unknown handling, reading path, redundancy judgment, and patch boundaries. No source, page brief, pending, decisions, active_source, or Delivery Output rules changed.

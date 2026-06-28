---
project: bomcase
type: spec
status: active
version: v0.2
updated: 2026-06-28
scope: unified_schema_v1
---

# BOMCASE Source / Brief Object Spec

## 0. Spec Scope

本规范是 BOMCASE Source / Brief Object Spec v0.2，当前用于维护 page brief / active source 的 Unified Schema v1 统一骨架。

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

## 8. v0.1 Relationship

版本关系如下：

* v0.1 是最小对象规范；
* v0.2 supersedes v0.1；
* v0.2 反映 2026-06-28 已落地的 Unified Schema v1；
* v0.1 历史语义保留用于追溯，但当前维护以 v0.2 为准。

## 9. Non-goals

v0.2 不处理：

* 新增页面产品事实；
* 新增 pending 或确认 pending；
* 新增 decisions 结论（由 `decisions.md` 维护）；
* source_type 改型；
* 把 outputs / drafts / archive 作为事实源；
* 把 Delivery Output prompt 正文改写进本 spec。

## Change Log

2026-06-28 | v0.1_initial | Created minimum object spec for BOMCASE page brief and active source maintenance. No existing fact layer files changed.
2026-06-28 | v0.2_unified_schema_v1 | Upgraded to active Unified Schema v1 maintenance spec with fixed 8-section brief and 11-section source skeleton, boundary rules, and v0.1 supersede relation.

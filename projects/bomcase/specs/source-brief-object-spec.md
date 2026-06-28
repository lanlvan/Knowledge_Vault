---
project: bomcase
type: spec
status: draft
version: v0.1
updated: 2026-06-28
scope: source_brief_object_spec
---

# BOMCASE Source / Brief Object Spec

## 0. Spec Scope

本规范是 BOMCASE Source / Brief Object Spec v0.1 最小草案。

本规范适用于 BOMCASE 当前 page brief 与 active source 的最小对象结构，只固化当前已经实际跑通的最小对象规则，用于降低后续维护 page brief / source 时的结构漂移风险。

本规范只约束维护对象的最低一致性，不是完整工程规范，不定义完整业务规则，不作为 Delivery Output 的事实源。

本规范不替代 `delivery-output-handoff.md`，不替代 `stage-check.md`，不改变 Loop 2 / Delivery Output 的事实读取链路。

本规范不触发 source 重命名，不要求历史 source 立即补正文。

## 1. Current Object Model

当前已经跑通的最小对象模型为：

```text
page brief
→ active_source
→ active source
+ pending.md
+ decisions.md
→ Delivery Output
```

page brief 负责页面摘要、页面表达压缩视图与 `active_source` 指针。

active source 负责页面详细事实，是页面事实核对的主要载体。

`pending.md` 负责待确认明细集中管理。

`decisions.md` 负责项目级稳定判断。

outputs / drafts 不反向作为事实源，archive 仅用于人工历史回溯，不参与当前 Delivery Output 事实读取。

## 2. Page Brief Frontmatter Minimum

page brief 当前最小 frontmatter 字段为：

```yaml
project:
type: page_brief
status:
knowledge_role:
active_source:
updated:
```

page brief 必须使用 `active_source`，不得回退到旧 `source` 字段。

`active_source` 必须指向当前页面唯一 active source。

`knowledge_role` 当前允许至少包括：

* `fact-brief`
* `handoff-brief`

v0.1 不扩展更多 role。

## 3. Source Frontmatter Minimum

source 当前最小 frontmatter 字段为：

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

`source_type` 当前允许至少包括：

* `consolidated_source`
* `handoff_document`

`source_history` 为条件字段，不是所有 source 的必填字段。

当 source 发生合并、吸收、替代、重命名等历史事件时，才考虑使用 `source_history`。

历史来源不应只依赖文件名表达，应优先放入 frontmatter、`source_history` 或 Maintenance Log。

## 4. Brief Role Boundary

`fact-brief` 用于已经完成较高事实收敛度的页面 brief。

`handoff-brief` 用于仍以交接文档事实承接为主的页面 brief。

当前 Open Box 是 `fact-brief`。

当前 Home / Shop / Open Box Result / Toy Collection 是 `handoff-brief`。

本规范不要求所有页面立即升级为 `fact-brief`。

`handoff-brief → fact-brief` 的升级条件留到 v0.2 或独立任务，不在 v0.1 拍板。

## 5. Source Content Minimum

成熟 source 推荐覆盖：

* 页面目标；
* 页面结构；
* 字段 / 信息项；
* 状态；
* 交互；
* 验收口径；
* 不覆盖范围；
* Maintenance Log。

v0.1 不要求历史 source 立即补齐所有章节。

不得把 Open Box 的全部章节强制复制到其它页面。

页面特有结构由页面业务决定。

当前只要求后续新增或大改 source 时，优先向该结构靠拢。

## 6. Page Brief Content Minimum

page brief 推荐保留：

* 页面定位 / 页面目标摘要；
* active source 指针；
* 当前确认事实摘要；
* 与 `pending.md` 的承接关系；
* 与 `decisions.md` 的相关边界；
* 不覆盖范围或后续补充边界，如已有。

page brief 不应维护完整字段表。

page brief 不应维护完整状态表。

page brief 不应维护完整交互表。

page brief 不应重复维护 pending 明细。

## 7. Pending / To-be-confirmed Boundary

`pending.md` 是唯一 pending 明细维护池。

page brief 只允许保留 pending 承接说明，不维护 pending 明细。

source 不维护 pending 明细。

`project-brief.md` 只维护 pending 概况，不维护 pending 明细。

source 中可以保留“待补充边界”或“不覆盖范围”，但不得把它等同于 pending 明细。

pending 不应由 Delivery Output 自动反向写入事实层。

## 8. Maintenance Log Minimum

Maintenance Log 当前最小格式为：

```text
YYYY-MM-DD | change_type | summary
```

Maintenance Log 记录 source / spec 的维护行为。

Maintenance Log 不用于承载业务规则正文，不替代 `updated` 字段。

`updated` 表示业务事实更新时间。

Maintenance Log 可以记录元数据迁移、结构整理、事实补充等。

`change_type` 暂不锁定完整枚举，只要求短标签。

## 9. v0.1 Non-goals

v0.1 不处理：

* source 文件重命名；
* archive 命名规范；
* draft output 命名规范；
* formal output 命名规范；
* 完整术语统一表；
* 字段表 / 状态表 / 交互表 / 验收表的完整列结构；
* source 正文章节强制顺序；
* 所有 source 立即补正文；
* `consolidated_source` 与 `handoff_document` 的最终升级路径；
* 完整规范变更流程。

## 10. v0.1 → v0.2 Upgrade Triggers

出现以下任一情况时，应考虑进入 v0.2 或拆分独立规范任务：

* 新增第 6 个 active source；
* 第 3 个非 Open Box 页面跑通 Delivery Output；
* 任一 source 出现 v0.1 无法分类的新章节结构；
* 任一 page brief 出现 v0.1 无法描述的新 frontmatter 字段；
* 跨页面术语漂移影响 Delivery Output 正确性；
* 准备执行 source 重命名；
* 准备系统性补齐 4 个 handoff source 正文颗粒度。

## Change Log

2026-06-28 | v0.1_initial | Created minimum object spec for BOMCASE page brief and active source maintenance. No existing fact layer files changed.

---
project: bomcase
type: page_brief
status: current
knowledge_role: handoff-brief
active_source: ../sources/toy-collection.md
updated: 2026-06-28
---

# Toy Collection Page Brief

## 1. Source Policy

* 本 brief 是潮玩图鉴摘要入口，不替代 `../sources/toy-collection.md`。
* 页面事实、文案、字段、状态、交互、验收以 active source 为准。
* pending 只在 `pending.md` 维护，brief 仅做编号和影响范围承接。

## 2. Page Objective

潮玩图鉴页用于展示收藏进度、SSR 统计、分类/系列/拥有状态筛选，以及系列卡组与单卡状态浏览。

## 3. Page Structure Summary

* 顶部导航与全站统计区；
* 分类 Tab 与筛选区（分类 / 系列 / 拥有状态）；
* 系列卡组列表与单卡列表；
* 集齐兑换占位区（未开放）；
* 卡组空状态入口。

## 4. Key Product Logic

* 顶部 SSR 统计与筛选区分层，统计不因筛选变化而直接改口径。
* 收藏完成度展示为整数百分比，但取整规则不固定。
* 单卡状态与筛选对象保持在“单卡层”表达，不固化跨模块语义边界。
* 页面保留 `xN` 单卡数量与隐藏款、全站唯一 SSR 等用户可见文案口径。
* 集齐兑换当前未开放且不可点击；空状态保留“去商城看看”入口。
* 不新增 loading / error / empty / reset 规则。

## 5. Pending Awareness

* `TC-A001`：收藏完成度整数百分比取整规则待确认。
* `TC-B005`：单卡状态语义边界待确认。
* `TC-B006`：分类与系列筛选联动关系待确认。
* `TC-B007`：拥有状态与分类 / 系列筛选联动关系待确认。
* 确认前不固定上述 4 项答案，不把 pending 写成事实。

## 6. Decision Boundary

* 承接 `BOM-D007`：本页为 `handoff-brief`，只做交接摘要。
* 承接 `BOM-D010`：截图仅示意，验收以 source 与确认口径为准。

## 7. Non-goals

* 不覆盖完整资产、交易、兑换、养成、背包系统规则。
* 不补充导航消息、库存、弹窗等已有能力内部规则。
* 不确认 pending 细项答案，不扩写未确认异常恢复流程。

## 8. Maintenance Notes

* brief 仅维护摘要索引与边界，完整字段/状态/交互/验收保持在 source。
* 如筛选联动或完成度取整口径确认，先更新 source 与 pending，再回写 brief。
* 2026-06-28 | schema_migration | Migrated brief structure to BOMCASE Unified Schema v1 without changing product facts.

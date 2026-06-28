---
project: bomcase
type: page_brief
status: current
knowledge_role: handoff-brief
active_source: ../sources/open-box-result.md
updated: 2026-06-28
---

# Open Box Result Page Brief

## 1. Source Policy

* 本 brief 为结果页摘要入口，不替代 `../sources/open-box-result.md`。
* 页面事实、文案、字段、状态、交互、验收以 active source 为准。
* `pending.md` 与 `decisions.md` 仅做边界承接，不在 brief 内转写为新事实。

## 2. Page Objective

结果页用于承接开箱结算后的结果反馈，以正常掉落为主，并补充保底反馈与水晶沉淀提示。

## 3. Page Structure Summary

* 顶部标题与保底反馈；
* 正常掉落饰品区；
* 保底奖励区（条件展示）；
* 底部按钮区；
* 水晶能量沉淀提示（条件展示）。

## 4. Key Product Logic

* 正常掉落为主，保底奖励不作为第 6 张普通掉落卡片。
* 保底奖励仅在触发保底并额外发放奖励时展示，且需有到账感知。
* 到账感知只约束结果表达目标，不固化具体 UI / 动效实现。
* 水晶提示只表达本次沉淀结果，不扩展完整资源总览。
* 结果页展示以后端最终结算结果为准。
* 不处理 “能量余额 / 水晶 / 水晶能量” 的跨页术语关系。

## 5. Pending Awareness

* 本页当前无独立 pending 编号。
* 结果态细节实现边界保留在 source 的待补充范围，不在 brief 中确认新答案。

## 6. Decision Boundary

* 承接 `BOM-D007`：本页为 `handoff-brief`，不替代 source 事实层。
* 承接 `BOM-D010`：截图示意不覆盖规则，验收按 source 与已确认口径执行。

## 7. Non-goals

* 不扩展完整保底计算、批量结算、资产入账、钱包、交易、发货等系统规则。
* 不扩展正常掉落卡片既有详细规则。
* 不把待补充实现细节写成确定规则。

## 8. Maintenance Notes

* brief 仅维护摘要、边界与读取路径；完整字段/状态/交互/验收留在 source。
* 若顶部反馈、保底奖励区或水晶提示口径变化，先更新 source 再回写 brief。
* 2026-06-28 | schema_migration | Migrated brief structure to BOMCASE Unified Schema v1 without changing product facts.

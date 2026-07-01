---
project: bomcase
type: page_brief
status: current
knowledge_role: handoff-brief
active_source: ../sources/open-box-result.md
updated: 2026-07-01
---

# Open Box Result Page Brief

## 1. Source Policy

* 本 brief 为结果页摘要入口，不替代 `../sources/open-box-result.md`。
* 页面事实、文案、字段、状态、交互、验收以 active source 为准。
* `pending.md` 与 `decisions.md` 仅做边界承接，不在 brief 内转写为新事实。

## 2. Page Objective

结果页用于承接开箱结算后的结果反馈，以本次实际获得饰品为主，并补充最终保底状态与水晶沉淀提示。

## 3. Page Structure Summary

* 顶部标题与保底反馈；
* 本次获得饰品区；
* 底部按钮区；
* 水晶能量沉淀提示（条件展示）。

## 4. Key Product Logic

* 本次获得饰品区展示本次结算后用户实际获得的全部饰品，包括正常开箱掉落饰品与触发保底后额外发放的保底奖励饰品。
* 保底奖励饰品不单独展示为独立奖励区域，不固定置顶、置尾或独立抽出展示，最终顺序以后端返回的结算顺序为准。
* 仅触发保底后由系统额外发放的保底奖励饰品展示“保底奖励”标识；自然获得焦点区卡牌不展示该标识。
* 顶部保底反馈只展示本次结算后的最新 / 最高优先级状态。
* 水晶提示只表达本次沉淀结果，不扩展完整资源总览。
* 结果页展示以后端最终结算结果为准，不重新定义 Open Box 页面保底计算规则。
* 不处理“能量余额 / 水晶 / 水晶能量”的跨页术语关系。

## 5. Pending Awareness

* 本页当前无独立 pending 编号。
* 本轮确认删除独立奖励区域，因此不保留该区域到账感知待补充项。
* 设计实现细节、接口字段和后端服务拆分不在本 brief 中确认。

## 6. Decision Boundary

* 承接 `BOM-D007`：本页为 `handoff-brief`，不替代 source 事实层。
* 承接 `BOM-D010`：截图示意不覆盖规则，验收按 source 与已确认口径执行。

## 7. Non-goals

* 不扩展完整保底计算、批量结算、资产入账、钱包、交易、发货等系统规则。
* 不扩展饰品卡片既有详细规则。
* 不把待补充实现细节写成确定规则。

## 8. Maintenance Notes

* brief 仅维护摘要、边界与读取路径；完整字段、状态、交互、验收留在 source。
* 若顶部反馈、本次获得饰品区、保底奖励标识或水晶提示口径变化，先更新 source 再回写 brief。
* 2026-07-01 | brief_sync | Synced Open Box Result brief with source change: guarantee reward now merges into backend-ordered acquired ornament list.
* 2026-06-28 | schema_migration | Migrated brief structure to BOMCASE Unified Schema v1 without changing product facts.

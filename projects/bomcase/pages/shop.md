---
project: bomcase
type: page_brief
status: current
knowledge_role: handoff-brief
active_source: ../sources/shop.md
updated: 2026-06-28
---

# Shop Page Brief

## 1. Source Policy

* 本 brief 只做商城页摘要入口，不替代 `../sources/shop.md`。
* 字段、状态、交互、验收与用户可见文案以 active source 为准。
* facts 与边界冲突时，优先回到 active source + `pending.md` + `decisions.md`。

## 2. Page Objective

商城页用于以商品为主体展示购买入口与随商品附赠的军需权益，并承接商品详情和已有下单流程。

## 3. Page Structure Summary

* 顶部说明横幅；
* 分类 / 排序 / 搜索；
* 商品列表与商品卡片；
* 空状态；
* 底部保障区域。

## 4. Key Product Logic

* 页面主语义为商品，不是军需直购。
* 顶部说明横幅保留原文案：`买商品 · 赠军需权益`、`下单赠权益，随商品展示为准`，并保留 `查看规则` 入口。
* 商品卡片保留固定权益与 `3 选 1` 权益两类表达，且存在默认选中与切换选中。
* 商品图 / 标题进入详情，CTA 进入已有下单流程。
* 商品列表、分类 / 排序 / 搜索、空状态与底部保障按 source 既有口径承接。
* 不扩展支付、库存、订单、履约、权益到账、发货规则。

## 5. Pending Awareness

* 本页当前无独立 pending 编号。
* 仅承接项目级 Navigation / 其它页面 pending 的外部影响，不在本 brief 内新增或确认 pending 结论。

## 6. Decision Boundary

* 承接 `BOM-D007`：本页 `handoff-brief` 仅作交接摘要，不替代 source。
* 承接 `BOM-D010`：页面截图示例不覆盖规则正文，验收以 source 事实为准。

## 7. Non-goals

* 不维护完整商品交易规则库。
* 不展开支付、库存、订单、发货、资产、权益、结算系统规则。
* 不替代商品详情页与下单流程内部规则。

## 8. Maintenance Notes

* brief 仅维护摘要、边界与读取路径；完整字段/状态/交互/验收留在 source。
* 后续若横幅文案、权益展示或入口链路变化，应先改 source 再同步 brief。
* 2026-06-28 | schema_migration | Migrated brief structure to BOMCASE Unified Schema v1 without changing product facts.

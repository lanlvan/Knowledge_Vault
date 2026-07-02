---
project: bomcase
type: page_brief
status: current
knowledge_role: fact-brief
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
* 商品列表与商品卡片（商品列表最多展示 2 排，不定义滚动加载、分页或无限列表）；
* 空状态；
* 底部保障区域。

## 4. Key Product Logic

* 页面主语义为商品，不是军需直购。
* 顶部说明横幅保留原文案：`买商品 · 赠军需权益`、`下单赠权益，随商品展示为准`，并保留 `查看规则` 入口。
* 商品图 / 标题进入详情，CTA 进入已有下单流程。
* 分类最多展示 9 个；超出上限由后端限制或控制，brief 不定义分类后台管理规则。
* 商品列表最多展示 2 排；本页不定义滚动加载、分页或无限列表。
* 单商品最多展示 1 个 Tag，brief 不扩展多 Tag 策略。
* 商品卡片保留固定权益与 `3 选 1` 权益两类表达；权益必须始终有默认选中，用户不可取消全部权益，选择结果承接商品详情 / 下单链路，brief 不扩写完整交易规则。
* 当前无划线价、折扣价、会员价；brief 不扩写价格策略、优惠系统或会员价规则。
* 商品列表、分类 / 排序 / 搜索、空状态与底部保障按 source 既有口径承接。
* 不扩展支付、库存、订单、履约、权益到账、发货规则。

## 5. Pending Awareness

* 本页当前无独立 pending 编号。
* 仅承接项目级 Navigation / 其它页面 pending 的外部影响，不在本 brief 内新增或确认 pending 结论。

## 6. Decision Boundary

* 承接 `BOM-D007`：本页已升级为 `fact-brief`，可作为当前页面事实口径层读取，但仍不替代 active source。
* 完整字段、状态、交互、验收与用户可见文案仍以 `../sources/shop.md` 为准。
* 本次角色升级不新增业务规则。
* 承接 `BOM-D010`：页面截图示例不覆盖规则正文，验收以 source 事实为准。

## 7. Non-goals

* 不定义完整交易流程，不维护完整商品交易规则库。
* 不定义支付、库存、订单、发货、资产、权益到账、结算、价格策略系统。
* 不定义商品后台管理规则。
* 不替代商品详情页与下单流程内部规则。

## 8. Maintenance Notes

* brief 仅维护摘要、边界与读取路径；完整字段/状态/交互/验收留在 source。
* 后续若横幅文案、权益展示或入口链路变化，应先改 source 再同步 brief。
* 2026-07-01 | role_upgrade | Upgraded Shop page brief from handoff-brief to fact-brief after role review; no business facts changed.
* 2026-07-01 | brief_sync | Synced Shop brief with core compressed facts from active source: category limit, list display boundary, tag limit, entitlement selection boundary, and price expression exclusions; no business facts changed.
* 2026-06-28 | schema_migration | Migrated brief structure to BOMCASE Unified Schema v1 without changing product facts.

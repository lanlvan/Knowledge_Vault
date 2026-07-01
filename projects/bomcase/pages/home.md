---
project: bomcase
type: page_brief
status: current
knowledge_role: handoff-brief
active_source: ../sources/home.md
updated: 2026-06-29
---

# Home Page Brief

## 1. Source Policy

* 本 brief 是首页摘要入口，不替代 `../sources/home.md`。
* 页面事实、字段、状态、交互与文案以 active source 为准。
* Delivery Output 读取链路保持 `page brief -> active source -> pending -> decisions`。

## 2. Page Objective

首页用于承接活动主视觉、商品入口、军需权益信息和信任说明，支持用户从浏览进入商品详情与下单流程。

## 3. Page Structure Summary

* 顶部全局导航；
* 三栏首屏（左侧热门掉落 / 中部 Banner + 流程 / 右侧权益与说明）；
* 热门商品区（商品卡片、赠品、CTA）；
* 安心购物与底部信任背书（含概率公示入口）。

## 4. Key Product Logic

* Banner 为管理端配置项，Banner 内容全部为图片，最多支持 3 张，支持自动轮播与手动切换。
* Banner 点击行为由管理端配置结果决定，首页侧不固化固定点击枚举。
* Header 使用全局导航能力，不在本页补登录态、头像点击、“我的盒柜”规则。
* 部分导航入口页面映射已确认：Bomcase Logo / Bomcase → Home 页面，商城 → Shop 页面，潮玩图鉴 → Toy Collection 页面；最终 URL 与剩余入口映射仍以 `NAV-B001` 为待确认边界；首页默认导航高亮显示为「Bomcase」。
* 用户可见文案口径保持 source 原文，包括活动与信任表达（如“买实体盲盒送军需权益”“下单后在线拆盒，并获赠军需权益”“100%必得军需权益”“点击查看概率公示”）。

## 5. Pending Awareness

* `NAV-B001`：部分全局导航入口页面映射已确认；最终 URL 与剩余入口页面映射 / 路由目标仍未确认。

## 6. Decision Boundary

* 承接 `BOM-D007`：本页为 `handoff-brief`，用于交接与理解，不替代 source。
* 承接 `BOM-D009`：Banner 点击行为由配置结果驱动，brief 不定义固定行为枚举。
* 承接 `BOM-D010`：截图仅示意，验收以规则与 source 事实为准。

## 7. Non-goals

* 不覆盖支付、库存、订单、发货、资产、权益到账、结算等完整系统规则。
* 不补全全局导航已有能力内部规则。
* 不承接 source 未确认事实，不把 pending 写成已确认事实。

## 8. Maintenance Notes

* 本 brief 只维护首页摘要、读取路径与边界，不维护完整字段表/状态表/交互表。
* 如首页结构或入口关系变更，先更新 active source，再回写本 brief 摘要。
* 2026-06-28 | schema_migration | Migrated brief structure to BOMCASE Unified Schema v1 without changing product facts.

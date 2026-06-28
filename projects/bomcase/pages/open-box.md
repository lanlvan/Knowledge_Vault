---
project: bomcase
type: page_brief
status: current
knowledge_role: fact-brief
active_source: ../sources/open-box.md
updated: 2026-06-28
---

# Open Box Page Brief

## 1. Source Policy

* 本 brief 是 Open Box 事实摘要入口，`../sources/open-box.md` 是唯一 active source。
* Open Box 作为高复杂度 source 保持细颗粒度，brief 不替代 source 详细字段/状态/交互/验收。
* 读取链路保持 `page brief -> active source -> pending -> decisions`，历史 output / archive 不反向作为事实源。

## 2. Page Objective

开箱页用于承接军需开启主流程，核心目标是稳定三栏职责、选卡填充与保底进度表达，并保证结果以后端结算为准。

## 3. Page Structure Summary

* 左侧资源概览；
* 中部主判断与主操作（X1 / X5、满足度、资源构成、CTA）；
* 中部保底进度模块；
* 右侧卡牌背包（半展开摘要态 / 全展开操作态 / 底部固定汇总区）；
* 下方饰品区保底标记与底部掉落信息 Tab（已有边界）。

## 4. Key Product Logic

* Open Box source 颗粒度必须保持，不压缩字段、状态、交互、验收内容。
* 卡牌背包、填充能量、已选卡牌、清除已选、消耗说明保持 active source 口径。
* `溢出 +Y% 存入能量余额` 为已确认表达；溢出值按整数展示，刷新时机与清除规则按 source 已确认口径执行。
* 能量溢出提示只在右侧全展开底部固定汇总区表达，不进入左侧资源概览或中部满足度/资源构成。
* X1 / X5 切换会清空已选卡牌、重算状态，并清空溢出提示。
* 保底模块以前端表达为主，但最终结果以后端返回为准。
* 不处理 Open Box / Open Box Result 跨页术语关系。
* 用户可见文案原文在 source 保持完整保留。

## 5. Pending Awareness

* 当前 `pending.md` 中 Open Box 无独立 pending 编号。
* source 中“待补充项”仅作为 UI / 前端实现与结果态细节边界，不等同 pending 已确认事实。

## 6. Decision Boundary

* 承接 `BOM-D005`：能量溢出提示属于页面展示补充，不构成资源计算规则变更。
* 承接 `BOM-D007`：本页为 `fact-brief`，可作事实口径层，但仍不替代 active source 详细层。
* 承接 `BOM-D010`：截图仅示意，规则与验收以 source 正文为准。

## 7. Non-goals

* 不扩展完整能量计算、资源扣减、资产入账、奖励发放、结算与钱包规则。
* 不展开顶部导航、底部掉落信息等已有功能内部规则。
* 不把待补充边界写成确定规则。

## 8. Maintenance Notes

* 本 brief 仅维护摘要、索引、边界和读取路径；细节维护在 `sources/open-box.md`。
* 若三栏职责、保底进度、选卡交互或能量溢出口径变化，需优先更新 active source。
* 2026-06-28 | schema_migration | Migrated brief structure to BOMCASE Unified Schema v1 without changing product facts.

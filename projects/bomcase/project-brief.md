# BOMCASE Project Brief

## 1. 项目定位

说明：

* BOMCASE 是当前主工作台中的 active 项目；
* 当前工作台用于沉淀页面资料、页面摘要、待确认问题和关键判断；
* 当前优先覆盖页面表达和交接资料，不替代完整业务规则库。

## 2. 当前页面范围

| 页面 | 当前 page brief | 当前 source | status | knowledge_role | 说明 |
|---|---|---|---|---|---|
| home | `pages/home.md` | `sources/home.md` | current | handoff-brief | 当前用于研发交接、页面理解和待确认承接。 |
| shop | `pages/shop.md` | `sources/shop.md` | current | handoff-brief | 当前用于研发交接、页面理解和待确认承接。 |
| open-box | `pages/open-box.md` | `sources/open-box.md` | current | fact-brief | 当前已沉淀为页面事实口径层。 |
| open-box-result | `pages/open-box-result.md` | `sources/open-box-result.md` | current | handoff-brief | 当前用于研发交接、页面理解和待确认承接。 |
| toy-collection | `pages/toy-collection.md` | `sources/toy-collection.md` | current | handoff-brief | 当前用于研发交接、页面理解和待确认承接。 |

## 3. 当前资料状态

* 已迁移 5 个页面 source；
* 已生成 5 个 page brief；
* `pending.md` 已汇总项目级待确认项；
* `decisions.md` 已记录当前工作台迁移和边界判断；
* 已形成 source / page brief / pending / decisions 的基础闭环；
* pages 下文件是当前可读页面层，但按 `knowledge_role` 区分为 `fact-brief` 与 `handoff-brief`；
* 当前仅 `open-box.md` 为 `fact-brief`，其余页面为 `handoff-brief`；
* 当前 facts 以本项目 `sources/` 为准，后续不再依赖 V1 作为 active reference。

## 4. 读取顺序

1. `README.md`；
2. `project-brief.md`；
3. `pending.md`；
4. `decisions.md`；
5. `pages/*.md`；
6. `sources/*.md`。

## 5. 事实源说明

* 本项目 `sources/` 是当前 active source；
* page brief / project brief 是工作摘要，不替代 source；
* pending 是待确认问题池；
* decisions 是关键判断记录；
* README 是导航；
* 不将历史 V1 作为当前 active 依赖路径。

## 6. 页面关系概览

* home：入口与整体承接；
* shop：商品与军需权益展示、购买承接；
* open-box：开箱操作与资源/背包/保底进度表达；
* open-box-result：开箱结果、保底触发反馈、奖励/水晶提示表达；
* toy-collection：潮玩图鉴、统计、筛选、卡组/单卡状态表达。

以上仅描述页面表达关系，不定义完整业务规则。

## 7. 当前待确认概况

基于 `pending.md` 当前汇总:

* 总计:8(A:1 / B:7 / C:0);
* Navigation:4(A:0 / B:4);
* Home:0(A:0 / B:0);
* Shop:0(A:0 / B:0);
* Open Box:0(A:0 / B:0);
* Open Box Result:0(A:0 / B:0);
* Toy Collection:4(A:1 / B:3)。

当前优先关注:

* Navigation:全局导航路由、登录态入口语义与首页默认高亮口径;
* Toy Collection:收藏完成度取整规则、单卡状态语义边界与筛选联动口径。

## 8. 当前关键判断概况

基于 `decisions.md` 的 active 判断可概括为：

* 根级 `decisions.md` 承接工作台级与跨项目通用治理规则；
* `projects/bomcase/decisions.md` 承接 BOMCASE 项目级产品判断；
* 当前 `sources/` 是事实底座；
* pages 下文件是当前可读页面层，page brief 按 `knowledge_role` 区分 `fact-brief` 与 `handoff-brief`；
* `open-box.md` 当前为 `fact-brief`；`home.md`、`shop.md`、`open-box-result.md`、`toy-collection.md` 当前为 `handoff-brief`；
* `handoff-brief` 用于研发交接、页面理解和待确认承接，不等同于事实源，也不替代 `sources/*`；
* 事实争议或核对场景仍回到 `sources/*.md`；
* 页面表达不替代完整业务规则。

## 9. 不覆盖范围

本 brief 明确不覆盖：

* 支付规则；
* 库存规则；
* 发货履约规则；
* 完整资产规则；
* 权益/奖励/结算规则；
* 订单/会员/活动系统规则；
* 背包/交易/兑换/养成系统规则；
* source 未确认事实。

## 10. 后续工作

1. 更新 BOMCASE README 导航；
2. 做当前主工作台全局 stage check；
3. 根据待确认项逐步处理页面迭代；
4. 如涉及完整业务规则，单独确认范围后再沉淀。

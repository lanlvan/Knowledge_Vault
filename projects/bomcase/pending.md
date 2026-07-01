# BOMCASE Pending

## 1. 使用说明

说明：

* 本文件是 BOMCASE 产品待确认问题池；
* 只记录已在 page brief / source / 历史来源中明确出现，且尚未形成产品口径的问题；
* 本文件不记录猜测性问题；
* 本文件不记录设计待办、研发任务、测试用例、项目排期或纯视觉实现细节；
* 已解决的问题应回写对应 page brief 正文，或在形成稳定产品判断后转入 `projects/bomcase/decisions.md`；
* 本文件不是业务规则库。

## 2. 分级规则

A：不确认会阻塞开发启动，或导致实现方向错误。  
B：不阻塞开发启动，但影响产品表达、验收口径或知识一致性。

## 3. 快速索引

* Navigation：1（A:0 / B:1）
* Home：0（A:0 / B:0）
* Shop：0（A:0 / B:0）
* Open Box：0（A:0 / B:0）
* Open Box Result：0（A:0 / B:0）
* Toy Collection：0（A:0 / B:0）

## 4. Navigation

来源：`global-navigation.md`；`pages/home.md`。

### NAV-B001：全局导航入口页面映射与最终 URL 待确认

* 等级：B
* 原问题：各全局导航入口具体路由 URL 尚未明确；当前仅确认部分入口的页面映射。
* 已确认页面映射：Bomcase Logo / Bomcase → Home 页面；商城 → Shop 页面；潮玩图鉴 → Toy Collection 页面。
* 来源文件：`global-navigation.md`；`pages/home.md`
* 当前影响：影响剩余顶部导航入口跳转落地、最终 URL 对齐与跨页面入口一致性。
* 待确认产品口径：各导航入口对应的最终 URL；军需、卡牌图鉴、活动中心、幸运空投、客户端下载、BOM战情室、公平公示、我的盒柜、个人头像的页面映射 / 路由目标。

## 5. Home

来源：`pages/home.md`；`sources/home.md`。

* 暂无明确待确认项。

## 6. Shop

来源：`pages/shop.md`；`sources/shop.md`。

* 暂无明确待确认项。

## 7. Open Box

来源：`pages/open-box.md`；`sources/open-box.md`。

* 暂无明确待确认项。

## 8. Open Box Result

来源：`pages/open-box-result.md`；`sources/open-box-result.md`。

* 暂无明确待确认项。

## 9. Toy Collection

来源：`pages/toy-collection.md`；`sources/toy-collection.md`。

* 暂无明确待确认项。

## 10. 后续处理规则

* 产品确认后，优先更新对应 page brief 正文；
* 如形成稳定项目级产品判断，再转入 `projects/bomcase/decisions.md`；
* 涉及完整业务系统规则的，不直接在 pending 中定规则，应先确认范围；
* 纯视觉、设计、动效、研发、测试、排期事项不进入 Knowledge Vault。

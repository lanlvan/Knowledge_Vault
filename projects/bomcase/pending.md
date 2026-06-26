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

* Navigation：3（A:0 / B:3）
* Home：0（A:0 / B:0）
* Shop：0（A:0 / B:0）
* Open Box：0（A:0 / B:0）
* Open Box Result：0（A:0 / B:0）
* Toy Collection：2（A:1 / B:1）

## 4. Navigation

来源：`global-navigation.md`；`pages/home.md`。

### NAV-B001：全局导航入口路由映射待确认

* 等级：B
* 原问题：各全局导航入口具体路由 URL 尚未明确。
* 来源文件：`global-navigation.md`；`pages/home.md`
* 当前影响：影响顶部导航跳转落地与跨页面入口一致性。
* 待确认产品口径：各导航入口对应的具体路由 URL。

### NAV-B002：个人头像点击行为待确认

* 等级：B
* 原问题：个人头像点击后的行为尚未明确。
* 来源文件：`global-navigation.md`
* 当前影响：影响登录态顶部导航的用户操作路径与验收口径。
* 待确认产品口径：个人头像点击后是进入个人中心、展开菜单，还是触发其它已定义入口。

### NAV-B003：我的盒柜功能范围待确认

* 等级：B
* 原问题：我的盒柜入口承接的功能范围尚未明确。
* 来源文件：`global-navigation.md`
* 当前影响：影响登录态导航入口命名、跳转承接和用户理解。
* 待确认产品口径：我的盒柜入口承接的是实物盒柜、订单盒柜、藏品盒柜，还是其它已定义范围。

## 5. Home

来源：`pages/home.md`；`sources/home-handoff.md`。

* 暂无明确待确认项。

## 6. Shop

来源：`pages/shop.md`；`sources/shop-handoff.md`。

* 暂无明确待确认项。

## 7. Open Box

来源：`pages/open-box.md`；`sources/open-box-handoff.md`；`sources/open-box-handoff-v1.3.md`。

* 暂无明确待确认项。

## 8. Open Box Result

来源：`pages/open-box-result.md`；`sources/open-box-result-handoff.md`。

* 暂无明确待确认项。

## 9. Toy Collection

来源：`pages/toy-collection.md`；`sources/toy-collection-handoff.md`。

### TC-A001：收藏完成度整数百分比取整规则待确认

* 等级：A
* 原问题：收藏完成度分子、分母和整数百分比展示已确认，但取整规则仍未明确。
* 来源文件：`pages/toy-collection.md`
* 当前影响：影响收藏完成度展示一致性和验收口径。
* 待确认产品口径：整数百分比展示时，计算结果应四舍五入、向下取整、向上取整，还是以后端返回值为准。

### TC-B005：单卡状态语义边界待确认

* 等级：B
* 原问题：单卡数量展示格式和状态枚举已确认，但状态语义边界与状态关系未完全明确。
* 来源文件：`pages/toy-collection.md`
* 当前影响：影响单卡状态判定一致性和筛选结果可解释性。
* 待确认产品口径：
  * “已解锁”和“拥有”的语义边界；
  * 用户曾经拥有卡牌、但后续兑换或消耗后，页面应归类为“已解锁但未拥有”，还是仍归类为“拥有”；
  * “隐藏”状态与“未解锁”状态是否互斥，或隐藏款未解锁时是否同时具备两类状态。

## 10. 后续处理规则

* 产品确认后，优先更新对应 page brief 正文；
* 如形成稳定项目级产品判断，再转入 `projects/bomcase/decisions.md`；
* 涉及完整业务系统规则的，不直接在 pending 中定规则，应先确认范围；
* 纯视觉、设计、动效、研发、测试、排期事项不进入 Knowledge Vault。

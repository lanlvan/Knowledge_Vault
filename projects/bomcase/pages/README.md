# BOMCASE Pages

## 1. 说明

说明：

* 本目录存放 BOMCASE 的页面级当前可读文档；
* 每个页面一个 Markdown；
* `pages/*.md` 用于承载当前页面状态、结构、边界与待确认承接信息；
* Delivery Output 生成时先读取 page brief，再读取 page brief 声明的 `active_source`；
* `pages/*.md` 是页面入口，不替代 `../sources/` 的详细事实载体；
* superseded source、archive、old output、draft output、`_drafts/` 不作为当前事实源。

## 2. 当前页面清单

| 页面 | Brief | Active Source | status | knowledge_role | 待确认数量 | 说明 |
|---|---|---|---|---|---:|---|
| home | `home.md` | 以该页面 brief frontmatter 的 `active_source` 为准 | current | handoff-brief | - | 用于研发交接、页面理解和待确认承接。 |
| shop | `shop.md` | 以该页面 brief frontmatter 的 `active_source` 为准 | current | handoff-brief | - | 用于研发交接、页面理解和待确认承接。 |
| open-box | `open-box.md` | `../sources/open-box.md` | current | fact-brief | - | Open Box 当前 page brief 指向 `../sources/open-box.md` 作为 active source。 |
| open-box-result | `open-box-result.md` | 以该页面 brief frontmatter 的 `active_source` 为准 | current | handoff-brief | - | 用于研发交接、页面理解和待确认承接。 |
| toy-collection | `toy-collection.md` | 以该页面 brief frontmatter 的 `active_source` 为准 | current | handoff-brief | - | 用于研发交接、页面理解和待确认承接。 |

待确认数量以 `../pending.md` 当前汇总为准。

### page brief 角色说明

* page brief 不统一等同于事实源；
* `fact-brief`：已治理沉淀，可作为当前页面口径承接层；
* `handoff-brief`：由交接文件压缩形成，用于研发交接、页面理解和待确认承接；
* `handoff-brief` 不替代 source；
* 当前仅 `open-box.md` 为 `fact-brief`，其它页面为 `handoff-brief`；
* 每个页面的详细事实载体以 page brief frontmatter 声明的 `active_source` 为准。

## 3. 推荐读取方式

1. 先读项目级 `../project-brief.md`；
2. 再按页面读取对应 page brief；
3. 如关注待确认问题，读 `../pending.md`；
4. 如关注关键判断，读 `../decisions.md`；
5. 如需要核对事实，读取 page brief 中声明的 `active_source`。

## 4. 页面 brief 使用边界

* `pages/*.md` 是当前可读页面层，但不同文件的知识性质可能不同；
* `pages/*.md` 不替代 `../sources/` 详细事实材料；
* `pages/*.md` 不定义完整业务规则；
* `../pending.md` 是正式产品待确认池，`pages/*.md` 待确认区需与其保持口径一致；
* 页面表达不等于支付、库存、发货、资产、权益、奖励、结算、订单、会员、活动、背包、交易、兑换、养成等完整系统规则；
* 不新增 `../sources/` 未确认事实。

## 5. 页面层与 source 核对关系

* `pages/*.md` 由 active source、`../decisions.md`、`../pending.md` 以及人工确认结果整理形成；
* `handoff-brief` 主要用于研发交接、页面理解和待确认承接，不等同于事实源；
* `fact-brief` 可作为当前页面口径承接层使用；
* 若 `pages/*.md` 与 active source 存在差异，应优先检查是否存在后续 decision / pending / 人工确认记录；
* 事实争议或核对场景统一回到页面声明的 `active_source`。

## 6. 当前状态

* 5 个 page brief 已生成；
* 5 个 page brief 已通过统一只读校验；
* `../pending.md` 已汇总页面待确认项；
* 后续如页面资料变更，应同步更新对应 page brief 和 pending/decisions。

## 7. Page Brief Update Rule

 * `pages/*.md` 是当前可读页面层（按 `knowledge_role` 区分 `fact-brief` 与 `handoff-brief`）；
* 页面 brief 记录当前页面状态、结构、边界以及待确认承接内容；
* 页面变化进入交付文档前，必须先判断是否需要更新对应 page brief；
* 若页面变化形成稳定判断，应同步进入 `../decisions.md`；
* 若页面变化仍未确认，应同步进入 `../pending.md`；
* `../outputs/handoff/` 中的交付文档不得反向覆盖 page brief；
* 如果生成交接文档时发现 page brief 缺失信息，应回到 `Knowledge Update Loop` 先补齐。

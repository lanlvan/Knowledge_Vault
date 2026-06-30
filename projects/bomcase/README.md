# BOMCASE

## 1. 项目入口

说明：

* 当前项目路径为 `F:\Knowledge_Vault\projects\bomcase\`；
* 本目录是 BOMCASE 在 Knowledge_Vault 中的 active 项目工作台；
* 用于查看项目摘要、页面 brief、待确认项、关键判断和 source；
* 当前以本项目 `sources/` 作为原始事实材料核对层，不再依赖历史 V1 路径作为日常回查入口。

## 2. 推荐读取顺序

1. `project-brief.md`：先看项目整体；
2. `pending.md`：查看待确认项；
3. `decisions.md`：查看关键判断与边界；
4. `pages/*.md`：查看页面 brief；
5. 对应 page brief frontmatter 声明的 `active_source`：核对当前页面详细事实。

## 3. 当前文件导航

| 文件/目录 | 用途 | 是否事实源 | 说明 |
|---|---|---|---|
| `project-brief.md` | 项目级摘要 | 否 | 汇总当前范围、状态、页面关系与后续工作。 |
| `pending.md` | 项目级待确认池 | 否 | 正式产品待确认入口，按页面汇总待确认项与优先级建议。 |
| `decisions.md` | 项目级判断记录 | 否 | 记录已形成的关键判断、边界与取舍。 |
| `pages/` | 当前可读页面层 | 否（不替代 source） | 生成交付物时优先读取的页面层视图，内部存在不同 knowledge_role。 |
| `sources/` | 原始事实材料层 | 是（原始） | 保存原始事实材料，用于核对与追溯。 |
| `prompts/` | 辅助 prompt 工具 | 否 | 用于生成/检查流程，不作为事实源。 |

补充说明：

* README 不是事实源；
* `pages/*.md` 是当前可读页面层；
* `pages/*.md` 作为交付生成时优先读取的页面层视图；
* `pages/*.md` 通过 `active_source` 指向当前页面详细事实载体；
* `sources/` 是原始事实材料层（事实核对入口）；
* superseded source、archive、old output、draft output、`outputs/handoff/_drafts/` 不作为当前事实源；
* 新增交付件不得继续放入 `sources/`，统一归档到 `outputs/handoff/`；
* `outputs/handoff/` 是交付归档层，不作为事实源；
* decisions 是判断记录；
* pending 是待确认问题池；
* prompts 是辅助工具。

## 4. 当前页面 brief

| 页面 | Brief | Active Source | status | knowledge_role | 待确认数量 |
|---|---|---|---|---|---:|
| home | `pages/home.md` | 以 page brief frontmatter 的 `active_source` 为准 | current | handoff-brief | - |
| shop | `pages/shop.md` | 以 page brief frontmatter 的 `active_source` 为准 | current | handoff-brief | - |
| open-box | `pages/open-box.md` | `sources/open-box.md` | current | fact-brief | - |
| open-box-result | `pages/open-box-result.md` | 以 page brief frontmatter 的 `active_source` 为准 | current | handoff-brief | - |
| toy-collection | `pages/toy-collection.md` | 以 page brief frontmatter 的 `active_source` 为准 | current | handoff-brief | - |

待确认数量以 `pending.md` 当前汇总为准。

补充说明：

* `pages/*.md` 当前均为可读页面层，但知识性质不同；
* `open-box.md` 已沉淀为 `fact-brief`（当前页面口径承接层）；
* `home.md`、`shop.md`、`open-box-result.md`、`toy-collection.md` 当前为 `handoff-brief`；
* `handoff-brief` 用于研发交接、页面理解和待确认承接；
* 除 `open-box.md` 外，其它 handoff-brief 当前不作为页面事实口径层使用；
* 所有 page brief 均不替代 `sources/*.md`；
* 事实争议或核对场景以 page brief 声明的 `active_source` 为入口；
* 页面与项目入口统计以 `pending.md` 正式条目为准。

## 5. 主库路径调整说明

* 历史 V1 已完成备份；
* 当前日常读取与核对以 `pages/`、`pending.md`、`decisions.md`、`sources/`、`project-brief.md` 为主；
* prompts 仅作为生成与校验辅助工具；
* 后续不再将 V1 作为 active 依赖路径。

## 6. 使用边界

* README 是导航，不是事实源；
* 本项目当前优先沉淀页面表达和交接信息；
* 不直接定义支付、库存、发货、资产、权益、奖励、结算、订单、会员、活动、背包、交易、兑换、养成等完整业务规则；
* 不承接设计待办、UI 出稿事项、研发任务、测试用例、项目排期或纯视觉实现细节；
* 如需高风险业务规则，需要另行确认范围。

## 7. 当前状态

* 5 个 source 已迁移；
* 5 个 page brief 已生成；
* `pending.md` 已汇总；
* `decisions.md` 已更新；
* `project-brief.md` 已更新；
* 后续可做当前主工作台全局 stage check。

## 8. Knowledge Workflow

### 8.1 Knowledge Update Loop

定义：

当页面规则、产品判断、待确认事项、合规/UI/研发/运营反馈发生变化时，必须先进入 `Knowledge Update Loop`。

流程：

1. 输入本次修改信息；
2. 读取当前 `pages/`、`decisions.md`、`pending.md`，必要时读取 `sources/`；
3. 判断本次变化影响的知识层级；
4. 输出知识库更新 patch；
5. 人工确认；
6. 写入知识库。

产出：

知识库实时源更新。

### 8.2 Delivery Output Loop

定义：

当知识库已更新并确认后，才允许生成交付物。

流程：

1. 读取当前 page brief；
2. 读取 page brief 声明的 `active_source`；
3. 读取 `pending.md` 与 `decisions.md`；
4. 按 `prompts/delivery-output-handoff.md` active 规则生成交付物；
5. 若 Copy Coverage 不通过，输出 Copy Coverage Failure Report，不得声称完整交付；
6. 人工确认；
7. 归档到 `outputs/handoff/`。

Module Change Note:

Use `projects/bomcase/prompts/delivery-output-module-change-note.md` only after the fact layer has already been updated and validated.

It is a module-scoped Delivery Output variant.

It inherits Delivery Output skeleton semantics and does not replace Full Handoff or Incremental Handoff.

边界：

* 不得将 archive、old output、draft output、`outputs/handoff/_drafts/` 作为事实源；
* full mode 不得将 active source 中仍有效事实摘要化；
* 执行命令只提供输入参数、读取范围、输出路径和执行边界，不补充、不替代、不扩展 prompt 规则。
* Module Change Note 命令同样只提供输入参数、读取范围、输出路径和执行边界，不补充、不替代、不扩展结构规则。

> Test-4 通过 Copy Coverage 验证仅作为 workflow 验证结论，不作为产品事实写入。

产出：

交付物归档。

### 8.3 Loop Order Rule

* `Knowledge Update Loop` 必须先于 `Delivery Output Loop`；
* 不允许在知识库未更新确认前直接生成最终交付物；
* 如果 `Delivery Output Loop` 发现知识库缺口，必须中止并回到 `Knowledge Update Loop`；
* 交付物不得反向覆盖 `pages/`、`decisions.md`、`pending.md` 或 `sources/` 的事实层。

### 8.4 Standard Change Input Format

```text
本次修改的页面：
变化来源：
修改内容：
确认状态：
```

补充说明：

* “确认状态”可为：已确认 / 待确认 / 部分确认；
* AI 应基于该输入输出知识库更新 patch；
* 人工确认后才写入知识库。

### 8.5 Directory Boundary

* `pages/` 是当前可读页面层（按 `knowledge_role` 区分 `fact-brief` 与 `handoff-brief`）；
* `pages/*.md` 是生成页面交付物时优先读取的页面层视图；
* `pages/` 保存从原始材料、判断和确认结果整理出的当前页面阅读口径与待确认承接状态；
* `decisions.md` 是已确认判断；
* `pending.md` 是待确认事项；
* `sources/` 是原始事实材料；
* 每个页面的详细事实载体以 page brief frontmatter 的 `active_source` 为准；
* 新增交付件不得放入 `sources/`；
* `outputs/handoff/` 是交付物归档层，不作为事实源；
* `outputs/handoff/_drafts/` 仅用于测试草稿，不作为事实源。

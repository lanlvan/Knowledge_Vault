# BOMCASE Decisions

## 1. 使用说明

说明：

* 本文件记录 BOMCASE 项目级产品判断；
* 本文件继承根级 `decisions.md` 的工作台治理规则与业务边界原则；
* 本文件不记录工作台级规则；
* 本文件不记录设计待办、研发任务、测试用例、项目排期；
* 本文件不替代 source；
* 本文件不记录 pending 未确认项；
* 本文件不作为完整业务规则库。

## 2. Project Source Decisions

### BOM-D001

* 编号：BOM-D001
* 原编号：D-005
* 判断：BOMCASE 已采用由 1 个 consolidated active source（`sources/open-box.md`）与 4 个 handoff_document active source 组成的 5 个页面级一级事实源，且均通过 page brief 的 `active_source` 字段引用。
* 影响范围：页面事实核对、争议回溯与 page brief 更新入口。
* 状态：active

### BOM-D002

* 编号：BOM-D002
* 原编号：D-007
* 判断：BOMCASE 不迁移 V1 confirmed rule 原结构，避免回到重规则拆分模式。
* 影响范围：项目资料结构轻量化与维护成本控制。
* 状态：active

## 3. Page Brief Decisions

### BOM-D003

* 编号：BOM-D003
* 原编号：D-010
* 判断：`home`、`shop`、`open-box`、`open-box-result`、`toy-collection` 五个 page brief 已作为当前 active 页面层。
* 影响范围：页面表达层主读取入口与日常维护路径。
* 状态：active

### BOM-D004

* 编号：BOM-D004
* 原编号：D-013
* 判断：BOMCASE 的 V1 rules 内容采用“压缩为 page brief”方式承接，而非照搬规则文件拆分结构。
* 影响范围：项目内历史信息复用与页面表达维护效率。
* 状态：active

### BOM-D007

* 编号：BOM-D007
* 类型：page-brief-governance
* 层级：project
* 原编号：无。该条为本轮新增项目级判断，不从旧 D 编号迁移。
* 判断：BOMCASE `pages/` 下 page brief 按 `knowledge_role` 区分为 `fact-brief` 与 `handoff-brief`。
* 具体口径：
  * `open-box.md`、`open-box-result.md`、`shop.md`、`toy-collection.md` 当前为 `fact-brief`，可作为当前页面事实口径层读取；
  * `home.md` 当前为 `handoff-brief`，用于研发交接、页面理解和待确认承接；
  * `handoff-brief` 不等同于事实源，不替代 source；
  * 事实争议仍回到 `sources/*` 核对。
* 背景/来源：本轮 BOMCASE Knowledge Vault 第一轮结构治理与 page brief role 治理结果。
* 同步记录：2026-07-01: Open Box Result upgraded to fact-brief after page brief role review; no business facts changed.
* 同步记录：2026-07-01: Shop upgraded to fact-brief after page brief role review; no business facts changed.
* 同步记录：2026-07-02: Toy Collection upgraded to fact-brief after brief sync validation and role upgrade review; no business facts changed.
* 影响范围：影响 BOMCASE 页面层读取顺序、AI 读取判断、page brief 与 source 的关系解释。
* 状态：active

### BOM-D008

* 编号：BOM-D008
* 类型：knowledge-loop-governance
* 层级：project
* 原编号：无。该条为本轮新增项目级判断，不从旧 D 编号迁移。
* 判断：BOMCASE 的 `pending.md` 作为当前待确认池维护，不作为 changelog 使用。
* 具体口径：
  * 已确认问题应从 `pending.md` 移出；
  * 已确认页面口径优先回写对应 `pages/*.md`；
  * 仅在形成稳定项目级判断时再转入 `projects/bomcase/decisions.md`。
* 背景/来源：本轮 BOMCASE Knowledge Update Loop 的页面回写与待确认收口实践。
* 影响范围：影响 BOMCASE 待确认维护方式、page brief 回写路径与 decisions 收口边界。
* 状态：active

## 4. Product Boundary Decisions

当前无新增仅属于 BOMCASE 的产品边界决策；项目边界治理沿用根级 `decisions.md`。

## 5. Page Expression Decisions

### BOM-D005

* 编号：BOM-D005
* 原编号：D-023
* 判断：Open Box 的“能量溢出提示”属于页面展示口径补充，不构成资源计算规则变更。
* 影响范围：开箱页信息层级解释与评审口径一致性。
* 约束：展示位置限定在右侧卡牌背包全展开态底部固定汇总区；不进入中部满足度、资源构成 icon 区或左侧资源概览；不改变中部主结构与开启按钮主状态。
* 状态：active

### BOM-D009

* 编号：BOM-D009
* 类型：page-expression-governance
* 层级：project
* 原编号：无。该条为本轮新增项目级判断，不从旧 D 编号迁移。
* 判断：当 Banner 点击行为来源于配置结果时，页面侧只消费配置结果，不在 page brief 中定义固定行为枚举，也不展开配置端能力。
* 影响范围：影响首页及后续同类 Banner 页面在 page brief 中的表达边界与验收口径。
* 状态：active

### BOM-D010

* 编号：BOM-D010
* 类型：page-expression-governance
* 层级：project
* 原编号：无。该条为本轮新增项目级判断，不从旧 D 编号迁移。
* 判断：当页面截图仅作为示意时，验收以产品规则为准，不以截图样例状态作为固定规则。
* 影响范围：影响页面验收基线、截图与规则冲突时的判断顺序，以及 page brief 的回写口径。
* 状态：active

## 6. Superseded / Legacy Decisions

### BOM-D006

* 编号：BOM-D006
* 原编号：D-014
* 判断：`project-brief.md` 中“page brief 尚未生成”的历史状态已被当前页面层事实替代。
* 影响范围：历史状态解释与当前页面层事实对齐。
* 状态：superseded

## 7. 当前不决策事项

以下内容仍属于待确认，不应写成已决策事项：

* `pending.md` 中仍在“待确认”状态的所有条目；
* 尚未完成 pending -> page brief -> decisions 闭环的页面细节；
* 设计待办、研发任务、测试用例、项目排期相关内容。

## 8. Delivery Output Loop Governance Decisions

### BOM-D011

* 编号：BOM-D011
* 类型：delivery-output-loop-governance
* 层级：project
* 状态：active

#### Delivery Output Loop v1.1 Neutral Prompt Baseline

* `projects/bomcase/prompts/delivery-output-handoff.md` v1.1 是当前项目级 Delivery Output Loop active prompt。
* `delivery-output-handoff.md` 是中立 prompt，不承载页面独有业务事实。
* 页面独有事实只来自当前 page brief、active source、`pending.md`、`decisions.md`。
* Delivery Output 生成不得读取 archive、old output、draft output 或 `_drafts/` 作为事实源。
* Full mode 必须保留 active source 中仍有效的字段、状态、交互、验收口径和用户可见文案颗粒度，不得摘要化。
* 已确认用户可见文案、info / hover 文案、按钮文案、状态文案、底部汇总文案不得被概括替代。
* 若 Copy Coverage 不通过，必须输出 Copy Coverage Failure Report，不得声称生成完整交付文档。
* 执行命令应保持纯净，只提供输入参数、读取范围、输出路径和执行边界，不补充、不替代、不扩展 prompt 规则。
* 交付正文中，“后端”用于角色 / 责任 / 协作确认；“服务端”用于接口返回 / 配置 / 结算 / 系统判断结果。
* 待确认 / 待补充项在交付正文中应按“是否阻塞开发启动 / 是否影响验收 / 是否属于后续补充边界”表达，不使用“已登记 / 未登记 / pending / 全局待确认池”等内部管理表达。
* Test-4 通过 Copy Coverage 验证仅作为 workflow 验证结论，不作为产品事实写入。

#### Delivery Output Capability Closure

* 本轮 Delivery Output 能力补强已闭环。
* Completeness Floor、Formal Body Shape、Reference ID Scope 已通过 Open Box 输出样本验证。
* 正式研发交付稿使用 `delivery-ready` 正文形态。
* 正式正文只包含 13 节研发交付正文，不包含 Generation Report。
* 普通 Full 测试稿可附 Generation Report / Coverage Baseline，用于治理复盘。
* Generation Report 是治理 / 自检报告，不是研发正文。
* Full Mode Completeness Floor 用于防止过度压缩。
* 字段、状态、交互、用户可见文案、info / hover、底部汇总、验收边界不得摘要化。
* Reference ID Scope 用于防止全文编号化。
* 编号只服务第 12 节验收口径中的行级验收引用。
* 普通字段、普通交互、普通状态、普通说明优先使用章节级引用。
* page brief / active source / `pending.md` / `decisions.md` 仍是 Delivery Output 事实读取链路。
* output drafts 仅作为验证样本，不反推事实层或 prompt 模板。
* 本轮能力治理不写入 `pending.md`，`pending.md` 仅记录产品待确认项。

## 9. Source / Brief Object Spec Decisions

### BOM-D013 Source / Brief Object Spec v0.1

* 编号：BOM-D013
* 类型：source-brief-object-governance
* 层级：project
* 原编号：无。该条为本轮新增项目级判断，不从旧 D 编号迁移。
* 判断：BOMCASE 已新增 `projects/bomcase/specs/source-brief-object-spec.md`，该文件在 v0.1 阶段作为最小对象规范草案，用于约束 page brief 与 active source 的最低对象一致性。
* 具体口径：
  * 该规范用于后续维护 page brief / active source 时避免结构漂移；
  * 该规范不替代 `delivery-output-handoff.md`；
  * 该规范不替代 `stage-check.md`；
  * 该规范不作为 Delivery Output 的页面事实源；
  * 该规范不改变当前 page brief → `active_source` → active source + `pending.md` + `decisions.md` → Delivery Output 的事实读取链路；
  * 该规范不触发 source 重命名；
  * 该规范不要求历史 source 立即补正文；
  * 命名重构、术语统一、表格列结构、archive / output 命名等仍留待 v0.2 或独立任务。
* 背景 / 来源：`projects/bomcase/specs/source-brief-object-spec.md` v0.1 最小草案创建与第一轮校验。
* 影响范围：BOMCASE page brief 与 active source 的最小对象治理起点。
* superseded_by：BOM-D014
* 当前口径：当前维护已切换到 `projects/bomcase/specs/source-brief-object-spec.md` `version: v0.2`。
* 状态：superseded

### BOM-D014 Unified Schema v1 / Source-Brief Object Spec v0.2

* 编号：BOM-D014
* 类型：source-brief-object-governance
* 层级：project
* 原编号：无。该条为本轮新增项目级判断，不从旧 D 编号迁移。
* 判断：BOMCASE Unified Schema v1 / `source-brief-object-spec.md` v0.2 成为当前 page brief 与 active source 的统一维护骨架。
* 适用范围：5 个 page brief + 5 个 active source。
* 具体口径：
  * brief 统一为 8 段骨架，source 统一为 11 段骨架；
  * Open Box 不作为结构例外，只作为高复杂度样本；
  * source_type 保持差异：Open Box 为 `consolidated_source`，Home / Shop / Open Box Result / Toy Collection 为 `handoff_document`；
  * 统一结构不等于统一颗粒度，不要求其它页面补到 Open Box 颗粒度；
  * `pending.md` 仍是唯一未确认事实池，`decisions.md` 仍是稳定项目判断池；
  * outputs / drafts / archive 不作为当前事实源；
  * Delivery Output 事实读取继续遵循 `page brief -> active source -> pending.md -> decisions.md`。
* 背景 / 来源：Unified Schema v1 在 5 页 brief/source 骨架已落地，v0.1 与当前事实层发生脱节，需要以 v0.2 固化当前维护口径。
* 影响范围：BOMCASE 后续 brief/source 维护、结构对齐与事实读取边界解释。
* 状态：active

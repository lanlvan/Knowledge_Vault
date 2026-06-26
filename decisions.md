# Knowledge Vault Decisions

## 1. 使用说明

说明：

* 本文件记录 Knowledge Vault 工作台级决策；
* 本文件只记录跨项目通用的知识库治理、读取顺序、边界规则、维护机制和多项目结构规则；
* 本文件不记录单项目产品判断、页面判断、业务规则或待确认项；
* 本文件不替代 source；
* 本文件不记录 pending 未确认项；
* 本文件不作为完整业务规则库；
* Knowledge Vault 是产品知识库，不是项目协作工具。

## 2. Workspace Governance Decisions

### W-D001

* 编号：W-D001
* 原编号：D-001
* 判断：`F:\Knowledge_Vault\` 是当前 active 工作台根路径。
* 影响范围：跨项目资料沉淀、AI 读取入口与工作台路径统一。
* 状态：active

### W-D002

* 编号：W-D002
* 原编号：D-003
* 判断：默认读取顺序采用“项目 README -> project-brief -> pending/decisions -> page brief -> sources”。
* 影响范围：跨项目人读与 AI 读时的检索顺序和上下文一致性。
* 状态：active

### W-D003

* 编号：W-D003
* 原编号：D-002 / D-004
* 判断：V1/legacy 资料仅用于追溯，不作为当前 active 文件体系直接执行。
* 影响范围：跨项目历史资料使用边界与日常核对路径。
* 状态：active

## 3. Source / Brief / Pending / Decisions Governance

### W-D004

* 编号：W-D004
* 原编号：D-011 / D-012 / D-015 / D-016
* 判断：`source`、`page brief`、`pending`、`decisions` 采用分工治理：source 是一级事实源，page brief 是页面表达摘要，pending 记录待确认事项，decisions 记录已确认判断。
* 影响范围：跨项目资料职责边界、冲突处理优先级与维护一致性。
* 状态：active

### W-D005

* 编号：W-D005
* 原编号：D-018
* 判断：不把猜测性问题写入 pending，仅记录已明确且待确认的事项。
* 影响范围：待确认池质量与沟通噪声控制。
* 状态：active

### W-D006

* 编号：W-D006
* 原编号：D-017
* 判断：已解决 pending 事项需回写对应 page brief；形成稳定判断后再进入 decisions，保持闭环。
* 影响范围：跨项目问题闭环与文档一致性维护。
* 状态：active

## 4. Knowledge Boundary Decisions

### W-D007

* 编号：W-D007
* 原编号：D-019
* 判断：采用“页面表达”与“完整业务规则”分离策略。
* 影响范围：需求澄清边界、文档范围控制与跨项目复用一致性。
* 状态：active

### W-D008

* 编号：W-D008
* 原编号：D-020
* 判断：不在 decisions 中定义支付、库存、发货、资产、权益、奖励、结算、订单、会员、活动、背包、交易、兑换、养成等完整系统规则。
* 影响范围：避免将 decisions 误用为完整业务规则库。
* 状态：active

### W-D009

* 编号：W-D009
* 原编号：D-021
* 判断：高风险或高复杂业务规则需先单独确认范围，再决定是否进入专项文档。
* 影响范围：跨项目规则治理流程与变更风险控制。
* 状态：active

## 5. Multi-project Structure Decisions

### W-D010

* 编号：W-D010
* 原编号：D-022
* 判断：当前工作台由 V2 独立化而来，并作为唯一 active 工作台使用；历史 V1 路径仅保留追溯用途，不作为 active 依赖。
* 影响范围：工作台历史定位解释、跨项目读取入口一致性与 active 路径治理。
* 状态：active

### W-D011

* 编号：W-D011
* 原编号：D-009
* 判断：迁移与日常维护不预建空壳大目录，不创建 `business-rules` 作为默认承载目录。
* 影响范围：目录轻量性、可读性与按需扩展策略。
* 状态：active

## 6. Legacy / Migration Decisions

### W-D012

* 编号：W-D012
* 原编号：D-006
* 判断：不迁移 `_import` 重复副本。
* 影响范围：迁移去重策略与后续维护成本控制。
* 状态：active

### W-D013

* 编号：W-D013
* 原编号：D-008
* 判断：不迁移 00-06 workflow 重流程模板。
* 影响范围：流程复杂度控制与知识库轻量化。
* 状态：active

## 7. 当前不决策事项

以下内容当前不进入工作台级 decisions：

* 各项目 `pending.md` 中仍在“待确认”状态的所有条目；
* 单项目页面细节、交互细节、文案细节与局部实现口径；
* 设计待办、研发任务、测试用例、项目排期等项目协作事项。

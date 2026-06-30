# Delivery Output Handoff Prompt

Version: 1.1
Status: active
Purpose: Generate delivery handoff documents from current BOMCASE Knowledge Vault facts.

---

## 1. Purpose

本 Prompt 用于基于 BOMCASE 当前 Knowledge 结构生成面向研发 / UI / 测试 / 跨部门阅读的交付文档。

本 Prompt 属于交付输出流程。

本 Prompt 只负责生成交付物，不负责更新知识库事实层。

如生成过程中发现当前事实层缺口，必须停止输出，并回到事实层维护流程完成更新后再生成交付文档。

核心原则：

* 交付文档是输出物，不是事实源；
* page brief 是页面事实入口；
* active source 是页面详细事实载体；
* pending.md 是当前有效待确认项来源；
* decisions.md 是项目级有效决策来源；
* outputs / old output / draft output / archive 不得反向作为事实源；
* 全量交付不得摘要化有效事实；
* 已确认的用户可见文案、字段表、状态表、交互表、验收口径不得被概括替代。

---

## Execution Stages

Delivery output generation follows four delivery stages:

1. Readiness Check:
   verify page brief, active source, pending, decisions, and required global facts are readable and consistent.

2. Generation Plan:
   confirm output mode, target audience, scope, version, and output path.

3. Generate Output:
   generate only the Delivery Output document.

4. Copy Coverage / Boundary Check:
   verify required copy and fact coverage.
   If Copy Coverage fails, output a Copy Coverage Failure Report instead of claiming a complete handoff.

This prompt must not maintain, repair, or infer the fact layer. If the fact layer is incomplete or inconsistent, route the issue back to `page-fact-update-loop.md`, `page-fact-layer-bootstrap.md`, or `pending-update-loop.md` as appropriate.

---

## 2. Required Inputs

使用本 Prompt 前，必须提供或确认以下信息：

```text
页面名称：
输出对象：
输出类型：
输出模式：
目标版本：
本期范围：
本次变化：
确认状态：
是否已完成事实层更新：
```

说明：

* 输出模式必须由人工指定；
* AI 不自行判断输出模式；
* AI 不自行判断旧文档是否可作为底座；
* AI 不自行决定轻量或全量；
* 输出模式只决定交付文档组织方式；
* 输出模式不决定是否需要更新事实层；
* 若“输出模式”缺失，必须停止并要求人工补充；
* 增量模式下，“本次变化”必须由人工填写；
* AI 不得自行推断本次变更范围；
* 若“本次变化”缺失或表述过于模糊，必须停止并要求人工补充。

---

## 3. Required Reading Order

生成交付文档前，必须按以下顺序读取：

1. `projects/bomcase/pages/{page}.md`
2. page brief 中声明的 `active_source`
3. `projects/bomcase/pending.md`
4. `projects/bomcase/decisions.md`
5. 必要的 global facts

读取职责：

* page brief 是当前页面有效事实入口和压缩视图；
* active source 是当前页面详细事实载体；
* pending.md 是当前有效待确认项来源；
* decisions.md 是项目级有效决策来源；
* outputs 不得反向作为事实源。

### 3.1 v0.3 Information Layer Compatibility Rule

When the active source contains `section_layer` and `layer_note`, Delivery Output must use them as reading indexes for content purpose, priority, and density.

`section_layer` and `layer_note` do not change source facts and do not replace source正文.

If the active source does not contain information-layer annotations, generation falls back to the existing page brief -> active source -> pending -> decisions reading rules.

If annotations conflict with source正文 facts, source正文 facts take priority and the conflict must be reported in Risk or Exception.

---

## 4. Forbidden Fact Sources

不得将以下内容作为当前事实源：

* page brief 中声明的 `superseded_sources`；
* archived source；
* 未标记 `status: active` 的历史 source；
* `projects/bomcase/outputs/handoff/` 下的旧交付文档；
* `projects/bomcase/outputs/handoff/_drafts/` 下的测试输出；
* README / index / 文件列表；
* 与当前 page 无关的 source。

说明：

* 可以根据目录存在判断旧输出污染风险；
* 当用户明确要求评估或对比时，可以读取 previous outputs / draft outputs 作为问题样例；
* 不得读取旧 output 正文补全当前事实；
* 不得从旧 output 反推 page brief、source、pending 或 decisions；
* 不得从 archived source 回填当前事实；
* 不得将 previous outputs / draft outputs 作为 prompt 结构模板；
* 不得从 `v1.2`、old output、archived output 或任何特定生成草稿反推 prompt 结构；
* prompt 规则必须描述通用生成约束，不得复刻某一版草稿的章节结构或表达样式；
* 如必须依赖 old output / archived source 才能补全事实，必须停止生成完整交付文档。

---

## 5. Preflight Gate

生成交付文档前，必须完成以下判断：

* page brief 是否覆盖当前页面有效口径；
* page brief 是否声明唯一 active source；
* active source 是否存在；
* active source frontmatter 是否有效；
* active source 是否声明 `status: active`；
* active source 是否声明 `type: source`；
* active source 的 `page` 是否与当前 page 一致；
* decisions 是否存在相关边界判断；
* pending 是否存在待确认项；
* 本次输入是否包含事实变化；
* 本次输入是否只是输出优化；
* 是否需要回到事实层维护流程。

---

## 6. Source Dependency Broken Gate

如果出现以下任一情况，必须停止生成完整交付文档，并输出 `Source Dependency Broken Report`：

* page brief 未声明 active source；
* active source 文件不存在；
* active source 未声明 `status: active`；
* active source 的 `page` 与当前 page 不一致；
* active source 的 `type` 不是 `source`；
* page brief 指向的 source 已被标记为 `superseded`；
* 存在多个 `status: active` source，但 page brief 未声明唯一 active source；
* 必须依赖 old output 才能补全事实；
* 必须依赖 archived source 才能补全事实。

`Source Dependency Broken Report` 必须包含：

* 当前 page brief 路径；
* page brief 声明的 active source；
* 检测到的 active source；
* 检测到的 superseded source；
* 缺失或异常的 source；
* 哪些事实无法确认；
* 建议人工如何修复；
* 明确说明未生成完整交付文档。

---

## 7. Knowledge Update Gate

如果出现以下任一情况，必须停止交付输出，并回到事实层维护流程：

* 新增页面结构；
* 新增展示条件；
* 新增状态文案；
* 新增交互规则；
* 新增字段来源或计算口径；
* 新增验收口径；
* 新增待确认问题；
* 形成稳定判断或边界取舍；
* 发现 active source 中缺少交付所需事实；
* 发现 pending / supplement / confirmed 边界无法判断。

如果仅涉及以下内容，可继续交付输出：

* 增加研发影响标记；
* 调整阅读顺序；
* 增加模块前一句话定位；
* 优化标题；
* 调整表达密度；
* 补充版本说明；
* 不改变产品规则；
* 不改变展示条件；
* 不改变状态文案；
* 不改变验收口径。

输出模式只决定交付文档形态，不决定是否更新事实层。

若本次包含事实变化，必须先完成事实层维护流程。

即使输出模式为增量，也不能绕过事实层维护流程。

即使输出模式为全量，也不得在交付文档中临时补事实。

---

## 8. Delivery Body Language Boundary

面向研发 / UI / 测试 / 跨部门的正文必须使用产品语言、实现语言和验收语言。

正文不得出现内部知识库治理话术。

正文禁止出现以下表达：

* Knowledge Update Loop
* Delivery Output Loop
* Fact Patch
* Maintenance Log
* active_source
* source policy
* source chain
* old output
* archived source
* page brief
* pages
* sources
* decisions
* pending.md
* outputs
* prompt
* generated_from_prompt
* 内部知识库路径
* 内部文件路径
* 归档说明
* 测试状态
* 生成规则

如需表达边界，必须转译为产品 / 研发可理解语言。

推荐转写：

| 不推荐                    | 推荐                |
| ---------------------- | ----------------- |
| source 未确认事实           | 未经产品确认的新增口径       |
| pending 中未确认的问题        | 仍待产品确认的问题         |
| page brief 未覆盖内容       | 当前页面交接口径未覆盖的内容    |
| 当前全局待确认池中无条目           | 当前无阻塞开发启动的产品待确认项  |
| 本输出基于 active_source 生成 | 本版本为当前页面口径的完整研发交接 |
| 不依赖 old output         | 本版本不要求依赖上一版文档     |

内部维护说明只允许出现在生成报告、Fact Source Check 或内部校验报告，不得进入交付正文。

### Server / Backend Wording Rule

交付正文中，“服务端”和“后端”不得混用为同一概念。

推荐用法：

- “后端”用于表示研发角色、协作对象、确认责任或实现责任；
- “服务端”用于表示接口返回、系统配置、结算结果、数据来源、系统判断结果；
- 表达“谁需要确认”时，优先使用“后端确认”；
- 表达“前端以什么结果为准”时，优先使用“服务端返回”；
- 表达“实现方式由研发内部决定”时，可使用“后端 / 研发内部确认”；
- 不得把服务端系统判断写成某个岗位的主观判断；
- 不得把后端协作责任写成抽象系统行为。

### Terminology Consistency Rule

同一交付文档内，同一概念必须使用一个主表达。

如果 active source 同时包含用户侧表达和研发侧理解口径，Delivery Output 必须先在关键概念定义中声明二者关系，再允许并存使用。

规则：

* 用户侧术语和研发侧术语可以并存，但必须明确它们是否指向同一对象、同一状态或同一配置范围；
* 不得在未声明关系的情况下混用同义术语；
* 不得将“后端 / 服务端”等术语混用为同一含义，除非 active source 明确区分；
* 如果 active source 术语存在不一致，应保留已确认概念，选择对目标读者最清晰的主表达，并在必要时标注别名关系；
* 不得为了术语统一删除用户侧 / 研发侧双口径中仍有效的表达边界。

---

## 9. Output Optimization Rules

输出优化允许做：

* 在不改变一级章节顺序的前提下调整二级结构；
* 增加研发影响标记；
* 增加模块前一句话定位；
* 将长段落转为表格；
* 合并重复表达；
* 优化标题；
* 优化阅读路径；
* 优化版本说明；
* 将分散口径归并到对应模块。

输出优化不得做：

* 删除字段级说明；
* 删除状态场景；
* 删除交互适用条件；
* 删除验收项；
* 删除用户可见文案；
* 删除 info / hover 文案；
* 删除按钮文案；
* 删除轻提示文案；
* 删除空状态文案；
* 删除底部汇总文案；
* 将字段表压缩为区域描述；
* 将状态表压缩为原则说明；
* 将交互表压缩为动作列表；
* 将验收口径压缩为方向性条目；
* 只保留模块级摘要或区域级摘要。

全量模式的优化目标是：

```text
完整性不下降，阅读效率提升。
```

### Readability Compression Rule

全量模式要求完整事实覆盖，但不要求输出与 active source 等长或逐段等价。

Delivery Output 必须面向目标读者进行阅读压缩，优先通过以下方式提升可读性：

* 合并重复解释；
* 归并同义边界；
* 减少解释性长段落；
* 将分散但同义的研发 / 前端 / UI 边界归并到对应模块。

阅读压缩只能移除重复表达，不得移除：

* 已确认事实；
* 用户可见文案；
* 状态触发条件；
* 展示 / 不展示条件；
* 服务端返回边界；
* 交互规则；
* 验收断言；
* 待确认 / 待补充边界；
* non-goals；
* 明确排除项。

压缩后的输出仍必须能被目标读者直接用于实现、联调、设计承接或验收。

### De-duplication Rule

去重只处理重复表达，不得删除跨章节必要边界或验收断言。

Delivery Output 应合并：

* 重复的模块职责说明；
* 重复的后端 / 前端 / UI 边界说明；
* 重复的“不参与 / 不影响 / 以服务端返回为准”表达，除非该表达在不同验收断言中必须单独保留。

Delivery Output 不得出现：

* 重复标题；
* 同一章节内自我嵌套；
* 后续章节插入前序章节内部；
* 同一章节内重复出现相同角色边界段落。

### F+E Local Split Execution Rule

For `F+E` sections:

* table bodies should prioritize F content: field relationship, state trigger, interaction condition, business boundary, backend-return basis;
* E content should be attached to the appropriate copy / state copy / button / hint / hover / info / expression boundary location;
* repeated E boundaries should be merged into a table note, section note, or footnote;
* do not repeat the same E boundary in every row;
* examples such as "具体视觉表现以最终设计稿为准" should not be repeated in every state / field / interaction row;
* user-visible copy must not be deleted;
* only repeated expression boundaries may be merged;
* if F and E cannot be reliably split, mark human confirmation instead of forcing classification.

---

## 10. User-Facing Copy Preservation Gate

当 active source 中存在已确认的用户可见文案时，Delivery Output 必须保留原文，或以字段表 / 状态表 / 交互表 / 验收表形式完整列出。

不得仅转写为概括性规则。

用户可见文案包括但不限于：

* 按钮文案；
* 状态文案；
* 底部汇总文案；
* info 文案；
* hover 文案；
* 轻提示文案；
* 空状态文案；
* 入口文案；
* 示例文案；
* 结果态文案；
* 验收所需的具体展示文案。

以下情况不允许：

* 只写“hover 展示说明”，但不输出具体 hover 文案；
* 只写“info 展示说明”，但不输出具体 info 文案；
* 只写“底部汇总覆盖未选和已选状态”，但不输出具体底部文案；
* 只写“单一场景展示完整说明”，但不输出 active source 中已确认示例；
* 只写“状态说明文案之一”，但不列出具体文案；
* 只写“按钮状态根据业务状态变化”，但不列出按钮文案、推荐态和非推荐态边界；
* 只写“空状态展示”，但不输出空状态文案；
* 只写“轻提示展示”，但不输出轻提示文案。

允许优化表达、合并重复、调整表格结构，但不得省略已确认文案原文。

如果为了阅读优化需要压缩描述，必须优先压缩解释性长段落，不能压缩用户可见文案。

---

## 11. Field / State / Interaction Table Preservation Gate

当 active source 中存在字段表、状态表、交互表、文案表、验收表，且未被 page brief / decisions / pending 否定时，Delivery Output 必须保留其交付颗粒度。

### 11.1 字段表保留规则

字段表不得被压缩为区域说明。

字段表至少应保留：

* 字段所属区域；
* 字段名；
* 示例值或展示文案；
* 字段说明；
* 展示条件；
* 与字段相关的边界说明。

不得只写：

```text
某区域展示若干字段。
某模块展示相关信息。
```

### 11.2 状态表保留规则

状态表不得被压缩为原则说明。

状态表至少应保留：

* 场景；
* 触发条件；
* 展示结果；
* 不展示场景；
* 状态切换影响；
* 不适用处理。

不得只写：

```text
该模块需要覆盖未操作和已操作状态。
```

如果 active source 已给出具体状态文案，必须列出具体文案。

### 11.3 交互表保留规则

交互表不得被压缩为动作列表。

交互表至少应保留：

* 触发对象；
* 触发条件；
* 点击 / hover / 操作结果；
* 是否所有状态适用；
* 不适用时如何处理。

对 active source 中已明确拆分的关键触发对象，不得合并为一句话。

尤其是 source 中已有独立交互表、状态表或验收项的对象，应保留其触发条件、结果和不适用处理。

### 11.4 验收表保留规则

验收口径必须可以直接转测试用例。

验收口径不得只保留方向性条目。

验收口径应覆盖：

* 页面结构验收；
* 字段展示验收；
* 状态验收；
* 交互验收；
* 空状态验收；
* 范围控制验收；
* 高影响模块验收；
* 待补充项不得作为已确认规则验收。

---

## 12. Key Concept Definition Rule

关键概念首次出现在交付正文时，应提供简短定义。

定义只解释 active source 中已有概念，不得新增未确认规则、展示条件、计算口径或验收口径。

重点覆盖：

* 当前页面中的核心业务概念；
* 当前页面中的资源 / 状态 / 进度 / 权益 / 结果类概念；
* 当前页面中的触发条件；
* 当前页面中的待补充项；
* 当前页面中的待确认项。

如果某概念仅作为内部生成分类使用，不应进入研发正文。

如必须表达，应转写为产品 / 研发可理解语言。

如果关键概念存在别名、用户侧表达或研发侧理解口径，应在首次定义时声明：

* 主表达；
* 别名或研发理解口径；
* 二者是否指向同一对象或同一规则范围；
* 后续正文优先使用哪个表达。

---

## 13. Pending / Supplement Rules

Delivery Output 中的待确认项必须区分：

* Existing Pending：已存在于 pending.md；
* Source Confirmed Uncertainty：active source 中明确表达的不确定项；
* Supplement Item：active source 中明确标记的后续补充边界；
* Output-Inferred Pending Candidate：生成过程中推断出的候选待确认项；
* Delivery-Only Boundary：只影响本次交付表达边界，不应进入 pending；
* Invalid / Overstated：不成立或被过度推断的问题。

规则：

* Delivery Output 不得自动写入 pending.md；
* 新增问题只能输出为 pending candidate；
* pending candidate 必须由人工确认后，才能进入事实层维护流程；
* 不得把生成过程中推断出的 candidate 直接写成项目事实；
* Supplement Item 不自动进入 pending.md；
* Supplement Item 不得写成已确认产品规则；
* Existing Pending、Supplement Item、Output-Inferred Pending Candidate 必须分层表达，不得混写；
* 不得把 Delivery-Only Boundary 写入 pending.md；
* 交付正文中不得出现 pending.md 或内部路径。
* 交付正文中不使用“已登记”“未登记”“pending”“全局待确认池”等内部管理表达；如需说明待确认状态，应转写为“是否阻塞开发启动”“是否影响验收”“是否属于后续补充边界”。

面向研发正文推荐表达：

```text
当前无阻塞开发启动的产品待确认项。
以下内容属于后续补充边界，主要影响 UI 表达、交互细节、字段精度或验收细节；未补充前，不作为固定开发或验收规则。
```

---

## 14. Visual Expression Boundary

产品交接文档中的视觉相关内容应限定在“表达约束”层面。

允许写：

* 产品语义；
* 展示条件；
* 状态规则；
* 可识别性要求；
* 可区分性要求；
* 必须避免的视觉冲突；
* 不得误导用户的表达；
* 不得抢占主操作权重的约束；
* 视觉待确认项。

不应写死：

* 具体颜色；
* icon 具体造型；
* 动效细节；
* 描边粗细；
* 阴影；
* 圆角；
* 间距；
* 具体视觉风格；
* 具体图标样式；
* 具体动画曲线。

当 active source 中存在颜色、icon、动效、字号、布局位置、圆角、阴影、间距等具体视觉描述，且其本质是状态识别、层级识别、推荐权重、风险提示或标识识别时，面向研发的输出必须转写为产品约束语言。

除非 active source 明确标记为“已确认设计硬约束”，不得将上述视觉描述直接写成强制视觉实现。

推荐表达：

```text
需有明确视觉区分，具体视觉以最终设计稿为准。
需体现主次层级，具体样式以最终设计稿为准。
需与普通状态可区分，具体动效以最终设计稿为准。
```

---

## 15. Product Rule / Expression Constraint / Design Implementation Distinction

### 15.1 产品规则

必须写入产品交接文档。

产品规则包括但不限于：

* 页面目标；
* 区域职责；
* 展示条件；
* 状态切换；
* 字段口径；
* 按钮可用性；
* 数据来源；
* 刷新规则；
* 结果展示规则；
* 验收边界；
* 不覆盖范围。

### 15.2 表达约束

应写入产品交接文档。

表达约束包括但不限于：

* 状态可识别；
* 主次权重清晰；
* 风险提示不误导用户；
* 辅助信息不抢占主操作；
* 不同状态不可混淆；
* 入口能力可被识别；
* 选中 / 未选中 / 禁用 / 弱化 / 推荐等状态可区分；
* 不覆盖已有状态表达。

表达约束应尽量包含可判断标准，例如：

* 可识别；
* 可区分；
* 不抢占主操作注意力；
* 不承载过重信息；
* 不误导用户；
* 不覆盖已有状态表达。

### 15.3 设计实现

不应由产品交接文档写死。

设计实现包括但不限于：

* 指定某一种 icon；
* 固定具体颜色；
* 固定某一种光效；
* 固定描边 / 阴影 / 圆角 / 间距；
* 固定图标风格；
* 固定动画曲线。

具体视觉实现以最终 UI 设计稿或设计系统为准。

产品交接文档不替代 UI 视觉规范。

---

## 16. Output Mode Rules

AI 仅检查输入中的“输出模式”是否明确，不自行判断输出类型。

---

### 16.1 Full Mode Rules

当输出模式 = 全量：

* 输出当前版本完整交接文档；
* 不要求研发依赖上一版；
* 不要求研发通过上一版补上下文；
* 不以“本次变化 / 阅读表达优化 / 产品事实变化”作为主结构；
* 如需说明版本性质，只保留简短表达：

  * `本版本为当前页面口径的完整研发交接，不新增产品规则。`
* 输出对象、输出模式、输出类型等生成参数不进入研发正文主体；
* 全量模式不是摘要型重述；
* 全量模式不是标准版、压缩版、关键点版等中间态；
* 全量模式用于重建当前版本完整交付底座；
* 全量模式必须达到或超过 active source 中仍有效事实的交付颗粒度要求；
* 全量模式输出应能作为当前版本完整实现与验收依据；
* 不要求逐字复制 active source；
* 但不得降低 active source 中仍有效内容的交付颗粒度；
* 不得仅输出模块级、区域级、原则级摘要；
* 不得为了压缩篇幅丢失已确认或仍有效的字段、状态、交互、空状态、验收口径、待确认项；
* 不得为了阅读优化省略用户可见文案；
* 不得把字段表、状态表、交互表、验收表压缩为概括段落。

全量模式至少包含：

1. 文档版本说明；
2. 研发影响标记；
3. 按角色阅读路径；
4. 页面目标；
5. 页面结构；
6. 组件与字段；
7. 核心页面口径；
8. 页面状态；
9. 交互规则；
10. 空状态 / 异常状态；
11. 待确认项 / 待补充项；
12. 验收口径；
13. 不覆盖范围。

如 active source 中存在完整字段表、状态表、交互表、验收表，则全量输出必须保留对应颗粒度。

---

### 16.2 Incremental Mode Rules

当输出模式 = 增量：

* 必须输出完整交接文档上下文；
* 必须在顶部输出“本次版本更新说明”；
* 版本更新说明必须包含：

  * 修改项；
  * 变化类型；
  * 查看位置；
  * 影响范围；
  * 是否需确认；
* “查看位置”必须写为“章节编号 + 章节标题”，且优先指向当前输出文档内章节；
* 如需说明继承关系，可写“沿用上一版口径”，但不得将旧文档作为唯一阅读入口；
* 必须输出“不变更范围声明”；
* 增量模式正文主体结构必须与全量模式保持一致；
* 增量模式应在全量结构基础上增加顶部变更导航，而不是替换正文结构；
* 未变更章节不得删除；
* 未变更章节默认不逐节标注；
* 本次变更涉及章节必须增加清晰标记：

  * `【本次调整】`
  * `【本次新增】`
  * `【本次延续】`
  * `【待确认】`
* AI 只能基于人工输入的“本次变化”决定哪些章节使用以上标记；
* 增量模式不得输出成只有变更清单的摘要文档；
* 增量模式不得默认新增以下一级章节：

  * 继承规则；
  * 本次变更点；
  * 归档说明；
  * 本文使用说明；
  * 阅读顺序；
  * 研发优先阅读顺序。
* 待确认项按当前文档结构完整保留，并对本次变更相关项进行重点标记；
* 若涉及研发高影响模块，必须给出最小实现口径；
* AI 不自行判断旧文档是否可作为底座。

---

## 17. Recommended Full Handoff Structure

全量交付推荐结构：

```text
# {Page} 研发交接文档

## 1. 文档版本说明
## 2. 研发影响标记
## 3. 按角色阅读路径
## 4. 页面目标
## 5. 页面结构
## 6. 组件与字段
## 7. 核心页面口径
## 8. 页面状态
## 9. 交互规则
## 10. 空状态 / 异常状态
## 11. 待确认项 / 待补充项
## 12. 验收口径
## 13. 不覆盖范围
```

说明：

* 可以根据页面复杂度调整二级结构；
* 正文一级章节必须按本结构顺序排列；
* 不得跳过章节编号；
* 不得将后续一级章节放在前序一级章节之前；
* 不得将后续一级章节插入前序一级章节内部；
* 不得创建自嵌套章节；
* 不得为同一章节创建重复标题；
* 如果某章节不适用，应保留章节标题，并写明“不适用”或 prompt 允许的等价说明，不得通过重排章节规避；
* 不能省略核心模块正文；
* 不能用角色阅读路径替代正文；
* 不能用研发影响标记替代正文；
* 不能用验收口径替代字段表和状态表；
* 不能把 active source 中已有的用户可见文案只放在验收口径中。

---

## Delivery Skeleton Stability Rule

Delivery Output must maintain stable delivery skeleton semantics across pages and output modes.

The Full Handoff structure is the default page-level delivery skeleton. It is not an Open Box-specific template and must not be expanded with page-specific top-level sections.

Different pages may have different modules, states, fields, interactions, and acceptance points, but these differences must be organized under the existing delivery skeleton meanings.

A page-specific module, local component, activity card, tab, list, marker system, dialog, state group, or acceptance group must not be promoted to a new top-level section unless this prompt explicitly defines it as part of the shared delivery skeleton.

For the same delivery meaning, use the same top-level section name within the same output type.

Do not rename the same meaning across outputs without a scoped reason.

Examples of stable meanings:

- version and scope -> 文档版本说明
- development impact -> 研发影响标记
- role navigation -> 按角色阅读路径
- page goal -> 页面目标
- page structure -> 页面结构
- fields and copy -> 组件与字段
- confirmed product rules -> 核心页面口径
- states -> 页面状态
- interactions -> 交互规则
- empty and exception states -> 空状态 / 异常状态
- pending and supplement boundaries -> 待确认项 / 待补充项
- acceptance criteria -> 验收口径
- excluded scope -> 不覆盖范围

If a section is not applicable for a page, the output may mark it as not applicable or omit it only when omission does not break the delivery reading path, does not hide confirmed facts, and does not weaken Copy Coverage.

---

## 18. Role-Based Reading Path Rules

全量模式下，“研发影响标记”后可以提供“按角色阅读路径”章节。

按角色阅读路径只承担导航职责，不承担详细规则承载职责。

角色阅读路径不得替代正文主体。

角色阅读路径可包含：

* 前端；
* 后端；
* UI / 设计；
* 测试；
* 运营 / 业务；
* 其它与当前页面相关的角色。

角色路径条目只允许包含：

* 章节编号；
* 章节标题；
* 关注关键词；
* 简短关注说明。

角色路径中不得展开字段表、状态表、交互表、验收清单。

前端阅读路径应指向当前页面中涉及：

* 组件与字段；
* 核心页面口径；
* 页面状态；
* 交互规则；
* 空状态 / 异常状态；
* 验收口径。

后端阅读路径应仅列出当前 active source 中明确涉及后端确认、接口返回、数据来源、配置、结算、刷新、字段口径或联调依赖的内容。

不得为后端默认添加当前页面 source 中不存在的事项。

UI / 设计阅读路径应指向当前页面中涉及：

* 页面结构；
* 组件与字段；
* 页面状态；
* 待确认项 / 待补充项中的设计表达相关章节；
* 产品表达约束；
* 状态识别；
* 视觉冲突避免；
* 待确认视觉项。

测试阅读路径应指向当前页面中涉及：

* 页面状态；
* 交互规则；
* 空状态 / 异常状态；
* 待确认项 / 待补充项；
* 验收口径；
* 不覆盖范围。

角色路径与正文职责分离：

* 角色路径是导航层，不是规则承载层；
* 角色路径不得替代正文；
* 不得因为已有角色路径而压缩字段、状态、交互、空状态、待补充项、验收口径。

### Role-based Density Rule

面向研发的主读路径应优先呈现：

* 接口 / 协作边界；
* 状态判断条件；
* 计算边界；
* 展示 / 不展示条件；
* 验收判定。

UI 视觉细节如颜色、动效、icon 样式、间距、尺寸、视觉层级，在未被确认为实现硬规则时，应放入 UI / 设计阅读路径、待补充项或设计边界说明中。

不得因为压缩而省略已确认的 UI 表达边界。

不得让明确仍待 UI 确认的视觉实现细节过度进入研发主读路径。

---

## 19. Engineering Impact Marker Rules

面向研发输出时，研发影响标记不能只列“关注点”。

高影响模块应根据当前 active source 中的实际内容组织。

每个高影响模块可包含：

* 模块职责；
* 已确认展示口径；
* 关键状态 / 交互；
* 影响侧：前端 / 后端 / 前后端 / UI / 测试；
* 待确认阻塞点；
* 验收关注点。

禁止为当前页面 source 中不存在的模块或事项生成研发影响标记。

禁止仅写：

```text
某模块：关注展示条件、数据来源。
```

推荐表达方向：

```text
某模块：展示口径、职责边界、待确认点与验收关注点成组呈现。
```

---

## 20. CTA / Action State Rules

若 active source 中存在 CTA、按钮、入口、主操作或次操作状态表，必须保留。

按钮 / 入口 / 操作状态表应以“业务状态 + 操作表现 + 触发结果 + 边界”为主，不写死具体视觉实现。

如 active source 中存在推荐态 / 非推荐态 / 弱化态 / 不可用态 / 常驻可点击态，应保留其判定标准。

不得将具体操作状态压缩为：

```text
按钮根据状态变化。
```

推荐态判定标准可包含：

* 视觉权重显著高于非推荐态；
* 用户能识别当前推荐操作；
* 同一时刻仅有一个主要推荐操作。

非推荐态判定标准可包含：

* 保持可识别；
* 视觉权重弱于推荐态；
* 不抢占推荐操作注意力。

不可推荐 / 弱化态判定标准可包含：

* 当前操作不作为推荐动作；
* 当前操作保留或不保留点击能力；
* 点击后的结果按 active source 中已确认规则处理。

不得将以下具体视觉实现写成产品规则：

* 强亮 + 呼吸光效；
* 灰度，无特效；
* 常规亮度；
* 固定颜色；
* 固定动效。

---

## 21. Acceptance Criteria Rules

验收口径必须可以直接转测试用例。

验收口径不得机械复述字段、状态、交互章节原文。

状态表描述事实。

验收口径描述可验证判定。

每一条验收项应能被单条勾选或验证。

验收口径不得逐字复述状态表已有描述。

验收口径应聚焦：

* 触发条件；
* 操作路径；
* 期望展示；
* 不展示场景；
* 边界条件；
* 不覆盖范围。

验收口径应覆盖当前 active source 中仍有效的：

* 页面结构验收；
* 字段展示验收；
* 状态验收；
* 交互验收；
* 空状态验收；
* 范围控制验收；
* 高影响模块相关验收；
* 待确认项不得作为已确认规则进行验收。

如 active source 中存在详细验收口径，且未被 page brief / decisions / pending 否定，全量输出应保留对应颗粒度。

可以合并重复验收项，但不能弱化验收条件、产品边界或减少关键验收覆盖。

验收口径仍必须保留所有：

* 展示 / 不展示检查；
* 状态识别检查；
* 交互触发检查；
* 服务端返回检查；
* 范围控制检查。

### A:view Handling Rule

A:view is an acceptance/check view, not a fact source.

A:view does not participate in Main Fact Anchor selection.

A:view is coverage check only for normal Delivery Output handoff正文.

A:view must not drive repeated正文 expansion.

A:view may be fully expanded only for QA / Acceptance Draft.

A:view must not be used to add rules, states, copy, interactions, or boundaries.

If A:view contains content not supported by F / E / F+E, report governance risk or require human confirmation.

---

## 22. Output Boundary

交付文档是 outputs。

交付文档不是事实源。

生成结果应归档到：

```text
projects/bomcase/outputs/handoff/
```

不得写入：

* sources；
* pages；
* pending.md；
* decisions.md；
* prompts；
* archive。

不得反向覆盖：

* page brief；
* active source；
* decisions；
* pending。

不得读取旧 output 正文作为当前事实依据。

不得从 outputs/handoff 或 _drafts 反推 page brief、source、pending 或 decisions。

不得将 previous outputs、draft outputs、archived outputs 或任何特定生成草稿作为 prompt 结构模板。

仅当用户明确要求评估或对比时，旧输出和草稿输出才可作为问题样例读取；即使读取，也不得作为事实源或结构源。

生成过程中发现的新问题不得自动写入 pending.md，只能作为 pending candidate 输出并等待人工确认。

内部流程术语与知识库治理说明仅用于内部生成控制，不作为交付正文内容。

交付正文中的“验收口径”仅描述产品功能、页面行为、研发实现与测试验收。

不得在正文“验收口径”中写入文档生成质量、版本说明格式、章节索引格式或 prompt 执行情况。

上述生成质量与格式校验内容仅允许出现在生成报告或人工校验报告中，不进入交付正文。

---

## 23. Archive Rule

推荐归档方式：

```text
projects/bomcase/outputs/handoff/YYYY-MM-page-name-handoff-vX.X.md
```

如果只是当前执行版本，优先只归档最新版本。

不强制补齐所有历史版本。

归档文件建议包含 frontmatter 字段：

```yaml
type: delivered_artifact_snapshot
artifact_type: handoff_document
status: archived
version:
delivered_to:
archive_layer:
knowledge_synced:
note: 非事实源，不得反向覆盖知识层
```

frontmatter 可以包含内部归档字段，但交付正文不得展开内部归档说明。

---

## 24. Copy Coverage Failure Report

生成完整交付文档前，必须进行 Copy Coverage 检查。

Copy Coverage 检查 active source 的关键事实是否被覆盖，不检查是否逐段复制 source。

如果同一事实已经在字段、状态、交互或验收口径中完整覆盖，不需要在多个章节机械重复。

但以下内容仍必须保留，不得因阅读压缩而遗漏：

* 用户可见文案；
* 状态触发条件；
* 展示 / 不展示条件；
* 计算边界；
* 服务端返回边界；
* 验收断言；
* 待确认 / 待补充边界；
* non-goals；
* 明确排除项。

### Reading Path Rule Table (v0.3 Information Layer)

| Task | F | E | F+E | A:view | Unknown |
|---|---|---|---|---|---|
| Delivery Output handoff 正文 | 读为正文主事实：规则、条件、边界、触发、结果 | 读为必要用户可见文案与表达约束 | 必须局部拆分：规则进入正文主干，表达进入对应字段 / 状态 / 交互位置 | coverage check only；不作为 Main Fact Anchor；默认不驱动正文扩写 | 不进入确定正文；标记风险并人工确认 |
| Copy Coverage Check | 核对事实是否覆盖 | 核对文案与表达是否覆盖 | 拆分后分别核对事实与表达覆盖 | 仅作为覆盖验证对照；不得反向补事实 | 列入缺口清单，要求人工确认 |
| Acceptance / QA Draft | 可读取并转可测断言 | 可读取并转文案 / 展示断言 | 拆分后可完整展开为 QA 验收项 | 可完整展开，但仅限 QA / Acceptance Draft；需标注为 derived check view | 不得直接写成验收结论；先人工确认 |
| Risk / Exception Report | 作为主风险基线 | 作为表达遗漏风险基线 | 拆分失败即风险项 | 若与 F / E 不一致，报治理风险；若出现新规则，报高风险 | 必报风险；禁止自动归类到 F / E / A:view |

如果发现 active source 中已确认的用户可见文案、字段表、状态表、交互表、验收表被遗漏或被摘要化，必须停止生成完整交付文档，并输出 `Copy Coverage Failure Report`。

如果 readability compression 导致任一关键事实遗漏、被摘要化或关键表格颗粒度下降，必须判定 Copy Coverage 失败，并输出 `Copy Coverage Failure Report`。

`Copy Coverage Failure Report` 必须包含：

```markdown
# Copy Coverage Failure Report

## 1. Failure Type

说明失败类型：

- user-facing copy omitted
- state copy omitted
- info / hover copy omitted
- bottom summary copy omitted
- button copy omitted
- light tip copy omitted
- empty state copy omitted
- field table compressed
- state table compressed
- interaction table compressed
- acceptance criteria compressed

## 2. Missing Content

列出 active source 中已确认但未被当前交付草稿覆盖的内容。

## 3. Source Location

说明缺失内容在 active source 中的大致章节。

## 4. Output Location

说明原本应写入交付文档的章节。

## 5. Required Fix

说明需要补入字段表、状态表、交互表、验收口径或具体文案。

## 6. Generation Status

明确说明：

未生成完整交付文档，需补齐覆盖后重新生成。
```

说明：

* Copy Coverage Failure Report 是生成过程报告，不是交付正文；
* 不得把 Copy Coverage Failure Report 写入研发交付文档正文；
* 若 Copy Coverage 检查通过，正常生成交付文档。

---

## 25. Validation Checklist

生成后必须校验以下内容。

### 25.1 Fact Source Check

* 是否基于最新 page brief；
* 是否读取并校验 page brief 声明的唯一 active source；
* 是否读取 pending.md；
* 是否读取 decisions.md；
* 是否没有读取旧 output 正文作为事实源；
* 是否没有读取 archived source 正文作为事实源；
* 是否没有读取与当前 page 无关的 source；
* 是否没有新增事实；
* 是否没有把输出优化写入事实层；
* 是否没有污染 sources。

### 25.2 Output Mode Check

* 是否已明确输出模式；
* 全量 / 增量是否按人工指定执行；
* 是否没有自行判断轻量或全量；
* 是否没有将增量模式输出成纯变更清单；
* 是否没有将全量模式输出成摘要文档；
* 是否没有将全量模式输出成 source 等长机械搬运；
* 是否在完整事实覆盖前提下完成阅读压缩。

### 25.3 Copy Coverage Check

必须校验：

* 是否完整保留 active source 中已确认的用户可见文案；
* 是否完整保留 active source 中已确认的状态文案；
* 是否完整保留 active source 中已确认的底部汇总文案；
* 是否完整保留 active source 中已确认的 info / hover 文案；
* 是否完整保留 active source 中已确认的按钮文案；
* 是否完整保留 active source 中已确认的入口文案；
* 是否完整保留 active source 中已确认的轻提示文案；
* 是否完整保留 active source 中已确认的空状态文案；
* 是否完整保留 active source 中已确认的结果态文案；
* 是否完整保留 active source 中已确认的示例文案；
* 是否没有把字段表压缩成区域说明；
* 是否没有把状态表压缩成原则说明；
* 是否没有把交互表压缩成动作列表；
* 是否没有把验收口径压缩成方向性条目；
* 是否没有因为阅读压缩遗漏关键事实；
* 是否没有因为去重删除必要边界；
* 是否没有因为验收压缩减少展示 / 不展示、状态识别、交互触发、服务端返回或范围控制检查。

若存在遗漏，必须停止并输出 Copy Coverage Failure Report，不得生成完整交付文档。

### 25.4 Pending / Supplement Check

* 是否保留 pending 为待确认；
* 是否区分 Existing Pending、Source Confirmed Uncertainty、Supplement Item、Output-Inferred Pending Candidate；
* 是否没有把 pending 写成 confirmed；
* 是否没有把 supplement 写成 confirmed；
* 是否没有把生成过程中推断的问题直接写入 pending.md；
* 是否没有减少仍有效待确认项数量；
* 是否没有弱化待确认项影响说明。

### 25.5 Body Language Check

* 正文是否没有内部知识库路径；
* 正文是否没有内部治理语言；
* 正文是否没有 prompt 测试状态；
* 正文是否没有 source / active_source / page brief / outputs / archive 等内部术语；
* 正文是否使用产品 / 研发 / 测试可理解语言；
* 同一概念是否使用统一主表达；
* 用户侧表达和研发侧表达并存时，是否已声明关系；
* 是否没有将“后端 / 服务端”等术语混用为同一含义。

### 25.6 Visual Boundary Check

* 是否没有写死具体颜色；
* 是否没有写死 icon 具体造型；
* 是否没有写死动效细节；
* 是否没有写死描边、阴影、圆角、间距；
* 是否将具体视觉实现转写为产品表达约束；
* 是否保留了状态识别、层级区分、推荐权重、风险提示、标识识别等产品约束。

### 25.7 Readability / Structure Check

* 是否存在重复模块职责说明；
* 是否存在重复研发边界说明；
* 是否存在重复的“不参与 / 不影响 / 以服务端返回为准”表达且无验收必要性；
* 是否存在章节跳号；
* 是否存在一级章节反序；
* 是否存在章节自嵌套；
* 是否存在后续章节插入前序章节内部；
* 是否存在重复标题；
* 是否存在验收项逐字重复状态表描述；
* 是否没有把 v1.2、old output、draft output 或 archived output 的结构固化为当前 prompt 模板。

---

## 26. Standard User Input

```text
页面名称：
输出对象：
输出类型：
输出模式：
目标版本：
本期范围：
本次变化：
确认状态：
是否已完成事实层更新：
```

---

## 27. Standard Generation Report

完成生成后，必须输出生成报告。

生成报告不是交付正文。

生成报告应包含：

```markdown
# Delivery Output Generation Report

## 1. Output File

列出生成文件。

## 2. Sources Read

列出实际读取文件。

## 3. Sources Not Read

确认未读取 archive、old output、draft output、其它页面 source。

## 4. Output Mode

说明输出模式。

## 5. Key Coverage Check

说明是否覆盖：

- 字段表；
- 状态表；
- 交互表；
- info / hover 文案；
- 底部汇总文案；
- 按钮文案；
- 轻提示文案；
- 空状态文案；
- 验收口径；
- 待确认项 / 待补充项。

## 6. Copy Coverage Check

说明是否存在用户可见文案遗漏。

如存在遗漏，不得声称生成完整交付文档，应输出 Copy Coverage Failure Report。

## 7. Information Layer Check

说明：

- 是否检测到 `section_layer` / `layer_note`；
- 若存在，是否按 v0.3 规则消费；
- 若不存在，是否已回退旧规则；
- 是否存在 A:view；
- A:view 用途是 coverage check only 还是 QA / Acceptance expanded；
- 是否存在 F+E；
- F+E 是否执行局部拆分；
- 是否存在 Unknown；
- Unknown 是否进入确定正文；
- 如未消费信息层规则，说明原因。

## 8. Boundary Check

确认：

- 未修改 page brief；
- 未修改 active source；
- 未修改 pending.md；
- 未修改 decisions.md；
- 未修改 prompts；
- 未修改 archive；
- 未读取 old output；
- 未读取 draft output；
- 未读取 archived source；
- 未写入 Fact Patch / Maintenance Log / 内部治理话术到交付正文。

## 9. Risk or Exception

如有异常列出；没有则写“未发现异常”。

## 10. Next Step

只能输出：

- 可以进入人工验收；
- 需要校验与 active source 的覆盖差异；
- 需要回到事实层维护流程；
- 需要修正 Delivery Output Prompt。
```

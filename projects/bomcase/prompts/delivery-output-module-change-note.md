# Delivery Output Module Change Note Prompt

## 1. Purpose

This prompt generates a module-level change note for a confirmed product change.

It is used when the user needs a focused handoff for one module or one local change, instead of a full page handoff or an incremental full-context handoff.

This prompt does not maintain the fact layer.

It must not modify source, page brief, pending, decisions, prompts, outputs, archive, or any other project files.

It must only generate a draft change note based on the current active fact layer.

The output is a developer-readable module change note. It is not a full handoff and not an incremental full-context handoff.

---

## 2. Use Cases

Use this prompt when:

- A single module has changed;
- A local feature rule has been replaced;
- The user wants developers to quickly understand previous background, current confirmed rule, development impact, and acceptance points;
- Full Handoff is too long for practical reading;
- Incremental Handoff still carries too much full-page context;
- The current fact layer has already been updated and validated.

Do not use this prompt when:

- The page has no active source;
- The fact layer has not been updated;
- The change is not confirmed;
- The user needs a full page handoff;
- The user needs an incremental full-context handoff;
- The user needs source / page brief / pending / decisions maintenance;
- The output requires old handoff documents as fact sources;
- The user expects the note to define new product rules not yet written into the fact layer.

---

## 3. Required Inputs

The command must provide:

- `page_name`
- `page_display_name`
- `module_name`
- `target_reader`
- `baseline_handoff_version` or `baseline_fact_layer_version`
- `change_note_version`
- `output_file`
- `change_scope`
- `confirmed_change_summary`
- `unchanged_scope`
- `fact_layer_update_status`

The command may provide:

- `known_previous_background`

Each item in `known_previous_background` must declare its source type.

Allowed source types:

- `historical background provided by user, not authoritative`
- `manually written by user based on team knowledge`
- `transcribed from a prior handoff version, used only as historical context`
- `extracted from the current active source's old-rule exclusion or replacement section`
- `extracted from current decisions / pending`

`known_previous_background` is not automatically authoritative.

The current confirmed rule must always be supported by current active source, decisions, or pending.

If previous background is transcribed from a prior handoff, old output, draft output, archived output, or historical handoff, the output must label it as:

```text
鍘嗗彶鑳屾櫙杈撳叆锛屼笉浣滀负褰撳墠浜嬪疄婧愩€?```

If the command does not provide a safe previous background, the output must omit the previous-background column and only describe the current confirmed rule and development impact.

---

## 4. Required Reading

Must read:

1. This prompt.
2. `projects/bomcase/pages/{page_name}.md`
3. The active source declared by the page brief.
4. `projects/bomcase/pending.md`
5. `projects/bomcase/decisions.md`
6. Necessary global facts, only if required by the page brief, active source, pending, or decisions.

May read:

- No other source unless explicitly required by the page brief, active source, pending, or decisions.

Do not read old outputs, draft outputs, archived outputs, archived sources, or unrelated page sources as fact sources.

---

## 5. Forbidden Fact Sources

Must not use as fact sources:

- old handoff outputs;
- draft outputs;
- archived outputs;
- archived sources;
- `_archive/`;
- README / index / file list;
- unrelated page sources;
- previous generated drafts;
- historical handoff documents;
- screenshots or images not declared as current fact sources;
- user assumptions not written into current fact layer;
- any source not declared active by the current page brief.

Previous outputs may only be read if the user explicitly asks for output comparison.

Even when previous outputs are read for comparison, they may only be used as comparison samples, not as fact sources, not as structure templates, and not as authority for current product rules.

---

## 6. Fact Layer Gate

Before generation, check:

- page brief exists;
- page brief declares an active source;
- active source exists;
- active source matches the target page;
- active source is current / active;
- `fact_layer_update_status` is 鈥滃凡瀹屾垚鈥?or equivalent;
- the requested module exists in current source;
- the confirmed change can be supported by current source;
- pending and decisions do not contradict the requested output.

Stop generation if:

- current source cannot support the change note;
- the change is not in the active source;
- the model needs old output to understand the current confirmed rule;
- the model needs archived source to complete the note;
- the input contains new facts not yet written to the fact layer;
- pending or decisions conflict with the requested output;
- `known_previous_background` is required to establish the current rule;
- `known_previous_background` conflicts with the current active source.

If stopped, output:

# Module Change Note Gate Failure Report

Include:

1. Failure Reason
2. Missing / Conflicting Source
3. Why Generation Cannot Continue
4. Required Next Step

Do not generate the change note if the gate fails.

---

## 7. Output Principles

The output must be short, focused, and developer-readable.

It must answer:

- What changed?
- What is the current confirmed rule?
- What previous understanding should no longer be followed?
- What should frontend do?
- What should backend / server provide or respect?
- What should UI / design know?
- What should testing verify?
- What is explicitly not changed?
- What remains pending?

The output must not become a full page handoff.

The output must not become an incremental full-context handoff.

The output must not reprint full source sections.

The output must not expand unrelated modules.

The output must preserve all critical facts related to the changed module.

The output must use concise tables and short explanatory notes where possible.

---

## Output Language Rule

Module Change Note must be written in Chinese.

Do not use English section titles, English table headers, or mixed Chinese-English structural labels unless the term is a product / technical term already used in the source.

Allowed English terms are limited to existing product / technical terms, file paths, prompt names, or necessary system terms, such as Full Handoff, Change Note, active source, Copy Coverage, baseline, page brief, or output file.

All reader-facing headings, table headers, check items, and report labels must use Chinese.

The output should follow BOMCASE delivery handoff's Chinese product / development handoff style.

注意：

不要强行翻译文件路径、prompt 名称、active source、Copy Coverage 等必要系统术语；
但最终文档的章节名、表头、检查项、报告项必须中文化。
---

## Structure Alignment Rule

Module Change Note is a lightweight variant of BOMCASE delivery handoff.

It may reduce scope and length, but must not introduce a separate document system or a separate reading style.

Module Change Note belongs to the Delivery Output family.

It is a module-scoped variant of Delivery Output, not a separate document system.

It must inherit the same delivery skeleton semantics as the main handoff prompt.

When a section has the same delivery meaning as Full Handoff or Incremental Handoff, use the same Chinese section name or the closest module-scoped equivalent.

Module Change Note may reduce scope and omit non-applicable page-level sections, but it must not create a parallel top-level structure for the same meanings.

Historical background, previous rule comparison, or current rule explanation must be placed under development impact, core module rule, or acceptance-related sections as appropriate. They must not become a separate document skeleton that replaces the Delivery Output structure.

Use module-scoped equivalents where needed:

- 页面目标 -> 模块目标
- 页面结构 -> 模块位置 / 模块结构
- 核心页面口径 -> 核心模块口径
- 页面状态 -> 模块状态

Use the same names where the meaning is unchanged:

- 文档版本说明
- 研发影响标记
- 组件与字段
- 交互规则
- 空状态 / 异常状态
- 待确认项 / 待补充项
- 验收口径
- 不覆盖范围

Naming boundary:

- 不得用“非目标”替代“不覆盖范围”；
- “不变更范围”仅可作为“不覆盖范围”下的子项说明，不得替代一级含义；
- 不得用“研发关注边界”替代“研发影响标记”；
- 不得用“状态与文案”替代“模块状态”；
- 不得用“交互与数据边界”替代“交互规则 + 核心模块口径”。

The output must use Chinese delivery-style headings and tables consistent with BOMCASE handoff documents.

It must remain module-focused and must not become a full handoff or an incremental full-context handoff.

Do not use English-facing structure names such as Version Note, One-screen Summary, Change Comparison, Role Impact, State and Copy, Acceptance Checklist, or Generation Report in the final document.

---

## 8. Previous Background / Current Rule Handling

The output may include a comparison table, but previous rules must be treated as historical background unless explicitly confirmed in the current active source, decisions, or pending.

Allowed uses of previous background:

- help developers understand what changed;
- explain what old understanding should no longer be followed;
- clarify development impact;
- prevent developers from continuing an obsolete interpretation.

Forbidden uses:

- treating previous background as current fact;
- using previous background to override current active source;
- using old handoff, draft output, archived output, or historical output as an authoritative source;
- deriving current rules from previous background;
- presenting old and current rules as a dual-track implementation requirement.

If previous background is transcribed from a prior handoff, old output, draft output, archived output, or historical handoff, the output must label it as:

```text
鍘嗗彶鑳屾櫙杈撳叆锛屼笉浣滀负褰撳墠浜嬪疄婧愩€?```

The authoritative rule must always come from current active source, decisions, or pending.

If previous background conflicts with current active source, current active source prevails.

If the source type of a previous-background item is unclear, do not use it in the comparison table.

---

## Required Output Structure

# {page_display_name} {module_name} 变更说明 {change_note_version}

## 1. 版本说明

必须包含：

- 页面；
- 模块；
- 阅读对象；
- 基准版本；
- 变更说明版本；
- 输出类型；
- 事实层状态；
- 事实依据；
- 生成边界。

## 2. 本次变化摘要

用研发可快速阅读的方式说明：

- 本次变化重点；
- 是否影响前端；
- 是否影响后端 / 服务端；
- 是否影响 UI / 设计；
- 是否影响测试；
- 是否阻塞开发启动。

## 3. 历史背景与当前确认口径

表格前必须写：

```text
“历史背景输入”仅用于帮助理解本次变化，不作为当前事实源；开发、联调与验收以“当前确认口径”为准。
```

如存在安全的历史背景输入，使用：

| 项目 | 历史背景输入（非当前事实源） | 当前确认口径（以此为准） | 研发影响 |
|---|---|---|---|

如无安全历史背景输入，使用：

| 项目 | 当前确认口径（以此为准） | 研发影响 |
|---|---|---|

## 4. 当前模块口径

仅描述当前模块已确认规则，必须由 current active source 支撑。

建议按以下小节组织：

- 模块位置；
- 前台表达；
- 展示条件；
- 数据 / 后端边界；
- 前端展示边界；
- 状态边界；
- 不覆盖内容。

## 5. 研发影响标记

使用表格：

| 角色 | 需要关注 | 不应处理 / 不应推导 |
|---|---|---|

角色必须沿用主 handoff 的角色口径，不得新增主 handoff 未定义角色。

## 6. 模块状态

只列本模块相关状态和文案，不展开整页状态表。

| 状态 | 触发条件 | 前台文案 | 说明 |
|---|---|---|---|

## 7. 交互规则

说明本模块涉及的交互触发、后端返回、前端不可自行推导内容。

不定义接口字段、表结构、服务拆分或算法。

## 8. 验收口径

验收项必须可单条勾选 / 验证。

按以下分组输出：

### 8.1 展示验收

### 8.2 状态验收

### 8.3 交互验收

### 8.4 后端返回边界验收

### 8.5 范围控制验收

## 9. 不覆盖范围

列出容易被误解为本次变化、但实际不调整的范围。

不展开未变更模块完整规则。

## 10. 待补充边界

只列与本模块直接相关的待补充项。

不得新增 pending。

## 11. 非目标（补充，不替代不覆盖范围）

列出本模块变更说明不覆盖的内容。

## 12. 生成报告

使用中文报告结构：

| 检查项 | 结果 |
|---|---|

必须包含：

- 输出文件；
- 已读取来源；
- 未读取来源；
- 事实层门禁；
- 模块覆盖检查；
- 边界检查；
- 风险或异常；
- 下一步。

要求：

- 保留 historical background 非事实源边界；
- 保留 current active source 才是当前确认口径；
- 不新增英文结构；
- 不把 v0.1 的实际输出内容写进 prompt。

---
## 10. Copy Coverage for Module Change

The output must cover all source facts directly related to the changed module.

It does not need to cover unrelated full-page facts.

It must preserve:

- user-facing copy;
- module position;
- display conditions;
- state triggers;
- backend-return boundaries;
- frontend non-derivation rules;
- interaction boundaries;
- acceptance criteria;
- pending / follow-up boundaries;
- non-goals;
- explicit old-rule exclusions;
- confirmed unchanged boundaries that developers may confuse with the changed module.

If any changed-module fact is omitted, distorted, or summarized too aggressively, stop and output:

# Module Change Note Coverage Failure Report

Include:

1. Missing Fact
2. Source Location
3. Why It Matters
4. Required Next Step

The output must not compensate for missing facts by reading old outputs, draft outputs, archived sources, or unrelated files.

---

## 11. Boundary Rules

The output must not:

- modify any file;
- generate a full handoff;
- generate an incremental full-context handoff;
- use old outputs as fact sources;
- infer facts from old outputs;
- infer old rules from archived materials;
- treat historical background as authoritative current fact;
- expand unrelated modules;
- introduce new product rules;
- create pending items;
- create decisions;
- define backend implementation details not confirmed by source;
- define UI visual details not confirmed by source;
- introduce roles not defined by the main handoff prompt or current delivery context;
- imply previous background and current confirmed rule are both valid;
- use baseline handoff version as a fact source unless it is also the current active source or explicitly permitted for comparison only.

---

## Standard Generation Report

At the end of the output, include:

# 模块变更说明生成报告

## 1. 输出文件

写明输出文件路径。

## 2. 已读取来源

只列出实际读取的文件。

## 3. 未读取来源

必须确认以下内容未作为事实源读取：

- old output；
- draft output；
- archived output；
- archived source；
- unrelated source；
- README / index 作为业务事实；
- previous generated drafts。

## 4. 事实层门禁

确认：

- page brief 存在；
- active source 存在；
- active source 支撑本次模块变更；
- pending / decisions 不冲突；
- fact layer update status 为已完成。

## 5. 模块覆盖检查

确认变更说明是否覆盖 active source 中与本模块直接相关的事实。

如未覆盖，输出 `Module Change Note Coverage Failure Report`。

## 6. 边界检查

确认：

- 未修改 source；
- 未修改 page brief；
- 未修改 pending；
- 未修改 decisions；
- 未修改 prompt；
- 未修改 archive；
- 未生成 full handoff；
- 未生成 incremental full-context handoff；
- old output 未作为事实源；
- historical background 未作为当前事实；
- 未展开无关模块。

## 7. 风险或异常

列出风险。

如无，写：

```text
无。
```

## 8. 下一步

Next Step 必须为以下之一：

- 可以进入模块变更内容校验；
- 需要先修 source；
- 需要先修 page brief；
- 需要先修 pending；
- 需要先修 decisions；
- 需要人工确认。

---

## Next Step Values

The only allowed Next Step values are:

- 可以进入模块变更内容校验；
- 需要先修 source；
- 需要先修 page brief；
- 需要先修 pending；
- 需要先修 decisions；
- 需要人工确认。
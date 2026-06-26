# Historical Material Intake Prompt

## 1. Purpose

用于将历史材料受控归位到 Knowledge Vault。

本 prompt 的目标不是直接生成结论，而是帮助判断历史材料的归属、有效性、沉淀方式和后续处理动作。

本 prompt 不承载业务事实，不替代 source，不自动确认 pending，不直接改写 source。

## 2. Required Input

使用本 prompt 前，用户应提供：

```text
材料名称：

材料来源：

材料时间：

材料原文或摘要：

材料类型：
会议记录 / 周报 / 月报 / 聊天记录 / 项目文档 / 管理判断 / AI 工作流 / 其他

初步归属判断：
projects / personal-work / methods / prompts / inbox / 不确定

是否涉及具体项目：

是否涉及 BOMCASE：

是否可能影响后续判断：

是否需要长期复用：
```

## 3. Intake Decision Flow

处理历史材料时，按以下顺序判断：

1. 判断材料是否值得保留；
2. 判断材料归属：

   * 明确属于具体项目 → `projects/xxx/sources/`
   * 明确属于非项目类个人工作 → `personal-work/sources/`
   * 可抽象为通用方法 → `methods/`
   * 可抽象为任务工具 → `prompts/`
   * 归属不明 / 材料混杂 / 有效性不明 → `inbox/`
3. 判断有效性状态：

   * `active`：当前仍有效，可作为当前依据；
   * `expired`：已过期，仅作历史参考；
   * `superseded`：已被后续材料、decision 或 correction 覆盖；
   * `uncertain`：有效性待确认；
4. 判断是否需要生成 brief；
5. 判断是否存在 pending；
6. 判断是否存在 decisions；
7. 判断是否需要 correction；
8. 输出建议动作，不自动执行写入。

## 4. Source Handling Rules

* source 是原始材料层，默认不改写；
* 不直接覆盖 source；
* 不在 source 中直接修改历史表述；
* 不因为 brief 更新而改 source；
* 如果材料存在明显错误，但不会持续影响后续判断，当次说明即可，不建立 correction；
* 只有当错误 source 会持续影响后续判断、复用、汇报或项目口径时，才建议建立 correction；
* correction 默认采用 `source-name.correction.md` 命名；
* 当前不强制建立 `corrections/` 子目录；
* 当同一 sources 目录下 correction 文件达到一定密度，或影响浏览时，再考虑建立 `corrections/` 子目录。

## 5. Brief Generation Rules

如果材料需要生成 brief，brief 应包含：

```text
材料名称：
材料来源：
材料时间：
归属位置：
有效性状态：
核心内容摘要：
可复用信息：
待确认问题：
已形成判断：
关联项目：
是否需要 correction：
备注：
```

## 6. Pending Extraction Rules

以下内容应进入 pending：

* 材料中无法确认但后续需要追踪的问题；
* 影响项目、汇报、管理判断或页面口径的问题；
* 与现有 decisions 冲突但暂未确认的问题；
* 有效性为 `uncertain` 且后续可能复用的信息。

pending 只能作为待确认内容，不得写成已确认结论。

## 7. Decision Extraction Rules

以下内容才适合进入 decisions：

* 已形成明确判断；
* 会影响后续表达、汇报、项目推进或管理动作；
* 可作为后续 AI 输出前提；
* 不是一次性事实；
* 不是尚未确认的猜测。

如判断仍不稳定，应进入 pending，而不是 decisions。

## 8. Correction Decision Rules

建议建立 correction 的情况：

* 原 source 中存在明确错误，且后续可能继续引用；
* 原 source 已被后续事实、会议、决策或版本覆盖；
* 原 source 与当前 decisions 冲突，且冲突会影响后续输出；
* 原 source 涉及团队成员、组织结构、部门方向、项目口径等持续复用信息；
* 原 source 已导致误用，或预计会反复影响同类任务；
* 原 source 被用于生成 brief / decisions，且需要说明旧口径不再适用。

不建议建立 correction 的情况：

* 只是一次性对话误引用；
* 当次纠正即可；
* 表达不完整但不影响后续判断；
* 错误没有持续影响；
* 后续不会再被使用。

## 9. Output Format

每次处理历史材料时，输出：

# Historical Material Intake Result

## 1. Material Summary

## 2. Suggested Destination

## 3. Validity Status

active / expired / superseded / uncertain

## 4. Brief Needed

是 / 否

## 5. Pending Candidates

## 6. Decision Candidates

## 7. Correction Needed

是 / 否

## 8. Suggested Write Actions

只建议，不执行。

## 9. Risks

## 10. Boundary Check

请明确：

* 是否未改写 source；
* 是否未把 pending 当成 decision；
* 是否未把 expired / superseded 当当前事实；
* 是否未自动写入文件；
* 是否仅输出建议动作。

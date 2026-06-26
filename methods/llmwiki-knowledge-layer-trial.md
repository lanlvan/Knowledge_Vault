---
type: method
status: active
version: v1.1
updated: 2026-06-18
---

# LLMWiki 知识层试运行方案

## 1. 文件定位

本文件用于沉淀 LLMWiki 知识层试运行方法，说明如何组织适合 AI 读取和人类维护的轻量知识层，可复用于后续项目、个人工作沉淀和 AI 工作流治理。

- 不替代 `README.md`；
- 不替代 `index.md`；
- 不替代 `workspace-brief.md`；
- 不替代任何项目 `sources/`；
- 不承载具体项目业务事实；
- 不定义完整业务规则。

## 2. 方案版本

- v1.0 是早期知识层试运行方案，偏完整知识资产结构探索；
- v1.1 是基于当前 Knowledge_Vault 正式主库状态的轻量修订版；
- 当前采用 v1.1 作为后续试运行基准；
- 后续如真实使用中发现问题，在本文件内继续更新 v1.2、v1.3，不频繁新增多个版本文件。

## 3. 从 v1.0 到 v1.1 的调整

| 项目 | v1.0 倾向 | v1.1 调整 |
| --- | --- | --- |
| 主库结构 | 编号目录、review/archive、shared、wiki 等较完整结构 | 轻量主库外壳，不恢复重治理目录 |
| 工作台状态 | 偏试点库/探索库 | `F:\Knowledge_Vault\` 作为唯一 active 主工作台 |
| 项目验证 | 以 BOMCASE 为试点 | BOMCASE 成为当前 active 项目样板 |
| 事实判断 | 强调 confirmed 状态 | `sources/` 是事实源，`brief` 是摘要，`pending` 是未确认，`decisions` 是判断 |
| 通用资产 | shared / workflows / templates / rules | `methods/` 放方法，`prompts/` 放通用 prompt，不恢复 shared |
| AI 工具 | 避免 AI 扩散读取 | AI / Codex 可在明确范围和禁改项下受控使用 |
| 试运行目标 | 验证知识库结构 | 验证真实工作中的资料归位、AI 读取、pending/decisions 运转 |

## 4. 当前推荐知识层结构

当前主库结构：

- `README.md`：说明这个库是什么、怎么用、边界是什么；
- `index.md`：列当前有什么、状态如何、去哪找；
- `workspace-brief.md`：说明这个工作台为什么这样设计、经历过什么版本、后续如何演进；
- `inbox/`：临时资料入口；
- `projects/`：项目知识工作台；
- `methods/`：通用方法沉淀；
- `prompts/`：通用 AI prompt；
- `personal-work/`：非项目类个人工作沉淀。

项目层推荐结构：

- `README.md`：项目入口；
- `project-brief.md`：项目摘要；
- `business-brief.md`：业务语境摘要，不替代 source；
- `pending.md`：待确认问题；
- `decisions.md`：判断记录；
- `sources/`：事实源；
- `pages/`：页面摘要；
- `prompts/`：项目专用 prompt。

补充：新项目不强制一次性建满，按真实资料和真实使用增量补齐。

## 5. 文件职责分工

| 文件/目录 | 职责 | 是否事实源 |
| --- | --- | --- |
| `README.md` | 使用说明、边界、读取顺序 | 否 |
| `index.md` | 当前内容索引、路径导航 | 否 |
| `workspace-brief.md` | 工作台背景、版本、设计取舍 | 否 |
| `project-brief.md` | 项目摘要 | 否 |
| `business-brief.md` | 业务语境摘要 | 否 |
| `sources/` | 原始交接文档、事实来源 | 是 |
| `pages/` | 页面级摘要与交接压缩 | 否 |
| `pending.md` | 未确认问题 | 否 |
| `decisions.md` | 已形成判断 | 是，限判断记录 |
| `methods/` | 通用方法 | 否 |
| `prompts/` | AI prompt 工具 | 否 |
| `inbox/` | 临时资料入口 | 否 |
| `personal-work/` | 非项目类工作沉淀 | 视具体文件而定 |

## 6. AI 读取原则

- AI 应先读 `README.md`，再读 `index.md`；
- 需要理解工作台背景时读 `workspace-brief.md`；
- 进入项目时先读项目 `README.md`；
- 需要项目概况时读 `project-brief.md`；
- 需要业务语境时读 `business-brief.md`；
- 需要页面摘要时读 `pages/`；
- 需要未确认问题时读 `pending.md`；
- 需要已形成判断时读 `decisions.md`；
- 需要核对事实时必须读 `sources/`；
- AI 不应默认全库扫描；
- AI 不应把 README / index / workspace-brief 当事实源；
- AI 不应把 pending 当已确认结论；
- AI 不应把 prompt 当业务事实。

## 7. Codex 使用原则

- Codex 可以用于本地文件整理、结构校验、受控写入；
- 每次 Codex 输入必须明确目标目录；
- 每次 Codex 输入必须明确允许读取、允许新增、允许修改、禁止修改；
- 涉及项目 source、pending、decisions、business-brief 时必须谨慎；
- Codex 不应自动确认业务事实；
- Codex 不应改写 source 原文；
- Codex 不应无范围扫描或重构整个知识库；
- Codex 输出后需要由用户或 AI 再做一次校验。

## 8. 试运行成功标准

当前 v1.1 的试运行重点不是继续搭目录，而是验证真实使用。

建议成功标准：

1. 新资料能快速判断放入 inbox / projects / methods / prompts / personal-work；
2. AI 能通过 README + index + 项目 README 快速进入上下文；
3. 项目事实能回到 sources；
4. 页面摘要能回到 pages；
5. 待确认问题能进入 pending；
6. 已形成判断能进入 decisions；
7. README / index / workspace-brief 不被误当事实源；
8. methods / prompts / personal-work 不为了完整性而空转扩张；
9. 不恢复 rules / archive / review / workflow 等重结构；
10. 真实使用中能减少重复解释和上下文丢失。

## 9. 调整原则

- 优先调整文案，不优先调整目录；
- 优先新增真实内容，不优先新增结构；
- 优先解决真实问题，不做想象中的完整性补齐；
- 不恢复 v1.0 的编号目录；
- 不恢复 rules / archive / review / shared / templates / workflow；
- 不把单次聊天内容直接当长期事实；
- 不把通用方法写成项目事实；
- 不把项目摘要写成事实源。

## 10. 适用范围

本方法适用于：

- Knowledge_Vault 主库维护；
- BOMCASE 这类项目交接资料沉淀；
- 后续新项目知识层搭建；
- 团队管理、月报、复盘等个人工作资料沉淀；
- AI / Codex 辅助整理本地 Markdown 知识库。

不适用于：

- 完整企业知识库治理；
- 严格审计型文档系统；
- 需要权限、审批、归档流的正式制度库；
- 未经人工校验的自动事实生成。

## 11. 后续版本维护

- 后续版本在本文件内更新；
- 不频繁新增多个版本文件；
- 只有当知识层结构、AI 读取原则、Codex 使用边界、文件职责分工发生明显变化时，才更新版本；
- 小的文案修正不必升版本；
- 真实试运行后如发现问题，可更新为 v1.2。

## 12. 版本记录

| 日期 | 版本 | 说明 |
| --- | --- | --- |
| 2026-06-18 | v1.0 | 原始 LLMWiki 知识层试运行方案，偏完整知识资产结构探索 |
| 2026-06-18 | v1.1 | 基于正式 Knowledge_Vault 轻量主库状态修订，明确当前文件职责、AI 读取原则和 Codex 受控使用原则 |

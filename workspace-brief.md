---
type: workspace_brief
status: active
updated: 2026-06-26
---

# Workspace Brief

## 1. 文件定位

说明：

* 本文件记录 Knowledge_Vault 的背景、作用、版本演进和设计取舍；
* 用于帮助用户和 AI 在遗忘上下文时快速理解这个工作台；
* 不替代 `README.md`；
* 不替代 `index.md`；
* 不替代任何 source；
* 不承载具体项目事实；
* 不定义完整业务规则。

## 2. 当前主库定位

说明：

* Knowledge_Vault 是当前唯一 active 的个人 LLM+ / LLMWiki 工作台；
* 面向人类阅读，也面向 AI 读取、复用、校验和持续迭代；
* 用于沉淀项目 source、brief、pending、decisions、business brief、methods、prompts 与个人工作资料；
* 当前不追求完整业务规则库，也不追求复杂 workflow 治理系统。

## 3. 背景

概括说明：

* 早期存在 V1 探索版本；
* V1 混合了项目资料、页面交接、shared rules、workflow templates、review/archive 等治理结构；
* V1 对资料整理有帮助，但对个人日常使用和 AI 读取来说偏重；
* 后续通过 BOMCASE 试点，收敛为轻量 LLM+ / LLMWiki 主库。

## 4. 版本演进

| 阶段 | 定位 | 主要特点 | 当前状态 |
|---|---|---|---|
| V1 探索期 | 重结构知识库探索 | 编号目录、rules、workflow、review/archive 等结构较重 | 已退出 active |
| V2 试点期 | BOMCASE 轻量项目工作台 | source / page brief / pending / decisions 闭环形成 | 已并入正式主库 |
| 正式主库期 | 个人 LLM+ / LLMWiki 工作台 | README + index + workspace-brief + projects/inbox/methods/prompts/personal-work | 当前 active |

## 5. 当前结构方案

说明当前根目录结构：

* `README.md`：说明这个库是什么、怎么用、边界是什么；
* `index.md`：列当前有什么、状态如何、去哪找；
* `workspace-brief.md`：说明背景、版本、设计取舍和演进方式；
* `inbox/`：临时资料入口；
* `projects/`：项目知识工作台；
* `methods/`：通用方法沉淀；
* `prompts/`：通用 AI prompt；
* `personal-work/`：非项目类个人工作沉淀。

## 6. 核心设计原则

说明：

* source 是事实源；
* brief 是摘要；
* business-brief 是业务语境说明，不替代 source；
* pending 记录未确认问题；
* decisions 记录已形成判断；
* README / index / workspace-brief 都不是事实源；
* prompts 是辅助工具，不承载业务事实；
* inbox 只是临时入口，不作为长期归档；
* 只按真实使用需要增量补充，不预建大量空目录。

## 7. 当前 active 项目

说明：

* BOMCASE 是当前第一个 active 项目；
* BOMCASE 也是当前项目结构样板；
* BOMCASE 已包含 README、project-brief、business-brief、pending、decisions、sources、pages、prompts；
* 后续新项目可以参考 BOMCASE 的最小结构，但不要机械复制不需要的内容。

## 8. 当前治理状态

说明：

* Knowledge_Vault 已完成第一轮结构治理；
* decisions 已拆分为根级工作台级 decisions 与项目级 decisions；
* pending / decisions / page brief / source 的职责边界已明确；
* BOMCASE 已完成项目级 pending 清洗与 page brief role 分层；
* 具体项目判断以对应项目 `decisions.md` 为准。

## 9. 后续演进方式

说明：

* 新项目进入 `projects/`；
* 临时资料先进入 `inbox/`；
* 通用方法进入 `methods/`；
* 通用 prompt 进入 `prompts/`；
* 非项目工作沉淀进入 `personal-work/`；
* 项目事实进入对应项目 `sources/`；
* 页面摘要进入对应项目 `pages/`；
* 未确认事项进入 pending；
* 已形成判断进入 decisions；
* 导航变化更新 README / index。

## 10. 明确不做什么

说明：

* 不恢复编号目录；
* 不恢复 `rules` / `archive` / `review` / `shared` / `templates` / `workflow` 重结构；
* 不把 prompt 当事实源；
* 不把 README / index 当事实源；
* 不把 workspace-brief 当事实源；
* 不把 business-brief 写成完整业务规则；
* 不为“看起来完整”创建大量空目录；
* 不把单次对话内容直接当长期知识沉淀。

## 11. 版本记录

| 日期 | 版本 | 说明 |
|---|---|---|
| 2026-06-26 | workspace-v1.1 | 补充当前工作台第一轮结构治理状态，明确治理分层与项目级判断引用边界 |
| 2026-06-18 | workspace-v1.0 | 正式主库完成改名、轻量主库外壳补齐，并新增 workspace-brief 记录背景与设计取舍 |

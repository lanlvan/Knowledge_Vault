# Obsidian Light Maintenance Method

## 1. Purpose

本文件用于说明如何使用 Obsidian 对 Knowledge Vault 进行日常轻量维护。

Obsidian 的角色是：

- 人工阅读界面；
- Markdown 维护界面；
- 信息状态分层管理界面；
- 少量链接与关系辅助工具。

Obsidian 不是新的流程系统，不替代 Knowledge Vault 的目录结构，不替代 AI prompt，也不替代受控写入流程。

## 2. Role Definition

Knowledge Vault 的分工如下：

| 层级 | 角色 |
|---|---|
| Knowledge Vault | 文件结构、信息分层、AI 可读规则 |
| Obsidian | 人工阅读、维护、链接、信息状态管理 |
| AI / Prompt | 按任务读取、生成、校验、提炼 |
| Cursor / Codex | 受控写入、结构性修改、批量文件操作 |

## 3. What Obsidian Can Maintain Directly

以下内容适合用 Obsidian 日常维护：

- 公司结构；
- 团队人员；
- 部门方向；
- 周报 / 月报 brief；
- 会议纪要；
- 管理判断草稿；
- AI 工作流笔记；
- pending 的人工补充；
- brief 的轻微修正；
- inbox 中的临时材料整理。

这些内容通常属于 personal-work 或 methods 层，不应默认影响具体项目 facts。

## 4. What Should Not Be Edited Casually

以下内容不建议在 Obsidian 中随手修改：

- source 原文；
- 已作为项目事实依据的 source；
- BOMCASE 项目 decisions；
- 明确影响项目口径的 page brief；
- 已经作为 AI 当前事实入口的核心口径文件；
- prompts 中正在稳定使用的任务模板；
- README.md / index.md / workspace-brief.md 等顶层结构说明。

如果必须修改上述内容，应优先走受控修改方式，并说明修改原因、影响范围和边界。

## 5. Information Status Layer

对复杂材料，建议在 brief 中使用信息状态分层。

推荐状态：

| 状态 | 含义 | AI 调用方式 |
|---|---|---|
| `confirmed` | 相对确定，可作为背景事实使用 | 可用于分析、汇报、上下文 |
| `current_observed` | 当前观察到的现状，但可能变化 | 可用于阶段判断，但需标注时间点 |
| `historical` | 历史发生过，但不代表当前仍有效 | 只能作为历史背景 |
| `unconfirmed` | 未确认、私下消息、传闻、疑似关系 | 只能作为风险或待确认事项 |
| `conflict_or_pending` | 存在口径冲突、日期矛盾、需核对 | 只能进入 pending，不可作为结论 |

建议在重要 brief 中使用如下结构：

```md
## Information Status Layer

### confirmed

### current_observed

### historical

### unconfirmed

### conflict_or_pending
```

## 6. Daily Maintenance Flow

日常维护时，不默认完整 intake。

优先使用轻量分级：

| 级别 | 场景 | 处理方式 |
| -- | ----------------- | --------------------------------------- |
| L0 | 无复用价值 | 不入库 |
| L1 | 价值或归属不确定 | 放入 inbox |
| L2 | 后续可能复用 | source + brief |
| L3 | 影响判断、汇报、项目口径或协作边界 | source + brief + pending / decisions 候选 |

日常建议：

1. 临时信息先进入 inbox；
2. 有复用价值的信息整理为 brief；
3. 影响判断的信息再考虑 pending / decisions；
4. 影响项目口径的信息走受控写入；
5. 不因一条信息就扩目录或新建项目。

## 7. Obsidian Linking Rules

初期只使用少量必要链接，不做大规模双链化。

建议链接：

* `[[personal-work/information-map]]`
* `[[personal-work/decisions]]`
* `[[personal-work/pending]]`
* `[[projects/bomcase/README]]`
* `[[methods/obsidian-light-maintenance]]`

不建议：

* 为所有文件强制加双链；
* 为所有人名建立独立页面；
* 为所有会议建立复杂关系图谱；
* 过早使用大量标签；
* 把 Obsidian 图谱当成知识库目标。

## 8. Boundary Rules

* Obsidian 用于轻维护，不用于绕过受控流程；
* source 默认不改写；
* pending 不等于 decision；
* brief 不等于 source；
* information-map 是分类地图，不是事实源；
* prompts 是工具，不承载业务事实；
* 项目资料默认进入 `projects/{project}/`；
* personal-work 承接非项目类个人工作信息；
* 不因 Obsidian 使用而恢复重结构。

## 9. Current Stage

当前阶段只建议：

1. 用 Obsidian 打开 Knowledge Vault；
2. 浏览 README / index / workspace-brief；
3. 重点查看 `personal-work/information-map.md`；
4. 对少数重要 brief 使用 Information Status Layer；
5. 暂不批量建标签、双链、图谱或独立人名页；
6. 等真实使用一段时间后，再判断是否需要拆分 reports / meetings / management 等目录。

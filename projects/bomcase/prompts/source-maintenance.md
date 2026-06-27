# Source Maintenance Prompt

根据用户提供的 Fact Patch，更新指定 active source。

## 规则

1. 只写 Fact Patch 明确列出的内容。
2. 只修改 Fact Patch 指定的目标文件。
3. 不读 archive、不读 outputs、不读 old output / draft output、不读其它页面。
4. 不改 page brief、pending.md、decisions.md、delivery prompt、outputs、archive。
5. Fact Patch 中包含具体视觉实现时，除非明确标记为“设计硬约束”，否则转写为产品约束语言。例如：
   - 颜色 → 需有明确视觉区分，具体颜色以最终设计稿为准
   - icon → 需有明确标识，具体 icon 样式以最终设计稿为准
   - 动效 → 需与普通状态可区分，具体动效以最终设计稿为准
6. 如果 Fact Patch 与当前 source 冲突，不要强行覆盖，列入未写入。
7. 如果 Fact Patch 中有空缺、未确认或仅建议内容，不要自行补写，列入未写入。
8. 完成后在 source 中追加轻量 log：
   - 如果目标 source 已有 `Maintenance Log` 或类似维护日志章节，则追加到该章节。
   - 如果目标 source 没有维护日志章节，则在文末新增 `## Maintenance Log`。
   - log 只记录事实层维护摘要，不写交付文档话术，不展开详细变更表。
   `YYYY-MM-DD | 类型 | 摘要`

## 输出格式

# Source Maintenance Report

## 1. 修改文件

- 

## 2. 写入章节

| 内容 | 写入位置 |
|---|---|
|  |  |

## 3. 未写入内容

| 内容 | 原因 |
|---|---|
|  |  |

## 4. Log

说明已追加的 log 内容。

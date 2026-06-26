# Personal Work Decisions

用于记录非项目类个人工作中已形成的判断。

## 当前判断记录

### Decision: 采用“轻框架搭建与历史信息归位”作为下一阶段

- 状态：进行中
- 阶段命名：Knowledge Vault v0.3（暂定）
- 判断内容：
  当前不采用“单模块慢跑”或“一次性完整搭建”的方式，而采用轻框架方式推进：
  先补齐可承接主要信息类型的最小结构，再输入历史材料做第一轮归位和沉淀。

- 适用范围：
  - index 状态修正；
  - personal-work 最小闭环；
  - inbox 出口机制；
  - 历史材料有效性判断；
  - source correction 低频机制；
  - sources / briefs / pending / decisions 分层；
  - Codex / Cursor 受控执行；
  - 任务型 prompt 初步建立。

- 不包含：
  - GBrain 接入；
  - Obsidian 双链批量改造；
  - 全量知识图谱；
  - 周报/月报/会议等复杂目录一次性展开；
  - BOMCASE 项目重构。

- 完成条件：
  1. index.md 已修正 methods 状态偏差；
  2. personal-work 已具备 sources / briefs / pending / decisions 最小承接结构；
  3. inbox 已定义入口与出口机制；
  4. 历史材料有效性状态已明确；
  5. 至少 5 份历史材料完成归位；
  6. 至少 5 份历史材料均生成 brief；
  7. 已从历史材料中提取 pending 与 decisions；
  8. 已建立至少 1 个任务型 prompt；
  9. 已跑一次日报 / 汇报 / 会议准备场景验证；
  10. 完成后判断是否需要进一步拆分 reports / meetings / management 等目录。

- 后续判断：
  若历史材料集中在某一类信息上，再决定是否新增二级目录。

### Decision: 个人工作沉淀需要承接部门方向与管理判断

- 状态：active
- 判断内容：
  后续个人工作沉淀不应只围绕单一项目进度展开，还需要承接部门方向、团队协作、管理判断、AI 工作流治理、周/月报与向上汇报材料。

- 背景：
  过去部分工作内容容易散落在对话、周报、会议记录或项目材料中，导致 AI 在新对话中无法稳定读取这些前提。
  例如部门方向、协作判断、项目责任边界、AI 使用边界、团队管理口径等信息，如果不进入 personal-work，后续生成日报、周报、月报或会议材料时容易缺少长期上下文。

- 适用范围：
  - 部门信息；
  - 周报 / 月报 / 日报；
  - 会议纪要；
  - 团队管理；
  - 绩效 / Owner 制；
  - AI 工作流治理；
  - 跨项目协作判断；
  - 向上汇报材料；
  - 非单一项目的个人工作判断。

- 不适用范围：
  - BOMCASE 页面事实源；
  - BOMCASE 项目页面交接；
  - BOMCASE 项目业务语境；
  - 具体项目 source；
  - 具体项目 pending / decisions。

- 使用规则：
  后续当材料属于非单一项目的管理判断、部门方向或个人工作复盘时，应优先判断是否进入 `personal-work/decisions.md`、`personal-work/briefs/` 或 `personal-work/pending.md`，不默认塞入 `projects/bomcase/`。

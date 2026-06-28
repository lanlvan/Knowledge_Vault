# Create Page Brief Prompt

使用场景：

* 日常高频使用；
* 新增页面时，基于 source 生成 page brief；
* 页面资料更新后，基于 source 更新对应 page brief；
* 需要把 source 信息整理为可读的页面工作摘要时使用。

不适用场景：

* 不用于沉淀完整业务规则；
* 不用于批量迁移历史规则原结构；
* 不用于自动确认事实。

用途：基于当前 source 与当前项目文档（pages / pending / decisions），为单个页面生成轻量 page brief。

输入：

* source path（示例：`F:\Knowledge_Vault\projects\bomcase\sources\home.md`）
* 相关页面已有 page brief path（如存在）
* pending / decisions 关联 path（如存在）
* output page brief path（示例：`F:\Knowledge_Vault\projects\bomcase\pages\home.md`）

要求：

1. 只生成一个页面 brief；
2. 不新增 source 未确认事实；
3. 不照搬历史规则文件结构；
4. 明确来源；
5. 标注待确认项；
6. 标注不覆盖范围；
7. page brief 是工作摘要，不是正式业务规则；
8. 不要求依赖旧路径回查；
9. 不自动补旧资料内容。

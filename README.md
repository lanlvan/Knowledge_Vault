# Knowledge Vault

## 1. 定位

说明：

* 这是当前唯一 active 的个人项目知识工作台；
* 用于沉淀项目 source、brief、pending、decisions、business brief、methods、prompts 与个人工作资料；
* 面向人类阅读，也面向 AI 读取和复用；
* 不是完整业务规则库；
* 不是文件归档仓库；
* 不是复杂 workflow 治理系统。

## 2. README 与 index 的分工

* `README.md`：说明这个库是什么、怎么用、边界是什么；
* `index.md`：列当前有什么、状态如何、去哪找；
* `workspace-brief.md`：说明背景、版本演进、设计取舍和后续演进方式。

## 3. 目录说明

* `index.md`：当前内容索引；
* `workspace-brief.md`：主库背景与演进说明；
* `inbox/`：临时资料入口；
* `projects/`：项目知识工作台；
* `methods/`：通用方法沉淀；
* `prompts/`：通用 AI prompt；
* `personal-work/`：非项目类个人工作沉淀。

## 4. 事实层级

* source 是事实源；
* brief 是摘要；
* business-brief 是业务语境说明，不替代 source；
* pending 是待确认；
* decisions 是判断记录；
* README / index 是导航，不是事实源；
* prompts 是辅助工具，不承载业务事实。

## 5. 日常读取顺序

1. 先读 `README.md`；
2. 再读 `index.md`；
3. 然后读 `workspace-brief.md`；
4. 进入具体项目 `README.md`；
5. 读 `project-brief.md` / `business-brief.md`；
6. 按任务读 `pages/` / `pending.md` / `decisions.md`；
7. 需要核对事实时读 `sources/`。

## 6. 新增内容原则

* 新项目进入 `projects/`；
* 临时资料先放 `inbox/`；
* 通用方法进入 `methods/`；
* 通用 prompt 进入 `prompts/`；
* 非项目工作沉淀进入 `personal-work/`；
* 不确定内容先进入 `pending`；
* 已形成判断进入 `decisions`。

## 7. 不恢复 V1 重结构

* 不使用编号目录；
* 不恢复 `rules` / `archive` / `review` / `shared` / `templates` / `workflow` 重结构；
* 后续按真实使用需要增量补充。

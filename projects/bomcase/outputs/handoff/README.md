# BOMCASE Handoff Outputs

## 1. Purpose

说明：

本目录用于归档 BOMCASE 项目已确认交付的交接文档或交付物。

## 2. Boundary

* 本目录是 outputs 层；
* 本目录不是事实源；
* 本目录默认只读归档，不承载知识库实时更新；
* 本目录内容不得反向覆盖 `../../pages/`、`../../decisions.md`、`../../pending.md`、`../../sources/`；
* 新交付件归档到这里，不再放入 `../../sources/`；
* 历史已存在于 `../../sources/` 的 `*-handoff.md` 保持不动，作为 historical source material。

## 3. Write Rule

说明：

只有经过 `Delivery Output Loop` 生成并人工确认的交付物，才允许归档到本目录。

## 4. Recommended Naming

命名建议：

* `YYYY-MM-page-name-handoff-vX.X.md`
* `YYYY-MM-page-name-handoff.md`

补充说明：

* 同迭代多次更新可使用版本号；
* 跨迭代可使用月份或迭代标识；
* 不强制预建页面子目录，必要时再创建。

## 5. Relationship With Sources

* `sources/` 保存原始事实材料；
* `outputs/handoff/` 保存交付物快照；
* 两者不得混用；
* 如交付物中出现新的事实缺口，应先回到 `Knowledge Update Loop` 更新知识库，而不是直接在 outputs 中补事实。

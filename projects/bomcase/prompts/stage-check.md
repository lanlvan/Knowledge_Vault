# Stage Check Prompt

使用场景：

* 阶段性结构检查（低频）；
* source / page brief / pending / decisions 一致性检查；
* 新增页面或新项目后的只读校验。

不适用场景：

* 不用于自动修复；
* 不用于自动删除；
* 不用于自动迁移；
* 不用于自动确认事实。

用途：只读检查当前主工作台结构是否清晰、source 是否可追溯、page brief / pending / decisions 是否一致且可独立运行。

检查：

1. 是否存在必要 README；
2. source 是否存在；
3. page brief 是否引用 source；
4. pending 是否集中；
5. decisions 是否清楚；
6. 是否还存在旧路径 active 依赖；
7. 是否误写 source 未确认事实；
8. 是否把 pending 未确认项误写为已确认；
9. 是否创建了无用空壳目录。

完成后输出：

1. 修改的文件清单；
2. 新增的文件清单；
3. 是否修改旧路径目录；
4. 是否修改 source 原文；
5. 是否修改 pending；
6. 是否删除、移动或改名文件；
7. pages 是否仍含旧版引用字段；
8. 是否仍有旧路径引用；
9. 是否新增超出范围的新目录；
10. business-brief 是否保持轻量语境定位；
11. decisions 是否有新增判断记录；
12. 下一步建议。

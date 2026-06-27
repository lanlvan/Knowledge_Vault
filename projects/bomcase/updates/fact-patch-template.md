# Fact Patch


页面：open-box  
目标文件：projects/bomcase/sources/open-box.md  
类型：confirmed_fact_add

补充内容：

右侧卡牌背包全展开态在未选卡牌时，不应只描述为“不展示底部已选消耗说明”，需要根据当前开启满足状态展示对应底部文案：

- 需要补能量，未选卡：`已选 0 张｜选择卡牌后填充能量`
- 赠品次数已满足，未选卡：`赠品次数已满足，暂无需填充`
- 开启能量已满足，未选卡：`开启能量已满足，暂无需填充`
- 已有选择：`已选 N 张｜填充 +X%｜清除已选`
- 已有选择补充说明：`已选卡牌将在开启时消耗`
- 已有选择且存在能量溢出：`已选卡牌将在开启时消耗，溢出 +Y% 存入能量余额`



2. 补充资源参与口径中的单 icon 场景文案规则。

补充内容：

资源参与口径需补充以下规则：

- 当仅有 1 个资源 icon 时，使用完整资源名称文案。
- 示例：`赠品次数 ×1`


3. 补充资源概览 info、能量余额 info、即将过期能量 hover 的文案。


补充内容：

资源概览 info 文案：

`展示账号当前与开启军需相关的资源概览，具体开启判断以中间区域为准。`

能量余额 info 文案：

`能量余额为账号当前已有能量，可用于补足开启满足度。开启时将优先消耗本次填充卡牌产生的能量，具体消耗以开启结果为准。`

即将过期能量 hover 文案：

`即将过期能量为近期可能失效的能量，请在有效期内使用。具体过期时间以系统记录为准。`


## 不写入事实层

- 

## 不做

- 不改 page brief
- 不改 pending.md
- 不改 decisions.md
- 不改 delivery prompt
- 不改 outputs
- 不读 archive
- 不读 old output / draft output
- 不改其它页面

## 类型说明

可选类型：

- `confirmed_fact_add`：已确认事实补充
- `confirmed_fact_fix`：已确认事实修正
- `confirmed_fact_remove`：已确认事实删除
- `expression_cleanup`：事实表达净化，不改变产品规则
- `supplement_add`：新增待补充边界
- `pending_candidate`：待确认候选，不直接写入 source

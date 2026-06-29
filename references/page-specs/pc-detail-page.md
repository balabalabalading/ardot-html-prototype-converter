# PC 详情页规范

适用于只读对象详情、单据详情，以及包含一个或多个子表的详情页面。

## 结构

`Content` 通常包含：

1. `TitleBar`
2. 一个或多个 `InfoCard`
3. 可选 `SubTable`
4. 可选 `ActionBar`

`Content` 是普通 frame，四周 padding 为 `24`，使用纵向 auto layout。页面自有区块水平 padding 为 `0`，圆角为 `0`。

## TitleBar

- 直接在 `TitleBar` 节点自身设置 `border-default` 底部描边。
- 不新增子节点模拟边框。
- 放置标题，以及源页面可见的返回或操作。

## InfoCard

- 每个逻辑信息分组使用一个 `InfoCard`。
- InfoCard 是普通 frame；除非系统已有匹配的本地卡片组件模式，否则不转组件。
- 卡片标题使用主要文本色。
- 字段使用 `label + value` 成对呈现。
- label 不使用 `:` 或 `：`。
- label 使用次要文本色。
- value 使用主要文本色。
- 字段行和换行使用 auto layout。
- 状态值使用语义色，例如成功、错误、警告或主色。

## SubTable

- 详情页子表沿用列表表格规则：`Table -> table column 组件实例`。
- 使用本地 table column 组件。
- 生成可编辑表格时，不使用 row/cell 容器。
- 如果源页面没有独立筛选或分页，子表可以不带 FilterBar/Pagination。
- 子表字段和样例行来自渲染证据。

## ActionBar

- 只放源页面中可见的操作。
- 主操作使用 Button `base / medium / primary`。
- 次要操作按需使用 Button `outline / medium / primary`。

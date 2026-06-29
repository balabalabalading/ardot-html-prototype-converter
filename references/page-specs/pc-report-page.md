# PC 报表页规范

适用于统计、汇总、审核报表、经营报表等以报表内容为主体的页面。

## 结构

`Content` 直接包含以下区块，顺序固定：

1. `TitleBar`
2. `FilterBar`
3. `ReportArea`

`Content` 是普通 frame，四周 padding 为 `24`。内部区块水平 padding 为 `0`，圆角为 `0`。

## TitleBar

- 直接在 `TitleBar` 节点自身设置 `border-default` 底部描边。
- 不新增子节点模拟分隔线。

## FilterBar

沿用 PC 列表页的 FilterBar 规则：

- 字段容器命名为 `Field / 字段名`。
- label 不使用 `:` 或 `：`。
- 字段宽度通常为 `240`。
- 隐藏 Input tips。
- 必须包含 `查询` 和 `重置` 按钮。
- 查询按钮：`base / medium / primary`。
- 重置按钮：`outline / medium / primary`。

## ReportArea

根据源页面证据选择报表形态：

- 表格型报表：使用 `Table -> table column 组件实例`，可能溢出时开启表格容器裁剪。
- 指标型报表：本地存在 Statistic 或 Card 组件时优先使用。
- 文本型报表：用分组 Text 节点组织，并放入清晰的容器。
- 混合型报表：拆成命名子区块，例如 `MetricArea`、`ReportTable`、`SummaryText`。

不要把报表数值直接散放在 `Content` 下。每个逻辑报表块都放入命名 auto-layout 容器。

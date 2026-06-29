# PC 表单页规范

适用于新增、编辑、提交、审批、配置等以输入字段为主体的页面。

## 结构

`Content` 直接包含以下区块，顺序固定：

1. `TitleBar`
2. `FormArea`
3. `ActionBar`

`Content` 是普通 frame，四周 padding 为 `24`，使用纵向 auto layout。`TitleBar`、`FormArea`、`ActionBar` 水平 padding 为 `0`，圆角为 `0`。

## TitleBar

- 直接在 `TitleBar` 节点自身设置 `border-default` 底部描边。
- 不新增子节点模拟边框。
- 源页面有返回操作时，在左侧放返回控件。

## FormArea

- 字段组织为 `Field / 字段名` 容器。
- 字段内部是 `label + 控件`。
- label 不使用 `:` 或 `：`。
- 控件默认宽度为 `300`，只有源页面明确需要时才调整。
- 字段内部使用横向 auto layout；多列字段使用行容器分组。
- 变量存在时，行间距使用 `spacing-lg`，字段间距使用 `spacing-xl`。
- 必填字段在 label 前添加红色 `*`，使用 `accent-error` 或等价错误色。

控件使用本地组件：

- 文本：Input
- 多行文本：Textarea
- 选择：Select
- 日期：DatePicker
- 数字：有 InputNumber 时使用 InputNumber，否则使用 Input 并记录限制
- 单选：Radio
- 复选：Checkbox
- 开关：Switch
- 权限或组织树：Tree

## ActionBar

- 表单操作放在底部。
- 主要提交/保存操作：Button `base / medium / primary`。
- 取消/返回次要操作：Button `outline / medium / primary`。
- 按钮组使用横向 auto layout，间距为 `spacing-base`。

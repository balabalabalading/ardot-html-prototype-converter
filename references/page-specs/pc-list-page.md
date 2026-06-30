# PC 列表页规范

适用于以表格为主体，并提供查询、导出、新增或其他列表操作的页面。

## 结构

`Content` 直接包含以下区块，顺序固定：

1. `TitleBar`
2. `FilterBar`
3. `ActionBar`
4. `Table`
5. `Pagination`

`Content` 自身四周 padding 为 `24`，应绑定 `spacing-xl`。上述五个内部区块水平 padding 为 `0`，圆角为 `0`。

## TitleBar

- 宽度通常为 `1160`，宽表页面可按页面实际宽度调整。
- 直接在 `TitleBar` 节点自身设置 `border-default` 底部描边。
- 只设置底部描边。不要新增 `BottomBorder`、line、rectangle 或子 frame 模拟分隔线。
- TitleBar 内放页面标题；只有原型中存在返回操作时才加入返回控件。

## FilterBar

- 宽度通常为 `1160`。
- 每个查询条件是一个 `Field / 字段名` 容器。
- 字段宽度为 `240`，除非源页面明确需要更宽控件。
- 字段高度通常为 `34`。
- label 不使用 `:` 或 `：`。
- 输入框宽度通常为 `120`；除非源页面明确要求，否则 clearable 为 false。
- 单选框的 placeholder 文案必须是「全部」。
- 隐藏 `InputComponent` 的 tips。
- 必须包含 `查询` 和 `重置` 两个按钮，将这两个按钮合并成一个容器。
- `查询`：Button 组件变体 `base / medium / primary`。
- `重置`：Button 组件变体 `outline / medium / primary`。

## ActionBar

- 宽度通常为 `1160`。
- 所有操作按钮都使用本地 Button 组件。
- 操作按钮默认使用 `base / medium / primary`，除非有明确记录的危险态或次要态。

## Table

- 使用 `Table -> table column 组件实例`。
- 生成列表表格时，不使用 `TableRow -> Cell`。
- 不要把表头或数据文本直接放在 `Table`、`Content` 或 page 根节点下。
- 紧凑后台列表页的 `Table` 高度通常为 `276`，除非源页面有明确差异。
- `Table` 必须开启裁剪溢出内容：`clipsContent=true`。
- 宽表的列总宽可以大于可视区域；由 Table 容器裁剪是预期表现。
- 表格列和样例数据必须来自渲染后的 element JSON、截图或整理后的列数据 JSON，不得编造业务列或样例数据。
- table column 组件通常包含默认占位行。创建表格后必须验证可见区域没有出现「项目名称」等组件默认占位文本。
- 如果默认占位行泄漏，优先补齐可见行数据、裁剪溢出，或调整为符合本页规范的可见高度；不要引入公式化高度规则替代 `276` 的默认规范。
- 只探查一次 table column 的表头和单元格文本路径，后续复用已确认路径；不要逐列深读完整子树。

复杂宽表推荐整理为以下列数据结构：

```json
{
  "cols": ["字段A", "字段B"],
  "col_data": {
    "字段A": ["第1行", "第2行"],
    "字段B": ["第1行", "第2行"]
  }
}
```

完成后必须验证 `Table` 的直接子节点都是 table column 组件实例。

## Pagination

- 内部 `PaginationComponent` 宽度固定为 `1160`。
- 宽表页面中，外层 `Pagination` 区块可以跟随宽表布局，但分页组件自身仍保持 `1160`。

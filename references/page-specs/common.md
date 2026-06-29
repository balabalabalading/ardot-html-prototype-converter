# 通用 Ardot 页面规则

除非页面类型规范另有说明，所有页面都遵守本规则。

## 页面命名

Ardot page 不能分组，因此页面名必须包含菜单层级。

- 每个 Ardot 文件默认对应一个系统时，不再额外添加系统名前缀。
- 一级菜单页面：`上级菜单-页面名-编号`
- 三级页面：`上级菜单-二级菜单-页面名-编号`
- 独立页面：`页面名-编号`

必须从解析后的页面 path 获取层级，不要只看平铺页面名。

## 根结构

每个业务页面只使用一个根 frame：

```text
Page
  PageFrame
    Sidebar instance
    Content frame
      页面类型区块
```

规则：

- page 根节点下不能挂大量独立 rectangle/text 节点。
- `PageFrame` 使用横向 auto layout。
- Sidebar 必须是当前一级菜单对应的组件实例。
- `Content` 是普通 frame，不是组件。
- `Content` 使用纵向 auto layout。
- PC 页面 `Content` 四周 padding 为 `24`，变量存在时绑定 `spacing-xl`。
- `Content` 背景使用系统正常的 surface/sidebar 背景色，不使用随意的浅色底。

## 本地组件

控件优先使用目标 Ardot 文件中的本地组件库：

- Button
- Input
- Textarea
- Select
- DatePicker
- Checkbox
- Radio
- Switch
- Tree
- Pagination
- table column
- Tabs、Tag、Card、Statistic 等按需使用

如果本地已有组件，不要用矩形加文本手绘按钮、输入框、分页或表格列。

## 变量与样式

共享颜色和间距优先使用设计变量：

- `surface` 或等价变量：内容区/卡片背景
- `sidebar-bg`：与侧边栏一致的背景
- `text-primary`、`text-secondary`
- `accent-primary`、`accent-success`、`accent-error`、`accent-warning`
- `border-default`
- `spacing-base`、`spacing-lg`、`spacing-xl`

如果当前文件没有变量 ID，可使用视觉等价值并记录差异。不要从另一个 Ardot 文件复制未验证的变量 ID。

## 容器纪律

- 所有主要区块使用 auto layout。
- 页面自有容器使用清晰名称，例如 `TitleBar`、`FilterBar`、`ActionBar`、`Table`、`Pagination`、`FormArea`、`InfoCard`、`ReportArea`。
- 页面自有容器通常水平 padding 为 `0`、圆角为 `0`；但 `Content` 本身仍保留页面 padding。
- 字段 label 不以中文或英文冒号结尾，除非它是业务正文段落而不是字段 label。
- 结构必须可编辑。除非源页面确实只有截图，否则不要把有意义的页面区域做成截图。

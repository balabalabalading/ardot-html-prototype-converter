# 执行检查清单

转换、修复、审查或交接 Ardot 原型页面时使用本清单。

## 编辑 Ardot 前

- [ ] 已读取 `workflow.md`。
- [ ] 已读取 `page-specs/common.md`。
- [ ] 已读取当前页面类型对应规范。
- [ ] 已解析页面树并确认页面 path / 层级。
- [ ] 已用 Playwright 或等价浏览器流程渲染 HTML。
- [ ] 已确认 element JSON 存在且有内容。
- [ ] 已确认截图存在。
- [ ] 已确认目标 Ardot file ID 和文件名。
- [ ] 已读取目标 Ardot 的组件库和变量。
- [ ] 已确认所需本地组件存在。
- [ ] 已确认所需 sidepanel 组件存在；若不存在，先创建后再生成页面。
- [ ] 已确认系统专用 manifest 路径。

## 建页过程中

- [ ] page 根节点只有一个 `PageFrame`。
- [ ] `PageFrame` 由 sidepanel 实例和普通 `Content` frame 组成。
- [ ] `Content` padding 为 `24`，可行时绑定 `spacing-xl`。
- [ ] 页面区块使用 auto layout。
- [ ] 页面自有容器 padding 为 `0`、圆角为 `0`，除非页面类型规范另有说明。
- [ ] TitleBar 使用自身底部描边，没有 `BottomBorder` 子节点。
- [ ] label 不包含 `:` 或 `：`。
- [ ] 常用控件使用本地组件实例。
- [ ] 组件属性修改后已验证生效。
- [ ] 表格使用直接的 table column 组件实例。
- [ ] Table 容器设置 `clipsContent=true`。
- [ ] 宽表没有被压缩到不可读。

## 验证

- [ ] 使用窄范围读取；只需要少量属性时不要读取整页。
- [ ] 已验证 page root、PageFrame、Sidebar、Content、页面类型区块，以及适用时的 Table/Pagination。
- [ ] 已验证 Sidebar 是组件实例。
- [ ] 已验证 Content 是普通 frame。
- [ ] 已验证列表/报表表格子节点是 table column 实例。
- [ ] 已验证 PC 列表页 PaginationComponent 宽度为 `1160`。
- [ ] 已生成或引用 Ardot 截图用于视觉检查。
- [ ] 已对照原始截图检查布局、字段、文本溢出和表格可读性。

## 交接

- [ ] 每完成一页都更新系统 manifest。
- [ ] 记录 Ardot page ID、PageFrame ID、Content ID、sidepanel 组件、页面类型、素材和验证状态。
- [ ] 对截图型或只能部分提取的页面记录已知限制。
- [ ] 明确写出下一位 agent 的具体下一步。

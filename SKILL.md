---
name: ardot-html-prototype-converter
description: 将 Axure 或 HTML 原型导出物转换为可编辑的 Ardot 原型文件，并审查或修复已有 Ardot 原型页面。适用于 HTML 转 Ardot、Axure 转 Ardot、Ardot 页面结构化重建、本地组件库复用、sidepanel 复用、按 table column 生成表格、按页面类型应用原型规范、转换结果交接与验证等任务。
---

# Ardot HTML 原型转换器

使用本 skill 将 Axure/HTML 原型导出物转换为可维护、可编辑的 Ardot 页面。目标不是逐像素复制 DOM，也不是按绝对坐标堆节点，而是基于本地组件、auto layout、可复用 sidepanel 和页面类型规范重建 Ardot 原型。

## 必读顺序

1. 计划或执行任何转换前，先读 `references/workflow.md`。
2. 创建或修复任何页面前，先读 `references/page-specs/common.md`。
3. 根据当前页面类型，只读取对应规范：
   - PC 列表页：`references/page-specs/pc-list-page.md`
   - PC 表单页：`references/page-specs/pc-form-page.md`
   - PC 详情页：`references/page-specs/pc-detail-page.md`
   - PC 报表页：`references/page-specs/pc-report-page.md`
   - 移动端页面：`references/page-specs/mobile.md`
4. 质量审查、修复他人产物、批量交接或接手已有结果时，还必须读取 `references/execution-checklist.md` 和 `references/failure-modes.md`。

## 不可违反的规则

- 创建 Ardot 页面前，必须用 Playwright 或等价浏览器流程渲染 HTML 原型。不要只依赖原始 HTML、文件名或截图印象。
- 渲染后的 element JSON 和截图是字段、label、表格列、样例数据、页面宽度和页面类型的依据。
- 最终 Ardot 页面不得按 DOM 绝对坐标散堆节点。
- 每个 Ardot page 根节点只能有一个 `PageFrame`，内部包含 sidepanel 组件实例和普通可编辑 `Content` frame。
- 必须复用当前 Ardot 文件中的本地组件库。不要假设另一个 Ardot 文件里的组件 ID 可用。
- `Content` 保持普通 frame，不转组件；`Content` 内的控件尽量使用本地组件实例。
- 使用 auto layout 和命名容器组织页面，不要让大量 rectangle/text 直接挂在 page 根节点或 content 根节点下。
- 表格必须使用 `Table -> table column 组件实例`。生成列表表格时，不使用按行组织的 `TableRow -> Cell` 结构。
- 每个系统维护独立 manifest，例如 `out/ardot_manifest_oms.json`。不要把多个系统混写到一个 manifest。

## 执行方式

每一批页面都先创建或验证一个样板页。样板页通过结构和视觉验证后，再继续处理同类页面。每完成一页都更新系统 manifest 和交接记录，不要等整批完成后再补。

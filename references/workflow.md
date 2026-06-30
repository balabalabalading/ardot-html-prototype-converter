# HTML 转 Ardot 转换流程

处理 Axure 或类似工具导出的 HTML 原型时，按本流程执行。

## 1. 确认输入

开始建页前，确认以下输入存在：

- HTML 原型导出目录存在，并且可以通过 HTTP 服务访问。
- 页面树来源存在，例如 `data/document.js`。
- 目标 Ardot 文件是当前系统对应的文件。
- 目标 Ardot 文件中已经有本地组件库，并至少有一个 sidepanel 示例组件。
- 已确定系统专用 manifest 路径，例如 `out/ardot_manifest_<system>.json`。

## 2. 解析页面树

将页面树解析为 `out/pages_manifest.json` 或等价 manifest。至少记录：

- `pageName`
- 页面 URL 或 HTML 文件路径
- 完整菜单路径
- 上级路径
- 页面编号
- 可能的页面类型
- 页面主体是否为截图型，是否适合结构化重建

必须使用完整路径判断页面层级。不要只根据平铺页面名推断页面所属菜单。

先输出目标范围的 compact manifest，再按需深挖单页。不要把整段压缩 `data/document.js`、全量 HTML 或宽泛搜索结果直接灌入上下文。compact manifest 只保留本批需要的 `pageId`、`pageName`、URL/HTML 路径、完整菜单 path、页面类型和少量状态判断。

## 3. 选择小批量范围

不要一次转换完整系统。先选择一个模块或一类页面。每个页面在系统 manifest 中记录：

- `sourcePageId`
- `pageName`
- `path`
- `pageType`
- `artifacts.elementJson`
- `artifacts.screenshot`
- `status`
- `verification`

## 4. 使用 Playwright 渲染 HTML

通过 HTTP 服务加载原型，并使用浏览器自动化流程渲染页面。Axure 导出的原始 HTML 通常不包含完整的动态内容。

每个页面至少需要以下证据：

- `out/elements/<pageId>.json` 存在。
- `out/screenshots/<pageId>.png` 存在。
- element JSON 的节点数不是 0。
- element JSON 或截图中能看到页面标题、筛选项、操作按钮、字段、表格列或业务内容。
- 已捕获页面宽高，用于判断是否为宽表页面。

如果渲染失败，先修复抓取流程，不要开始创建 Ardot 节点。

## 5. 检查 Ardot 文件状态

编辑前读取 Ardot 文件状态：

- editor state
- component library
- variables
- existing pages
- existing sidepanel components

确认本地组件库中存在按钮、输入框、选择器、分页、表格列以及当前页面所需控件。组件 ID 是文件内局部有效的，不要跨 Ardot 文件复用未验证的 ID。

读取组件库后，立即整理最小组件映射，例如 `sidePanel`、`Button`、`Input`、`Select`、`DatePicker`、`Pagination`、`table column`。后续操作引用这份映射，不要为了单个组件反复全量展开组件库。

## 6. 先做一个样板页

每批第一个页面按以下步骤执行：

1. 按 `page-specs/common.md` 的命名规则创建 Ardot page。
2. 创建唯一根节点 `PageFrame`。
3. 插入正确的 sidepanel 组件实例。
4. 创建普通 frame：`Content`。
5. 按对应页面类型规范创建 Content 内部区块。
6. 从渲染证据中填入字段、操作、表格和文本。
7. 完成结构和视觉验证。

样板页没有通过前，不要批量生成后续页面。

## 7. 批量构建

样板页有效后，复用其结构生成同类页面。但每页的 label、列、数据和按钮仍必须来自该页面自己的渲染 JSON 或截图。

如果页面主体是截图型，不要编造完整可编辑结构。只创建标准页面框架，提取可靠的可见字段，并在 manifest 中记录限制。

## 8. 验证每个页面

每页至少验证：

- page 根节点只有一个 `PageFrame`。
- Sidebar 是组件实例。
- `Content` 是普通 frame。
- 页面区块符合所选页面类型规范。
- 常用控件使用本地组件实例。
- 表格使用 `Table -> table column 组件实例`。
- 宽表可读，必要时由 Table 容器裁剪溢出。
- TitleBar 使用自身底部描边，而不是子节点模拟边框。

需要生成或引用截图进行视觉验证。如果当前模型不能看图，也要记录截图路径，交给人工或后续可看图模型检查。

## 9. 记录交接状态

每完成一页或一批，更新系统 manifest 和交接说明，至少包含：

- Ardot file ID
- 系统 manifest 路径
- 使用的 sidepanel 组件 ID
- 已完成页面 ID 和根 frame ID
- 使用的素材文件
- 验证状态
- 已知限制
- 下一步具体任务

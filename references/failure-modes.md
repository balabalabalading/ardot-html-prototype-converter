# 常见失败模式与修复方式

审查或修复已有 Ardot 原型页面时读取本文档。

## 跳过 HTML 渲染

表现：

- 字段或表格列缺失。
- 只根据页面名猜页面类型。
- 样例数据是编造的，和源页面不一致。

修复：

- 通过 HTTP 服务加载原型。
- 使用 Playwright 或等价浏览器流程渲染。
- 重新生成 element JSON 和截图。
- 根据渲染证据重建不确定区域。

## 按 DOM 绝对坐标散堆节点

表现：

- page 根节点下有大量 rectangle/text 节点。
- 没有 `PageFrame`、没有 `Content`、没有清晰区块。
- 页面无法按结构编辑。

修复：

- 将该页面视为废弃页。
- 按 `PageFrame -> Sidebar instance + Content frame` 重建。
- 使用页面类型区块和本地组件。

## 未使用本地组件

表现：

- 按钮、输入框、选择器、分页或表格列是手绘的。
- 本地组件库存在，但页面中没有复用。

修复：

- 读取本地组件库。
- 用当前文件的组件实例替换控件。
- 编辑后验证实例的实际状态。

## 页面命名错误

表现：

- 页面名缺少上级菜单。
- 三级页面只使用叶子页面名。
- Ardot 文件已经按系统拆分，但页面名仍重复添加系统前缀。

修复：

- 使用解析后的页面 path 重命名：`上级菜单-页面名-编号` 或 `上级菜单-二级菜单-页面名-编号`。

## TitleBar 使用子节点模拟边框

表现：

- `TitleBar` 里有 `BottomBorder`、rectangle、line 或只用于模拟底部分隔线的 frame。

修复：

- 删除子边框节点。
- 直接在 `TitleBar` 自身设置 `border-default` 底部描边。

## 生成表格按行组织

表现：

- `Table -> TableRow -> Cell`。
- 文本节点按 x/y 坐标散放。
- 列宽难以统一调整，组件无法复用。

修复：

- 改为 `Table -> table column 组件实例`。
- 将字段名和行数据写入各列组件实例。
- 设置 `Table.clipsContent=true`。

## 宽表被压缩

表现：

- 很多列被挤进 1160px。
- 文本不可读或重叠。

修复：

- 根据渲染页面宽度或列宽总和设置 PageFrame/Content/Table。
- PC 列表页的 `PaginationComponent` 仍保持宽度 `1160`。
- 列总宽超过可视区域时，由 `Table` 裁剪溢出。

## Manifest 混用

表现：

- 一个系统的进度覆盖到另一个系统的 manifest。
- 一个 Ardot 文件中的组件 ID 被直接复用到另一个文件。

修复：

- 按系统拆分 manifest，例如 `out/ardot_manifest_oms.json`。
- 从当前 Ardot 文件重新读取组件 ID 和变量 ID。

## 读取或编辑过量

表现：

- 大范围 `batch_read` 导致上下文爆炸。
- 每个表格列都完整回读。
- `componentProperties` 更新产生大量 potential issue 输出。

修复：

- 只读取当前判断需要的节点和属性。
- 优先浅层读取。
- 先探查一个 table column 的文本路径，再复用已确认模式。
- 优先复制正确组件变体，再更新实例内部可见文本。

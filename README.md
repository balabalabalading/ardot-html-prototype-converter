# Ardot HTML Prototype Converter

中文 | [English](#english)

一个用于将 Axure/HTML 原型导出物转换为可编辑 Ardot 原型文件的 Codex Skill。它把项目实践中沉淀的转换流程、页面规范、执行检查清单和失败模式固化为可复用的 agent 工作流。

## 适用场景

- 将 Axure 或类似工具导出的 HTML 原型转换为 Ardot 可编辑页面。
- 审查或修复已有 Ardot 原型中散节点、未使用组件、表格结构错误等问题。
- 让能力较弱的 agent 按固定 SOP 执行原型转换，减少遗漏步骤。
- 为不同系统的后台管理页面建立一致的页面结构和验证标准。

## 核心规则

- 必须先用 Playwright 或等价浏览器流程渲染 HTML 原型，再根据 element JSON 和截图重建页面。
- 不把 DOM 绝对坐标直接搬到 Ardot；最终页面必须使用容器、auto layout 和组件实例。
- 每个页面根节点只保留一个 `PageFrame`。
- Sidebar 使用当前 Ardot 文件中的 sidepanel 组件实例。
- `Content` 保持普通 frame，PC 页面默认 padding 为 `24`。
- 表格使用 `Table -> table column 组件实例`，并设置 `clipsContent=true`。
- 页面规范按类型拆分：PC 列表页、表单页、详情页、报表页、移动端占位规范。

## 目录结构

```text
ardot-html-prototype-converter/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── workflow.md
│   ├── execution-checklist.md
│   ├── failure-modes.md
│   └── page-specs/
│       ├── common.md
│       ├── pc-list-page.md
│       ├── pc-form-page.md
│       ├── pc-detail-page.md
│       ├── pc-report-page.md
│       └── mobile.md
└── LICENSE
```

## 使用方式

在支持 Codex Skills 的环境中，将本仓库放入 skills 目录，然后在任务中调用：

```text
使用 $ardot-html-prototype-converter 将 Axure HTML 原型转换为可编辑的 Ardot 原型。
```

Agent 会先读取 `SKILL.md`，再根据任务类型按需读取 `references/` 下的 SOP、页面规范、执行检查清单和失败模式。

## 许可

本项目使用 [MIT License](LICENSE)。

---

## English

A Codex Skill for converting Axure/HTML prototype exports into editable Ardot prototype files. It packages a reusable workflow, page specifications, execution checklist, and failure-mode guide distilled from real HTML-to-Ardot conversion work.

## Use Cases

- Convert Axure or similar HTML prototype exports into editable Ardot pages.
- Review or repair Ardot prototype pages with scattered nodes, missing component usage, or incorrect table structure.
- Help less capable agents follow a strict SOP and avoid missing critical conversion steps.
- Keep backend management prototypes consistent across systems.

## Core Rules

- Render the HTML prototype with Playwright or an equivalent browser workflow before rebuilding pages from element JSON and screenshots.
- Do not copy DOM absolute coordinates directly into Ardot; final pages must use containers, auto layout, and component instances.
- Each page root should contain only one `PageFrame`.
- Sidebar must use a sidepanel component instance from the current Ardot file.
- `Content` remains a normal editable frame. PC pages use `24` padding by default.
- Tables use `Table -> table column component instances` and set `clipsContent=true`.
- Page specs are split by type: PC list, form, detail, report, plus a placeholder mobile spec.

## Structure

```text
ardot-html-prototype-converter/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── workflow.md
│   ├── execution-checklist.md
│   ├── failure-modes.md
│   └── page-specs/
│       ├── common.md
│       ├── pc-list-page.md
│       ├── pc-form-page.md
│       ├── pc-detail-page.md
│       ├── pc-report-page.md
│       └── mobile.md
└── LICENSE
```

## Usage

Place this repository in a Codex Skills directory, then invoke it in a task:

```text
Use $ardot-html-prototype-converter to convert an Axure HTML prototype into an editable Ardot prototype.
```

The agent will read `SKILL.md` first, then load the relevant workflow, page spec, checklist, and failure-mode references as needed.

## License

This project is released under the [MIT License](LICENSE).

# Sql2Json · SQL / JSON 可视化转换器

把 SQL（或纯 JSON）转换成结构化的抽象语法树（AST）JSON，并提供多种视图帮助你读懂一段查询到底在做什么——**纯前端、零依赖、本地运行，不调用任何大模型 API**。

> 在线体验：[https://mybookstores.github.io/Sql2Json/](https://mybookstores.github.io/Sql2Json/)

---

## 它能做什么

| 视图 | 说明 |
|------|------|
| **JSON 文本** | 把 SQL 解析为格式化、带缩进的 AST JSON；纯 JSON 输入则原样美化输出。 |
| **树形视图** | 可折叠的 JSON 树。**点击任意节点即可复制「`"键": 值`」形式的完整子树**（含键名、含整棵子树）。 |
| **结构可视化** | 把查询拆成 `SELECT → FROM → JOIN → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT` 的流程图，条件以 `AND / OR` 嵌套展示。 |
| **SQL / JSON 解释** | 规则化的自然语言说明（例如「这是一条更新语句：修改表 products 中符合条件的记录…」），无需联网、无需 API Key。 |

## 主要特性

- **多方言支持**：MySQL / PostgreSQL / SQLite / MariaDB / SQL Server / BigQuery 等，下拉框切换。
- **SQL 输入区语法高亮**：零依赖的叠加式高亮（关键字 / 字符串 / 数字 / 操作符），输入即着色。
- **点击节点复制**：树形视图中点击节点，自动复制该节点及其子树的 JSON 文本（带键名）。
- **固定高度 · 卡内滚动**：左右两块卡片占满视口高度，内容超长时在卡片内部滚动，滚动条默认隐藏、悬停时显示。
- **结构可视化精准**：UPDATE / DELETE 等语句的表名、多列 `SET` 赋值均正确呈现（已修复早期 `[object Object]` 显示问题）。
- **完全本地**：解析在浏览器内完成，`assets/sql-parser.js` 为本地内置解析器，**不会把你的 SQL 发送到任何服务器**。

## 如何使用

### 在线使用
直接打开 [https://mybookstores.github.io/Sql2Json/](https://mybookstores.github.io/Sql2Json/)

### 本地运行
1. 克隆仓库：
   ```bash
   git clone https://github.com/mybookstores/Sql2Json.git
   cd Sql2Json
   ```
2. 直接用浏览器打开 `index.html` 即可（无需安装、无需构建、无需起服务）。
   - 若浏览器对 `file://` 加载本地脚本有限制，可任选一种静态服务：
     ```bash
     # 任选其一
     python3 -m http.server 8139
     npx serve .
     ```
   然后访问 `http://127.0.0.1:8139/index.html`。

## 支持的方言

在左上角下拉框选择，常见包括：`MySQL`、`PostgreSQL`、`SQLite`、`MariaDB`、`SQL Server (TransactSQL)`、`BigQuery` 等。不同方言对语法细节（如引号、函数）的解析略有差异，转换器会按所选方言解析。

## 工作原理

- 解析内核使用 [node-sql-parser](https://github.com/taozhi8833998/node-sql-parser)（以 UMD 方式打包在 `assets/sql-parser.js`，全局暴露 `Parser`），负责把 SQL 文本解析成 AST，并提供 `astify` / `sqlify` / `exprToSQL`。
- 四种视图全部基于同一个 AST 生成：
  - **JSON 文本 / 树形视图** 直接序列化 AST；
  - **结构可视化** 按语句类型（SELECT / INSERT / UPDATE / DELETE 等）抽取 `from`、`join`、`where`、`set` 等字段渲染为流程图；
  - **SQL / JSON 解释** 复用 `exprToSQL` 把各子句规则化转成中文自然语言。
- 纯原生 JavaScript（无框架、无打包工具），所有渲染在客户端完成。

## 项目结构

```
Sql2Json/
├── index.html            # 主页面（HTML + CSS + JS 全部内联，单文件可运行）
├── assets/
│   └── sql-parser.js     # 本地 SQL 解析器（node-sql-parser UMD）
└── README.md
```

## 隐私

所有解析与转换都在你的浏览器本地完成，**不会上传任何 SQL 或 JSON 数据**。可放心粘贴含有敏感字段的查询进行查看。

## 技术栈

- 解析：`node-sql-parser`（UMD 本地打包）
- 前端：原生 HTML / CSS / JavaScript，零运行时依赖
- 部署：GitHub Pages（main 分支根目录）

## Roadmap（可能的后续方向）

- 多语句批量解析与切换
- 两段 SQL 的结构差异高亮对比
- 暗色 / 浅色主题切换
- 导出当前视图为图片或文件

## License

MIT —— 可自由使用、修改与分发。

---

欢迎提交 Issue 与 PR 来完善功能或修复问题。

# Sql2Json

SQL / JSON 可视化转换器。把 SQL（或纯 JSON）转换成结构化 JSON，并提供多种视图：

- **JSON 文本**：格式化输出
- **树形视图**：可折叠的 JSON 树，点击节点可复制「键: 值」
- **结构可视化**：将 SQL 的 FROM / JOIN / WHERE / GROUP BY 等渲染为流程图
- **SQL / JSON 解释**：规则化的自然语言解释（不调用大模型 API）

支持多方言（MySQL / PostgreSQL / SQLite / MariaDB / SQL Server / BigQuery 等），纯前端、零依赖、本地运行。

## 使用

直接用浏览器打开 `index.html` 即可（`assets/sql-parser.js` 为本地 SQL 解析器）。

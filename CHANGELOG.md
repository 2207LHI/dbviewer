# Change Log

All notable changes to the "dbviewer" extension will be documented in this file.

Check [Keep a Changelog](http://keepachangelog.com/) for recommendations on how to structure this file.

## [Unreleased]

- 初始开发与修复（见下面版本历史）

## [0.0.5] - 2026-03-24

- SQL 查询编辑器升级为 Monaco：支持更完善的编辑体验、建议面板和悬浮信息展示。
- SQL 智能提示增强：支持 SQL 关键字、模板片段、表名、列名、`alias.column` 场景补全。
- 查询上下文补全增强：在 `FROM/JOIN/INTO/UPDATE` 后优先建议表名，在 `SELECT/WHERE/ON/HAVING/SET/GROUP BY/ORDER BY` 等语境优先列名。
- 新增轻量语法诊断：执行前检查引号未闭合、括号不匹配及多语句提醒，并在编辑器内显示标记。
- 查询编辑框主题适配优化：颜色与建议框风格对齐 VS Code 当前主题。
- 查询页新增 schema 元数据接口与缓存机制（60 秒）以提升补全响应性能。

## [0.0.4] - 2026-03-24

- SQL 查询面板增强：支持 SQL 关键字高亮、注释高亮（`--`、`#`、`/* ... */`），并将默认输入区高度提升到 260px。
- SQL 编辑快捷键增强：支持 `Cmd/Ctrl + /` 切换行注释，支持 `Shift + Alt + A` 切换块注释。
- 查询草稿持久化：按连接 ID 自动保存查询内容，重新打开该连接查询页时优先恢复已保存内容。
- 查询结果导出：支持将当前结果导出为 CSV 或 JSON，并通过保存对话框选择导出路径。
- 侧边栏数据库树刷新稳定性优化：连接状态变化时改为整树刷新，并修复 `SHOW` 语句加载路径以提升展开可靠性。

## [0.0.3] - 2026-03-04

- 修复并增强 SQL 查询面板：在 webview 中处理 `execute` 消息并返回结果；当在表级打开时注入默认 SQL（`SELECT * FROM \\`DB\\`.\\`TABLE\\` LIMIT 100;`），在数据库级打开时默认展示 `SHOW TABLES;`；对无结果集的语句返回受影响行信息。
- 修复表视图后端：使用 `information_schema.COLUMNS` 返回列信息并按前端期望别名（Field/Type/Null/Key/Default/Extra/Comment）；改用 `.query` 执行以避免 prepared-statement 参数错误；返回分页数据与外键引用以支持结构/数据/ER 页面渲染。
- 修复连接配置面板：实现 `save`/`test`/`delete` 消息处理；`test` 使用临时连接并立即断开，`delete` 后自动关闭编辑面板并刷新侧栏（加入短延迟以缓解删除首项的刷新竞态）。
- 修复侧栏连接图标显示问题：使用彩色 SVG 图标并为 `TreeItem` 设置稳定 `id`，保证局部刷新与颜色显示一致。
- 其他：若干编译与 lint 修复，改进错误提示与日志。

## [0.0.2] - 2026-03-03

- 支持 SSH 隧道连接（ssh2 forwardOut），并在隧道断开时自动重连（指数退避），添加 keepalive 设置
- 在连接配置面板添加 SSH 配置字段（SSH 主机/端口/用户/私钥/密码）
- 导入/导出连接（支持包含明文密码的导入导出）并在侧栏视图标题添加导入/导出按钮
- 单连接“刷新连接”功能：右键连接项可重连并刷新面板（复用刷新按钮）
- 连接配置持久化到 `~/.dbviewer/config.json`（同时保留 globalState），导入导出支持用户自选路径
- 密码可见切换（小眼睛）用于 MySQL 密码与 SSH 密码输入框
- 在 SSH 隧道或连接错误时给出用户提示并自动清理连接状态
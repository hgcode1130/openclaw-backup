# projects.md

## 状态

- [OpenClaw 运维] Daily Reflection 已按 `/home/re0hg/.openclaw/workspace` 作为统一 Git 根连续验证 commit/push 可用；本日进一步确认仅做“前置备份”会让当日复盘产出滞后入仓，后续流程需补“写回记忆后再 commit/push”闭环；但当前 `git add memory` 仍会带入 `memory/_state/`、`heartbeat-state.json`、`memory/weekly/` 与 archive 重命名等自动产物，下一步应改成“仅人工维护记忆文件”的显式白名单。
- [小红书运营] 已建立固定运营工作流文档：`memory/xiaohongshu-workflow.md`。后续默认按“受众分析→标题A/B→正文→标签→封面文案→确认后发布→评论引导”执行，无需重复提醒；2026-03-07 已新增“网页抓取→PRD→subagent 草稿生成→用户确认→发布”的执行路径，并验证可在 browser 不可用时降级到命令行抓取出最小可发草稿。
- [搜索工作流] 外部/时效信息检索已固化为“优先走 grok-search skill（Codex→MCP）”，仅在不可用时降级；相关偏好已同步到 `USER.md` 与 `skills/grok-search/SKILL.md`，后续按该策略执行。

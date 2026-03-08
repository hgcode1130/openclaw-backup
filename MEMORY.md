# MEMORY.md

- 仅主会话加载：群聊或共享上下文不要加载本文件
- 用户时区: Asia/Shanghai (北京时间)
- 记忆索引: 见 memory/ 目录
- memory/projects.md ← 项目层：每个项目的当前状态和待办
- memory/infra.md    ← 基础设施层：服务器配置、API地址等速查信息
- memory/lessons.md  ← 教训层：踩过的坑，按严重程度分级
- memory/YYYY-MM-DD.md ← 日志层：每天发生了什么
- QQ OpenID: 21D2CC74AB9A049C0B0BBB10EBE083AE

## 用户偏好与约束（已固化）
- 回复风格：信息充分、结构清晰、逻辑严密。
- 外部/时效信息检索：优先使用 grok-search skill（Codex→MCP），仅在不可用时降级。
- 配置修改后的重启门禁（硬规则）：先执行 `openclaw doctor --non-interactive`，无阻塞错误后才允许重启。
- Windows 远控/运维场景（尤其 RustDesk）优先使用目标程序原生 CLI，避免依赖脆弱的 GUI 探测与跨壳引号拼接。
- 浏览器使用策略（WSL2/Windows 互操作）：优先从 PowerShell 通过 `wsl -e google-chrome-stable --proxy-server="http://127.0.0.1:7897" --remote-debugging-port=9222 --user-data-dir=/home/re0hg/.config/google-chrome` 启动 Chrome（固定 profile，不使用 `$HOME`）；默认无头，登录/风控时切有头，由 agent 先拉起后再通知用户接手。

## 关键配置（长期）
- Discord 代理：`127.0.0.1:7897`
- 会话默认 reasoning：`off`
- 默认模型：`gpt-5.4`
- 模型别名：`complex=gpt-5.2-codex`、`medium=gpt-5.4`
- MLLM 每日论文速览默认发送频道：Discord `1479351623871631361`（#paper-daily）

## 常见故障与修复策略
- Daily Reflection 备份根路径统一为 `/home/re0hg/.openclaw/workspace`；若该路径 Git 检查失败：
  - 立即停止 Git 写操作；
  - 标记“备份失败但继续复盘”；
  - 转入只读复盘，保证流程连续性。
- Cron-only/低活动日复盘：
  - 除证据最小集（`projects.md`、`lessons.md`、今昨日日志）外，必须用 `sessions_list` 交叉确认无遗漏会话。
- 日志落盘规则：
  - 若 `memory/YYYY-MM-DD.md` 不存在，先创建文件再写结论。

## 项目状态（周级快照）
- OpenClaw 运维：
  - Daily Reflection 已按 `/home/re0hg/.openclaw/workspace` 作为统一 Git 根并验证 commit/push 可用；
  - 当前仍存在 `git add memory` 白名单过宽导致噪音提交的问题（`memory/_state/`、`heartbeat-state.json`、`memory/weekly/`、archive 重命名）。
- 多图 Unified Model 可控性研究：
  - 已建立机器可读 PRD，执行路径固定为“先结构化 PRD，再检索与精读”；
  - 长任务优先 subagent，单次超时 2 小时。
- Ralph Loop Skill 化：
  - 已采用无脚本轻量版（SKILL + references）作为默认试跑形态，待闭环验证后再决定自动化。
- 小红书运营：
  - 固定工作流已沉淀到 `memory/xiaohongshu-workflow.md`，后续按模板执行。

## 待核对事项
- `dangerouslyDisableDeviceAuth=true` 高风险配置：需在不影响现网可用性的前提下评估回退方案并安排验证窗口。
- WSL→Windows 互操作修复（`/etc/wsl.conf` interop）需用户侧复测确认是否生效。

## 近期重要更新（自动，滚动7天）
- [2026-03-08][关键决策] 小红书发布阶段若用户端看不到登录窗口，必须切换“有头可见窗口”或提供二维码，不继续停留在无头链路等待。
- [2026-03-08][关键决策] 固定 profile 的登录判定以“创作者中心关键登录态 cookie”为准；仅有站点 cookie 不视为已登录。
- [2026-03-08][关键规则] heartbeat poll 无待办时只回 `HEARTBEAT_OK`，禁止夹带论文速览或其他扩展内容。
- [2026-03-07][关键配置] 浏览器启动策略固定为 PowerShell `wsl -e google-chrome-stable --proxy-server="http://127.0.0.1:7897" --remote-debugging-port=9222 --user-data-dir=/home/re0hg/.config/google-chrome`；默认无头，登录/风控时切有头。
- [2026-03-07][关键决策] 小红书发布登录职责固定：由 agent 先拉起 Chrome，仅在需要登录/风控时通知用户接管，不再要求用户手动敲启动命令。
- [2026-03-07][已验证修复] CPA `/v1/chat/completions` 调用已确认需使用 `reasoning_effort`；`reasoning: {"effort": ...}` 为 `/responses` 风格，不应混用。
- [2026-03-07][已验证基线] XML 探针测试结论稳定：`gpt-5.3-codex / gpt-5.2-codex / gpt-5.2` 输出 `768`，`gpt-5.4` 输出 `512`。
- [2026-03-07][已验证修复] WSL interop 恢复（`WSLInterop` handler 正常），`cmd.exe`/`powershell.exe`/`winget.exe` 在 WSL 调用通过；RustDesk 1.4.1 安装完成且服务自动启动。
- [2026-03-06][待核对] `dangerouslyDisableDeviceAuth=true` 可能带来认证风险，需安排回退验证。
- [2026-03-06][待核对] WSL→Windows interop 修复路径已给出，待用户复测确认。

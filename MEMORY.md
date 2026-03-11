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
- Heartbeat 轮询协议：无待办时仅回复 `HEARTBEAT_OK`，不夹带扩展内容。
- 小红书发布登录门禁：若用户端看不到登录窗口，必须立即切换有头可见窗口或二维码方案；仅有站点 cookie 不视为已登录，需以创作者中心关键登录态 cookie 为准。

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
- Daily Reflection 采用“前置备份 + 写回后二次备份”闭环；否则当日新增的日志/教训/规则可能只留在本地、要到次日才被补带进远程。
- Cron-only/低活动日复盘：
  - 除证据最小集（`projects.md`、`lessons.md`、今昨日日志）外，必须用 `sessions_list` 交叉确认无遗漏会话。
- 日志落盘规则：
  - 若 `memory/YYYY-MM-DD.md` 不存在，先创建文件再写结论。
- WSL↔Windows 互操作排障：
  - 若出现 `Exec format error`/`MZ not found`，先检查 `/proc/sys/fs/binfmt_misc/WSLInterop` handler；本机已验证修复后 `cmd.exe`/`powershell.exe`/`winget.exe` 在 WSL 可调用。

## 项目状态（周级快照）
- OpenClaw 运维：
  - Daily Reflection 已按 `/home/re0hg/.openclaw/workspace` 作为统一 Git 根并补齐“写回记忆后再 commit/push”的闭环；
  - 2026-03-10 起备份白名单已收紧为显式枚举 `memory/*.md` 与根目录记忆文件，不再把 `memory/_state/`、`heartbeat-state.json`、`memory/weekly/`、archive 重命名等自动产物带入提交。
- 多图 Unified Model 可控性研究：
  - 已建立机器可读 PRD，执行路径固定为“先结构化 PRD，再检索与精读”；
  - 长任务优先 subagent，单次超时 2 小时。
- Ralph Loop Skill 化：
  - 已采用无脚本轻量版（SKILL + references）作为默认试跑形态，待闭环验证后再决定自动化。
- 小红书运营：
  - 固定工作流已沉淀到 `memory/xiaohongshu-workflow.md`，后续按模板执行；
  - 发布阶段登录门禁已固化（不可见窗口即切有头/二维码；登录态以创作者中心关键 cookie 为准）。

## 待核对事项
- `dangerouslyDisableDeviceAuth=true` 高风险配置：需在不影响现网可用性的前提下评估回退方案并安排验证窗口。
- 固定 profile 下 `headed → headless` 切换后的登录态长期稳定性，需后续发布任务继续观测。

## 近期重要更新（自动，滚动7天）
- 2026-03-11｜关键决策（待核对）：MLLM 论文跟进优先从 InternVL-U、CourtSI、MissBench、VLM-Loc 中选 2-3 篇做深读，深读后再固化为长期结论。
- 2026-03-10｜关键修复：Daily Reflection 备份白名单已改为显式枚举 `memory/*.md` 与根目录记忆文件，避免 `_state/`、heartbeat、weekly、archive 噪音进入提交。
- 2026-03-09｜关键决策：Heartbeat 轮询在“无待办”场景仅允许回复 `HEARTBEAT_OK`；若再出现扩展执行，按协议偏离处理并优先纠偏。
- 2026-03-09｜关键策略：论文速览链路在 grok-search 异常（502/403）时可临时降级 arXiv 直查；恢复后应回切 grok-search。（待核对：需再观测 1-2 次任务确认稳定性）


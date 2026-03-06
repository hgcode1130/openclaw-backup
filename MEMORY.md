# MEMORY.md

- 仅主会话加载：群聊或共享上下文不要加载本文件
- 用户时区: Asia/Shanghai (北京时间)
- 记忆索引: 见 memory/ 目录
- memory/projects.md ← 项目层：每个项目的当前状态和待办
- memory/infra.md    ← 基础设施层：服务器配置、API地址等速查信息
- memory/lessons.md  ← 教训层：踩过的坑，按严重程度分级
- memory/YYYY-MM-DD.md ← 日志层：每天发生了什么
- QQ OpenID: 21D2CC74AB9A049C0B0BBB10EBE083AE
- 用户最新全局偏好（2026-03-06）：Discord 代理走 127.0.0.1:7897；会话默认关闭 reasoning；默认模型 gpt-5.4；模型别名保持 complex=gpt-5.2-codex、medium=gpt-5.4。

## 近期重要更新（自动，滚动7天）
- [2026-03-06] 长期配置偏好固定：Discord 代理 `127.0.0.1:7897`，默认 reasoning=off，默认模型 `gpt-5.4`，别名 `complex=gpt-5.2-codex`、`medium=gpt-5.4`。
- [2026-03-06] 研究任务执行策略固定：中长周期研究先结构化 PRD（机器可读）再检索与精读，优先 subagent，单次超时 2 小时。
- [2026-03-06] Ralph loop 采用无脚本轻量落地（SKILL+references）作为默认试跑形态，先验证闭环再决定自动化。
- [2026-03-06] OpenClaw 稳定性问题画像已验证：Discord 1006 断连 + listener 超时 + pending delivery 重试失败为主要异常簇。
- [2026-03-06][待核对] `dangerouslyDisableDeviceAuth=true` 存在高风险，需在不影响现网可用性的条件下安排回退与验证。

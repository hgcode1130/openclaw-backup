# lessons.md

## 经验教训

- [S2|流程前置检查] 执行 daily-reflection 前先验证 `/root/.openclaw` 是否是 Git 仓库（`git -C /root/.openclaw rev-parse --is-inside-work-tree`）。若失败，直接在简报标记“备份失败但继续复盘”，避免在不存在仓库上重复执行 add/commit/push。
- [S2|路径可达性优先] 若 `/root/.openclaw` 报 `Permission denied`，先记录为“路径不可达”并停止后续 Git 子命令，再做只读复盘，避免无效重试。
- [S2|时区一致性] 每日日志文件名按用户时区（Asia/Shanghai）生成，避免 UTC 日期导致日志写入到错误日期文件。
- [S3|低活动日复盘口径] 当日除定时复盘外无关键业务会话时，需在日志与简报中明确标注“无新增业务会话结论”，避免误导为遗漏分析。
- [S3|复盘证据最小集] 低会话量场景仍需至少核对 `memory/projects.md`、`memory/lessons.md` 与今昨日日志后再下结论，避免仅凭单条会话做过度推断。
- [S3|Cron-only 日判定] 若当日主要活动来自定时任务（如 daily-reflection），需额外用 `sessions_list` 交叉确认是否存在遗漏业务会话；确认无后再在简报中明确“无新增业务会话结论”。
- [S3|日志文件先行] 若 `memory/YYYY-MM-DD.md` 不存在，先创建当日日志文件再写复盘结论，避免结论仅停留在会话输出、未沉淀到记忆层。
- [S2|Reflection 备份白名单收窄] 现行 daily-reflection 使用 `git add memory` 会把 `memory/_state/`、`heartbeat-state.json`、`memory/weekly/` 与 archive 重命名一并纳入提交，造成高噪音备份；后续应改为更细粒度白名单，只提交人工维护记忆文件。
- [S2|Reflection 仓库根统一] Daily Reflection 的 Git 检查与备份以 `/home/re0hg/.openclaw/workspace` 为唯一根路径；若继续引用 `/root/.openclaw` 旧路径，会制造错误告警并误判备份状态。
- [S2|Heartbeat 轮询只回执] 遇到 heartbeat poll 且无待处理事项时，只回复 `HEARTBEAT_OK`；不要顺带输出论文速览或其他内容，避免把维护通道误用为内容投递通道。
- [S2|Linux Browser 故障定位] OpenClaw 在 Linux 上遇到 browser tool 超时时，不要只看“browser control service unreachable”字面；应先区分 18791 控制服务、CDP 18800 与实际 Chromium 启动链。若系统 Chromium 来自 snap，优先参考 `docs/tools/browser-linux-troubleshooting.md`，重点排查 attach-only + 独立 CDP 服务 + profile lock（SingletonLock/Socket）冲突。

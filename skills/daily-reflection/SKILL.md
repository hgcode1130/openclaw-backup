---
name: daily-reflection
description: 每日复盘与自我进化流程：先备份 .openclaw 到 GitHub（失败不阻断），再基于 memory/ 与会话记录做问题复盘、记忆沉淀与规则微调，并输出中文简报。适用于“每日复盘”“nightly review”“sync & improve”“自我进化”等请求。
---

# Daily Reflection（自我进化）

按以下流程执行，默认语言为中文。

## 0) 执行边界

- 严禁修改 `SOUL.md`。
- 严禁未经确认安装第三方 Skill。
- 严禁未经确认执行草稿脚本（仅可写入 `workspace/skill_drafts/`）。
- 允许在工作区内读取/整理/更新记忆文件。
- 涉及外发动作（如推送失败后改远程、发消息到外部）需显式说明结果，不擅自扩展行为。

## 1) 备份优先（GitHub）

目标：先尝试将 `.openclaw` 中的 reflection 相关变更同步到远程仓库，失败也继续复盘。

建议命令顺序（按环境适配）：

1. 可达性与仓库检查：`git -C /home/re0hg/.openclaw/workspace rev-parse --is-inside-work-tree`
2. 检查 reflection 白名单状态：
   - `git -C /home/re0hg/.openclaw/workspace status --porcelain -- .gitignore memory MEMORY.md AGENTS.md TOOLS.md USER.md skills/daily-reflection/SKILL.md`
3. 若有改动（白名单范围内）：
   - `git -C /home/re0hg/.openclaw/workspace add -f .gitignore`
   - `git -C /home/re0hg/.openclaw/workspace add memory MEMORY.md AGENTS.md TOOLS.md USER.md skills/daily-reflection/SKILL.md`
   - `git -C /home/re0hg/.openclaw/workspace commit -m "chore: daily reflection backup"`（无改动则跳过）
4. 推送：`git -C /home/re0hg/.openclaw/workspace push`

若任一步失败：

- 记录错误摘要（1-2 行），
- 明确标记“同步失败但继续复盘”，
- 继续执行后续步骤。

## 2) 内省与分析

### 2.1 读数据

至少读取并对比：

- `MEMORY.md`（基线）
- `memory/YYYY-MM-DD.md`（今天、昨天）
- `memory/projects.md`
- `memory/lessons.md`
- 当日关键会话结论（仅提炼结论，不转储隐私原文）

### 2.2 找问题（必须给出证据）

至少覆盖三类：

1. 理解偏差：需求理解错误、边界误判
2. 执行低效：重复动作、可脚本化却手工执行
3. 用户纠正点：被用户明确纠偏的行为

每条问题用三段式：

- 现象：发生了什么
- 影响：造成什么损失/风险
- 改法：下次具体怎么做

### 2.3 记日志（当日）

把复盘结论追加到 `memory/YYYY-MM-DD.md`，使用统一格式：

```text
[PROJECT: Daily Reflection] 每日复盘
结论: 一句话总结今天最关键改进
文件变更: 逗号分隔路径
教训: 最重要的1-2条
标签: #reflection #improvement
```

只写结论，不写冗长过程。

## 3) 沉淀与调整

### 3.1 更新记忆

- 通用、可复用的经验写入 `memory/lessons.md`。
- 项目状态变化写入 `memory/projects.md`。
- `MEMORY.md` 仅在“索引层信息变化”时更新。
- 过期或冲突信息要清理，避免双版本真相。

### 3.2 微调规则/工具

按痛点小步修改：

- `AGENTS.md`：流程、边界、协作规则
- `TOOLS.md`：工具源、本地速查、稳定实践

要求：

- 每次只做可解释的最小改动；
- 明确写出“为什么改、预期收益”。

### 3.3 补强能力（按需）

若发现缺能力：

- 只输出候选 Skill 清单（来源 + 价值 + 风险），不自动安装。

若发现可自动化重复动作：

- 在 `workspace/skill_drafts/` 写 Python/Bash 草稿；
- 仅写不跑，并在简报中注明“待人工确认执行”。

## 4) 输出简报（中文）

最终输出四段：

1. **同步**：Git 推送状态（成功/失败 + 一行原因）
2. **复盘**：今日核心问题与改进要点（最多 5 条）
3. **变更**：本次修改了哪些记忆/规则文件
4. **建议**：候选 Skill 或脚本草稿（若无则写“无”）

风格要求：客观、直接、少废话。

## 5) 面向当前工作区的定制约束

- 用户是 MLLM 研究生，偏好“信息充分、结构清晰、逻辑严密”；简报必须结构化。
- 时间语义以用户时区（Asia/Shanghai）为准。
- 涉及定时任务（cron）时：
  - 使用主会话最后路由回传结果；
  - `sessionTarget="isolated"`；
  - `payload.kind="agentTurn"`；
  - `payload.deliver=true`；
  - 不设置 `payload.channel/to`；
  - 不调用 `message` 工具发送回执。

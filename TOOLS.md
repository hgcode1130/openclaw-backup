# TOOLS.md - Local Notes

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is your cheat sheet.

## Skill Sources

### 聚合网站

- skillsdirectory.com — Reddit 社区口碑榜单
- skillsmp.com — 聚合 GitHub 11 万 + 开源技能，可溯源
- agentskills.me — 人工精选
- skillstore.io — 中文友好，有安全审查
- aitmpl.com/skills — Claude Code 模板
- skills.sh — 热门趋势，一键安装
- agent-skills.md — 6000+ 常用技能

### 源码仓库

- anthropics/skills — Anthropic 官方
- vercel-labs/skills — Vercel 官方（Web / 全栈）
- antfu/skills — antfu 维护，工程化好
- ZhanlinCui/Ultimate-Agent-Skills-Collection — 终极大杂烩
- JackyST0/awesome-agent-skills — 精选合集索引
- VoltAgent/awesome-openclaw-skills — OpenClaw 专属合集

### 使用原则（本地约束）

- 先看来源质量与维护状态，再决定是否引入。
- 先在隔离环境验证，再进主工作流。
- 默认只“推荐和评估”技能，不自动安装第三方技能。

### Daily Reflection 执行前检查（新增）

- 先执行：`git -C /root/.openclaw rev-parse --is-inside-work-tree`
- 若报 `Permission denied`：直接标记“目标路径不可达，备份失败但继续复盘”，不再执行 add/commit/push。
- 若报“not a git repository”：标记“非 Git 仓库，备份失败但继续复盘”，不再执行 add/commit/push。
- 原因与收益：先判定“可达性→仓库性”，避免重复无效命令，减少噪音报错并保证复盘主流程稳定完成。

### Daily Reflection 复盘证据最小集（新增）

- 至少同时核对：`memory/projects.md`、`memory/lessons.md`、`memory/今天.md`、`memory/昨天.md`。
- 若当日会话很少，额外以 `sessions_list` 确认“是否存在遗漏会话”。
- 输出问题项时必须给“现象-影响-改法”三段证据链，避免泛化结论。

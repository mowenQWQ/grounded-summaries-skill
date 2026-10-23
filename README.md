# grounded-summaries

**防止 AI Agent 在总结类任务中编造内容——来自一次真实的线上事故。**

**Prevent AI agents from fabricating daily summaries — born from a real production incident.**

[中文](#中文) | [English](#english)

> ⚠️ **AI 使用说明**：本作品由 AI 辅助生成（生成时间：2026-08-23）。仅供学习与参考使用，发布、引用或投入使用前请人工核实关键信息。

---

## 中文

一个防止 AI Agent 在总结类任务中编造内容的 skill（Claude / Agent Skills 格式）。

### 背景

来自一次真实的线上事故：一个 AI agent 收到定时总结任务，但当天没有任何对话。它没有输出"今日无记录"，而是从用户画像和记忆档案里拼凑出了一整天的活动——细节具体到小数点，甚至把虚构条目写入了持久化配置形成自证循环。直到用户看到报告问出那句"我什么时候问过？"

这个 skill 把事故的完整复盘（失败模式 → 触发机制 → 铁律 → 自检清单 → 示例）固化为可复用的防护规范。

### 适用场景

- AI agent 的每日/每周自动总结任务（重灾区）
- 任何基于对话历史或存储数据生成回顾、报告、变更日志的任务
- 审计 agent 生成的日志，检查是否存在编造内容

### 核心内容

- **失败模式**：空白日幻觉——数据为空时从画像生成"当天活动"
- **触发公式**：数据真空 × 强模板 × 高仿真素材在场 × 统计先验 × 无自检
- **六条铁律**：事实性输出只用当次工具返回；空数据写"无记录"；记忆档案≠当天事实等
- **写前自检清单**：溯源 / 画像污染 / 数字出处 / 空白合法性 / 持久化守门

### 安装

```bash
git clone https://github.com/mowenQWQ/grounded-summaries-skill.git
cp -r grounded-summaries-skill/grounded-summaries /path/to/your/agent/skills/
```

对于 Claude Code / OpenClaw 类环境，skills 目录通常是 `~/.claude/skills/` 或项目内的 `.claude/skills/`；其他 agent 框架请查阅各自的 skills 路径。

安装后无需任何配置——skill 通过 description 在总结类任务中自动触发。

### 给 Agent 维护者的一句话

如果你的 agent 跑在定时任务/无人值守环境里，最低成本的防幻觉措施是在总结任务的 prompt 里显式写入：

> "数据源为空时，输出'无记录'是正确行为。"

这一句话就能拆掉触发公式里的两个条件（任务前提暗示 + 统计先验）。完整的部署建议见 [SKILL.md](grounded-summaries/SKILL.md) 第六节。

### 更多技能库

| 仓库 | 简介 |
|------|------|
| [win-dev-pitfalls](https://github.com/mowenQWQ/win-dev-pitfalls) | Windows 开发踩坑全量主线 |
| [bat-ps1-dev](https://github.com/mowenQWQ/bat-ps1-dev) | bat/PowerShell 脚本开发专项经验库 |
| [Web-Security-Test-Rules](https://github.com/mowenQWQ/Web-Security-Test-Rules) | 已授权网站安全测试规则库 |
| [unattended-task-pitfalls](https://github.com/mowenQWQ/unattended-task-pitfalls) | 无人值守自动任务加固经验库 |
| [agent-mistake-patterns](https://github.com/mowenQWQ/agent-mistake-patterns) | AI 智能体犯错模式库与自我纠错纪律 |

### 许可

MIT

---

## English

A skill (Claude / Agent Skills format) that stops AI agents from fabricating content in summary tasks.

### Background

From a real production incident: an AI agent received a scheduled daily-summary task, but there had been no conversations that day. Instead of reporting "no records," it assembled an entire day of activity from the user profile and memory archives — details precise to the decimal point. It even wrote the fabricated entries into a persistent config file, creating a self-corroborating loop. Until the user saw the report and asked: *"When did I ever ask that?"*

This skill turns the full postmortem (failure mode → trigger mechanism → rules → pre-flight checklist → examples) into a reusable guardrail.

### Use Cases

- Daily/weekly automated summary tasks for AI agents (the worst-hit zone)
- Any retrospective, report, or changelog generated from conversation history or stored data
- Auditing agent-generated logs for fabricated content

### What's Inside

- **Failure mode**: the Blank-Day Hallucination — generating "today's activity" from the user profile when data is empty
- **Trigger formula**: Data Vacuum × Strong Template × High-Fidelity Material × Statistical Prior × No Verification
- **Six rules**: factual output only from current-session tool returns; empty data → "no records"; memory archives ≠ today's facts; and more
- **Pre-flight checklist**: traceability / profile contamination / number provenance / blank legitimacy / persistence gatekeeping

### Installation

```bash
git clone https://github.com/mowenQWQ/grounded-summaries-skill.git
cp -r grounded-summaries-skill/grounded-summaries /path/to/your/agent/skills/
```

For Claude Code / OpenClaw-style environments, the skills directory is typically `~/.claude/skills/` or `.claude/skills/` within a project; for other agent frameworks, check their respective skills paths.

Zero configuration after install — the skill auto-triggers on summary-type tasks via its description.

### One Line for Agent Maintainers

If your agent runs scheduled or unattended jobs, the cheapest anti-hallucination measure is to explicitly write into the summary-task prompt:

> "Outputting 'no records' when data sources are empty is correct behavior."

That single line defuses two conditions of the trigger formula (the hidden presupposition + the statistical prior). See [SKILL.md](grounded-summaries/SKILL.md) section 6 for full deployment advice.

### More Skill Repos

| Repo | What it does |
|------|--------------|
| [win-dev-pitfalls](https://github.com/mowenQWQ/win-dev-pitfalls) | Windows development pitfalls vault (full line) |
| [bat-ps1-dev](https://github.com/mowenQWQ/bat-ps1-dev) | Batch & PowerShell scripting vault |
| [Web-Security-Test-Rules](https://github.com/mowenQWQ/Web-Security-Test-Rules) | Authorized web security testing rules |
| [unattended-task-pitfalls](https://github.com/mowenQWQ/unattended-task-pitfalls) | Hardening playbook for unattended agent tasks |
| [agent-mistake-patterns](https://github.com/mowenQWQ/agent-mistake-patterns) | AI-agent mistake patterns & self-correction discipline |

### License

MIT

---

<div align="center">

<img src="https://cdn.openai.com/API/docs/images/codex-logo.png" alt="OpenAI Codex" width="80" />
&nbsp;&nbsp;&nbsp;
<img src="https://avatars.githubusercontent.com/u/150475366?s=80" alt="OpenClaw" width="80" />

# openclaw-codex-skill

**OpenAI Codex CLI Skill for OpenClaw**

An [OpenClaw](https://openclaw.ai) agent skill that enables full Codex CLI integration — write code, fix bugs, review PRs, and automate engineering tasks from your AI assistant.

[English](#english) · [中文](#中文)

</div>

---

<a name="english"></a>

## 🇬🇧 English

### What is this?

This is an [AgentSkill](https://agentskills.io) for [OpenClaw](https://openclaw.ai) that gives your AI assistant deep knowledge of the [OpenAI Codex CLI](https://developers.openai.com/codex/cli) — including installation, all commands, slash commands, approval modes, AGENTS.md configuration, Skills, MCP, Cloud tasks, and automation workflows.

### Features

- ✅ Full CLI reference (install, auth, models, flags)
- ✅ Interactive TUI usage and keyboard shortcuts
- ✅ Non-interactive / scripting mode (`codex exec`)
- ✅ Approval & sandbox modes
- ✅ Session resume and fork
- ✅ Code review workflows (`/review`)
- ✅ Slash commands quick reference
- ✅ AGENTS.md configuration
- ✅ MCP server integration
- ✅ Cloud task delegation
- ✅ Skills system
- ✅ Shell completions

### Installation

**Via ClawHub (recommended):**
```bash
clawhub install codex
```

**Manual:**
```bash
# Clone into your OpenClaw skills directory
git clone https://github.com/isyayanoaa/openclaw-codex-skill ~/.openclaw/workspace/skills/codex
```

### Usage

Once installed, OpenClaw will automatically activate this skill when you mention Codex:

> "用 codex 修复这个 bug"  
> "let codex review my PR"  
> "codex exec 帮我写单元测试"

### Requirements

- [OpenClaw](https://openclaw.ai) installed and running
- [OpenAI Codex CLI](https://developers.openai.com/codex/cli): `npm i -g @openai/codex`
- ChatGPT Plus / Pro / Business / Edu / Enterprise plan, or OpenAI API key

### Skill Structure

```
skills/codex/
├── SKILL.md      # Main skill instructions (loaded by OpenClaw)
└── README.md     # This file
```

---

<a name="中文"></a>

## 🇨🇳 中文

### 这是什么？

这是一个用于 [OpenClaw](https://openclaw.ai) 的 [AgentSkill](https://agentskills.io)，让你的 AI 助手全面掌握 [OpenAI Codex CLI](https://developers.openai.com/codex/cli) 的用法——包括安装配置、所有命令参数、斜杠命令、审批模式、AGENTS.md 配置、Skills 系统、MCP 集成、Cloud 任务委派和自动化工作流。

### 功能覆盖

- ✅ 完整 CLI 参考（安装、认证、模型选择、全局参数）
- ✅ 交互式 TUI 操作与键盘快捷键
- ✅ 非交互/脚本模式（`codex exec`）
- ✅ 审批模式与沙箱策略
- ✅ 会话恢复与分叉（resume / fork）
- ✅ 代码审查工作流（`/review`）
- ✅ 斜杠命令速查表
- ✅ AGENTS.md 配置说明
- ✅ MCP Server 集成
- ✅ Cloud 任务委派
- ✅ Skills 系统
- ✅ Shell 自动补全

### 安装方式

**通过 ClawHub（推荐）：**
```bash
clawhub install codex
```

**手动安装：**
```bash
git clone https://github.com/isyayanoaa/openclaw-codex-skill ~/.openclaw/workspace/skills/codex
```

### 使用方法

安装后，当你在 OpenClaw 中提到 Codex 时，skill 会自动激活：

> "用 codex 修复这个 bug"  
> "让 codex review 我的 PR"  
> "codex exec 帮我写单元测试"  
> "codex 怎么切换模型"

### 环境要求

- 已安装并运行 [OpenClaw](https://openclaw.ai)
- [OpenAI Codex CLI](https://developers.openai.com/codex/cli)：`npm i -g @openai/codex`
- ChatGPT Plus / Pro / Business / Edu / Enterprise 或 OpenAI API Key

### 文件结构

```
skills/codex/
├── SKILL.md      # Skill 主文件（OpenClaw 自动加载）
└── README.md     # 本文件
```

---

<div align="center">

**文档来源：** [developers.openai.com/codex](https://developers.openai.com/codex) · 更新于 2026-03-05

Made with ❤️ for [OpenClaw](https://openclaw.ai)

</div>

---
name: codex
description: "OpenAI Codex CLI - 写代码、修复bug、代码审查、添加测试"
---

# Codex Skill

调用 OpenAI Codex CLI 完成编码任务的完整参考指南。

> 文档来源：https://developers.openai.com/codex（2026-03-05 更新）

## 激活条件

用户提到以下内容时激活：
- "codex"、"用 codex"、"让 codex 帮我"、"调用 codex"

---

## 安装

```bash
# npm（推荐）
npm i -g @openai/codex

# 升级到最新
npm i -g @openai/codex@latest

# 或 Homebrew（macOS）
brew install --cask codex
```

支持平台：macOS、Linux；Windows 为实验性支持（建议用 WSL）。

---

## 认证

```bash
codex login                       # 浏览器 OAuth（ChatGPT 账号）
codex login --device-auth         # 设备码流程
printenv OPENAI_API_KEY | codex login --with-api-key  # API Key
codex login status                # 检查认证状态（返回 0 = 已登录）
codex logout                      # 移除凭证
```

需要 ChatGPT Plus / Pro / Business / Edu / Enterprise 计划。

---

## 模型

| 模型 | 说明 |
|------|------|
| `gpt-5.3-codex` | 默认推荐主力模型 |
| `gpt-5.3-codex-spark` | 极速版（1000+ tokens/s），Pro 用户 research preview |
| `gpt-5.2-codex` | API Key 用户默认 |

```bash
codex --model gpt-5.3-codex "任务"   # 启动时指定
# 会话中用 /model 切换
```

---

## 基本用法

### 交互式模式（TUI）

```bash
codex                          # 启动 TUI
codex "解释这个代码库"          # 带初始 prompt 启动
```

**TUI 快捷键：**

| 快捷键 | 作用 |
|--------|------|
| `@` | 模糊搜索文件并插入路径 |
| `!ls` | 行首加 `!` 直接执行 shell 命令 |
| `Enter`（运行中） | 注入新指令到当前 turn |
| `Tab`（运行中） | 排队下一个 turn |
| `Esc×2` | 编辑上一条消息，可溯源，Enter 从该点分叉 |
| `Ctrl+L` | 清屏但保留对话 |
| `Ctrl+G` | 用 `$EDITOR` 编辑长 prompt |
| `Ctrl+M` | 语音输入（App 内） |

### 非交互模式（推荐自动化使用）

```bash
codex exec "任务描述"           # 非交互执行（别名 codex e）
codex exec - < prompt.txt       # 从 stdin 读取 prompt
```

**`codex exec` 常用参数：**

| 参数 | 说明 |
|------|------|
| `--json` | 输出换行分隔的 JSON 事件流 |
| `--ephemeral` | 不持久化会话文件 |
| `--output-last-message, -o <path>` | 把最终消息写入文件 |
| `--output-schema <path>` | 用 JSON Schema 验证输出格式 |
| `--skip-git-repo-check` | 允许在非 Git 目录运行 |

---

## 全局参数

```bash
codex exec "任务" --full-auto                        # 自动审批 + workspace-write 沙箱
codex exec "任务" --ask-for-approval never           # 从不询问
codex exec "任务" --sandbox workspace-write          # 沙箱策略
codex exec "任务" --model gpt-5.3-codex             # 指定模型
codex exec "任务" --image screenshot.png            # 附加图片
codex exec "任务" --search                          # 启用实时网络搜索
codex exec "任务" -c key=value                      # 临时覆盖配置项
codex exec "任务" --profile myprofile               # 使用 config.toml 中的 profile
codex exec "任务" --add-dir /extra/path             # 追加可写目录
codex exec "任务" --dangerously-bypass-approvals-and-sandbox  # 危险：跳过所有限制（--yolo）
```

> ⚠️ 全局参数须放在子命令**之后**，如 `codex exec --full-auto "任务"`

---

## 审批模式（Approval Modes）

| 模式 | 参数 | 说明 |
|------|------|------|
| Auto（默认） | — | 可读写工作目录，出范围才询问 |
| Read-only | `--sandbox read-only` | 只读，变更前需审批计划 |
| Full Access | `--sandbox danger-full-access` | 无限制含网络，谨慎使用 |
| Full Auto | `--full-auto` | auto approve + workspace-write |

会话中用 `/permissions` 随时切换。

---

## 会话管理

```bash
codex resume                   # 交互选择历史会话
codex resume --last            # 直接恢复最近会话
codex resume --all             # 显示所有目录的会话
codex resume <SESSION_ID>      # 按 ID 恢复

# 非交互式恢复
codex exec resume --last "继续修复 race condition"
codex exec resume <UUID> "实现上次规划的方案"

codex fork                     # 分叉当前会话为新线程
```

---

## 代码审查

```bash
# 交互模式中输入 /review
# 或直接：
codex exec "review my changes for security issues"
```

**四种审查模式（`/review` 菜单）：**

| 模式 | 说明 |
|------|------|
| Review against a base branch | 对比上游分支，找 PR 前主要风险 |
| Review uncommitted changes | 审查所有未提交改动（含未追踪文件） |
| Review a commit | 查看特定 SHA 的变更集 |
| Custom review instructions | 自定义审查重点 |

---

## 图片输入

```bash
codex -i screenshot.png "解释这个错误"
codex --image img1.png,img2.jpg "总结这些图"  # 多图用逗号分隔或重复 -i
```

支持 PNG、JPEG 格式。

---

## 斜杠命令速查（Slash Commands）

| 命令 | 作用 |
|------|------|
| `/model` | 切换模型 |
| `/permissions` | 切换审批/沙箱级别 |
| `/personality` | 切换回复风格（`friendly`/`pragmatic`/`none`） |
| `/plan` | 进入计划模式（先规划再执行） |
| `/review` | 代码审查菜单 |
| `/diff` | 查看 Git diff（含未追踪文件） |
| `/compact` | 压缩对话历史为摘要（节省 token） |
| `/clear` | 清屏 + 新对话 |
| `/new` | 新对话（不清屏） |
| `/fork` | 分叉当前对话 |
| `/resume` | 恢复历史会话 |
| `/mention <file>` | 附加文件到对话 |
| `/copy` | 复制最近输出到剪贴板 |
| `/status` | 显示模型/策略/token 用量 |
| `/debug-config` | 显示配置层级和来源 |
| `/theme` | 打开主题选择器 |
| `/experimental` | 切换实验性功能 |
| `/agent` | 切换 sub-agent 线程（多智能体模式） |
| `/mcp` | 列出可用 MCP 工具 |
| `/apps` | 浏览 App connector |
| `/ps` | 显示后台终端及输出 |
| `/init` | 在当前目录生成 AGENTS.md |

---

## 配置

配置文件：`~/.codex/config.toml`

```toml
model = "gpt-5.3-codex"
web_search = "cached"    # "live" | "cached" | "disabled"

[tui]
theme = "Monokai"

[agents]
# 多智能体配置
```

**Profile 支持：**
```bash
codex exec --profile work "任务"   # 读取 config.toml 的 [profile.work] 段
```

**命令行临时覆盖（优先级最高）：**
```bash
codex exec -c model=gpt-5.3-codex -c web_search=live "任务"
```

---

## AGENTS.md

在项目根目录放 `AGENTS.md` 控制 Codex 行为：

```markdown
# AGENTS.md

## Review guidelines
- Don't log PII.
- Verify authentication middleware wraps every route.
- Treat typos in docs as P1.

## Coding conventions
- 使用 TypeScript strict mode
- 所有异步函数必须有错误处理
```

- 全局：`~/.codex/AGENTS.md`
- 仓库：项目根目录 `AGENTS.md`
- 子目录：可放更细粒度的 `AGENTS.md`
- 生成：`/init` 自动基于当前仓库生成

---

## MCP（Model Context Protocol）

```bash
# 添加 MCP Server
codex mcp add myserver -- npx my-mcp-server        # stdio
codex mcp add myserver --url https://mcp.example.com  # HTTP
codex mcp add myserver --url https://... --bearer-token-env-var MY_TOKEN

# 管理
codex mcp list
codex mcp remove myserver
codex mcp login/logout

# 以 MCP Server 模式运行 Codex
codex mcp-server
```

会话中用 `/mcp` 查看可用工具列表。

---

## Skills 系统

```bash
# 调用 skill
$skill-name "任务描述"

# skill 存放位置（按优先级）
~/.codex/skills/           # 用户全局 skills
.codex/skills/             # 项目级 skills（优先）
```

每个 skill 是一个文件夹，包含：
- `SKILL.md`（必须）— 说明和指令
- `scripts/`（可选）— 脚本
- `references/`（可选）— 参考文档
- `assets/`（可选）— 静态资源

官方 skills 仓库：https://github.com/openai/skills

---

## Cloud 集成

```bash
# 终端管理 Cloud 任务
codex cloud                                              # TUI 选择器
codex cloud exec --env ENV_ID "任务描述"                 # 启动 cloud task
codex cloud exec --env ENV_ID --attempts 3 "任务"       # best-of-3
codex cloud list --json --limit 10                       # 列出任务（脚本分页）

# 应用 cloud task 结果
codex apply                                              # 别名 codex a
```

---

## 功能标志（Feature Flags）

```bash
codex features list
codex features enable unified_exec
codex features disable shell_snapshot
```

写入 `~/.codex/config.toml`；使用 `--profile` 时写入对应 profile 文件。

---

## Shell 补全

```bash
codex completion bash | zsh | fish

# 写入 ~/.zshrc
eval "$(codex completion zsh)"
```

---

## Sandbox 调试

```bash
codex sandbox <命令>    # 在 Codex 沙箱内运行任意命令（实验性）
codex execpolicy        # 检查命令是否符合执行策略（实验性）
```

---

## 在 OpenClaw 中的使用示例

```bash
# 写代码
codex exec "用 Go 写一个快速排序，保存到 sort.go"

# 修复 bug（自动审批）
codex exec --full-auto "修复 user.go 中的 nil pointer bug"

# 代码审查（输出到文件）
codex exec -o review.md "review all uncommitted changes for security issues"

# 添加测试
codex exec "为 auth.go 添加完整单元测试"

# 图片辅助调试
codex exec -i error_screenshot.png "根据截图修复这个错误"

# 非 Git 目录使用
codex exec --skip-git-repo-check "整理这些脚本"

# 恢复上次会话继续工作
codex exec resume --last "继续实现之前规划的 API 接口"

# 结构化输出（JSON Schema 验证）
codex exec --json -o output.jsonl "分析这个仓库的依赖关系"
```

---

## 注意事项

- 默认在当前目录运行，敏感操作前确认工作目录
- `--full-auto` / `--yolo` 在生产环境慎用，建议只在 CI/隔离环境用
- `codex exec` 默认需要 Git 仓库；非 Git 目录用 `--skip-git-repo-check`
- 多任务并行时避免两个会话修改同一文件
- 配置优先级：`-c key=value` > `--profile` > 根 `config.toml`

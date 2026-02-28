---
name: codex
description: "OpenAI Codex CLI - 写代码、修复bug、代码审查、添加测试"
---

# Codex Skill

调用 OpenAI Codex CLI 来写代码的 skill。

## 激活条件

当用户提到以下内容时激活：
- "codex"
- "用 codex 写代码"
- "让 codex 帮我写"
- "调用 codex"
- "codex exec"

## 前置要求

需要安装 Codex CLI：

```bash
# macOS / Linux
curl -fsSL https://claude.ai/install.sh | bash -s -- --with-codex

# 或用 npm
npm install -g @openai/codex
```

登录：
```bash
codex login
```

## 基本用法

### 1. 交互模式 (常用)
```bash
codex
codex "解释这个代码库"
```

### 2. 非交互模式 (推荐用于 OpenClaw)
```bash
codex exec "你的任务描述"
```

常用参数：
- `--path <目录>` - 指定工作目录
- `--model <模型>` - 指定模型，如 gpt-5.3-codex
- `--yes` - 自动批准所有操作 (yolo 模式)

### 3. 继续之前的会话
```bash
codex resume --last
codex resume <session-id>
```

## 常用命令

### 代码审查
```bash
codex /review                    # 打开审查菜单
codex exec --yes "review uncommitted changes"
```

### 继续之前的工作
```bash
codex resume --last              # 继续最近的任务
codex resume <session-id>        # 继续指定任务
```

### 指定模型
```bash
codex --model gpt-5.3-codex "任务"
```

### 图像输入 (截图/设计稿)
```bash
codex -i screenshot.png "解释这个错误"
codex --image img1.png,img2.jpg "总结这些图表"
```

### Web 搜索
```bash
codex exec --search "最新React教程"  # 强制使用实时搜索
```

## 权限模式

- **Auto (默认)** - 可以读写工作目录，但访问外部需要确认
- **Read-only** - 只读模式，不会修改任何文件
- **Full Access** - 完全访问权限，包括网络

在交互模式中用 `/permissions` 切换。

## 快捷键

- `Ctrl+G` - 用编辑器编写长提示
- `@` - 快速插入文件路径
- `Tab` - 队列下一个问题
- `Esc Esc` - 编辑上一条消息
- `!ls` - 直接运行 shell 命令

## 在 OpenClaw 中使用

### 示例
```bash
# 写一个函数
codex exec "用 Go 写一个快速排序函数"

# 修复 bug
codex exec --yes "修复 user.go 中的 nil pointer bug"

# 代码审查
codex exec --yes "review uncommitted changes"

# 添加测试
codex exec "为 auth.go 添加单元测试"
```

## 模型

- `gpt-5.3-codex` - 默认模型
- `gpt-5.3-codex-spark` - 更快 (需要 ChatGPT Pro)

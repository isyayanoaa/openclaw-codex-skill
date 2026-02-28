# Codex Skill

一个用于 OpenClaw 的 Codex CLI 集成 Skill，可以帮助你完成各种编程任务。

## 什么是 Codex？

Codex 是 OpenAI 推出的 AI 编程助手，可以通过命令行交互来：
- 编写新代码
- 修复 bug
- 代码审查
- 添加单元测试
- 重构代码
- 解释代码库

## 安装

```bash
# macOS / Linux
curl -fsSL https://claude.ai/install.sh | bash -s -- --with-codex

# 或使用 npm
npm install -g @openai/codex
```

首次使用需要登录：

```bash
codex login
```

## 使用方法

### 交互模式

启动交互式会话：

```bash
codex
```

指定初始任务：

```bash
codex "解释这个代码库的结构"
```

### 非交互模式 (推荐)

直接执行任务并返回结果：

```bash
codex exec "写一个快速排序函数"
codex exec --yes "修复这个 bug"
```

### 继续之前的会话

```bash
codex resume --last    # 继续最近的任务
codex resume <session-id>  # 继续指定任务
```

## 常用场景

### 编写代码
```bash
codex exec "用 Python 写一个判断质数的函数"
```

### 修复 Bug
```bash
codex exec "修复 user.go 中的 nil pointer panic"
```

### 代码审查
```bash
codex exec --yes "review uncommitted changes"
codex /review  # 交互式审查
```

### 添加测试
```bash
codex exec "为 auth.go 添加单元测试"
```

### 解释代码
```bash
codex exec "解释 main.go 的逻辑"
```

### 图像输入
```bash
codex -i error.png "解释这个错误"
codex --image design.jpg "这个设计稿的实现建议"
```

## 常用参数

| 参数 | 说明 |
|------|------|
| `--path <目录>` | 指定工作目录 |
| `--yes` | 自动批准所有操作 (yolo模式) |
| `--model <模型>` | 指定模型 |
| `--cd <目录>` | 切换工作目录 |

## 权限模式

- **Auto (默认)** - 可以读写工作目录文件，访问外部需确认
- **Read-only** - 只读，不会修改任何文件
- **Full Access** - 完全访问，包括网络

用 `/permissions` 切换权限模式。

## 在 OpenClaw 中使用

当需要 Codex 帮忙时，直接说：
- "用 codex 写一个排序函数"
- "用 codex 修复这个 bug"
- "让 codex 审查这段代码"

我会自动调用 Codex CLI 来完成任务。

## 模型

- `gpt-5.3-codex` - 默认模型，适合大多数任务
- `gpt-5.3-codex-spark` - 更快 (需要 ChatGPT Pro 订阅)

## 参考

- [Codex 官方文档](https://developers.openai.com/codex/cli/features)

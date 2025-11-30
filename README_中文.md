<div align="center">

<h2 id="claude-code-community-guide">Claude Code 指南</h2>

*有关更新和贡献，请访问 [Claude Code 官方文档](https://claude.ai/code)*

![Claude Code](https://img.shields.io/npm/v/@anthropic-ai/claude-code?label=Claude%20Code&logo=anthropic)
[![状态](https://img.shields.io/badge/Status-Active-brightgreen)](https://github.com/anthropics/claude-code)
[![许可证](https://img.shields.io/badge/License-Anthropic-orange)](https://claude.ai/code)


</div>

<div align="center">

<kbd>

| 章节                                        | 状态          |
|---------------------------------------------|------------------------------|
| Windows、Linux、MacOS 安装指南              | ✅ |
| 技巧和窍门                                   | ✅ |
| MCP 概述及使用建议                           | ✅ |
| 社区指南                                     | ✅ |
| 故障排除                                     | ✅ |
| Claude Code 最佳使用方法                     | ✅ |

### 如何通过 Discord 使用 Claude Code [点击这里!](https://github.com/zebbern/claude-code-discord)


</kbd>

#### [点击查看每日更新的 Claude 变更日志和新闻](https://github.com/zebbern/claude-code-guide/tree/main/Official%20Claude%20Releases)

</div>

---

<h3 id="content">目录</h3>

_快速链接:_ [安装](#quick-start) · [命令](#claude-commands) · [快捷键](#keyboard-shortcuts) · [MCP](#mcp-integration) · [故障排除](#help--troubleshooting)

- **[快速开始](#getting-started)**
  - [快速启动](#quick-start)
  - [初始设置](#initial-setup)

- **[配置与环境](#configuration--environment)**
  - [环境变量](#environment-variables)
  - [配置文件](#configuration-files)

- **[命令与使用](#commands--usage)**
  - [Claude 命令](#claude-commands)
  - [速查表](#cheat-sheet)

- **[界面与输入](#interface--input)**
  - [键盘快捷键](#keyboard-shortcuts)
  - [Vim 模式](#vim-mode)

- **[高级功能](#advanced-features)**
  - [子代理](#sub-agents)
  - [MCP 集成](#mcp-integration)
  - [钩子系统](#hooks-system)

- **[安全与权限](#security--permissions)**
  - [危险模式](#dangerous-mode)
  - [安全最佳实践](#security-best-practices-main)

- **[自动化与集成](#automation--integration)**
  - [自动化与脚本](#automation--scripting-with-claude-code)
  - [自动 PR 审查](#auto-pr-review-inline-comments)
  - [问题分类](#issue-triage-suggest-labels--severity)

- **[帮助与故障排除](#help--troubleshooting)**
  - [安装问题](#installation--nodejs-issues)
  - [MCP 问题](#mcp-model-context-protocol-issues)
  - [最佳实践](#best-practices)

- **[第三方集成](#third-party-integrations)**
  - [DeepSeek 集成](#deepseek-integration)


---

<h1 id="getting-started">快速开始</h1>

**当 claude 完成任务时启用声音提醒:**
>
> <kbd>claude config set --global preferredNotifChannel terminal_bell</kbd>
<h2 id="quick-start">快速启动</h2>

> [!TIP]
> **在终端中发送 <mark>claude</mark> 或 <mark>npx claude</mark> 启动界面**
>
> **前往 [帮助与故障排除](#help--troubleshooting) 修复问题...**
```C
# Node.js 18+⭐️
/*通用方法                */ npm install -g @anthropic-ai/claude-code
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Windows
/* 通过 CMD              */ npm install -g @anthropic-ai/claude-code
/* 通过 Powershell       */ irm https://claude.ai/install.ps1 | iex
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# WSL/GIT
/* 通过终端              */ npm install -g @anthropic-ai/claude-code
/* 通过终端              */ curl -fsSL https://claude.ai/install.sh | bash
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# MacOS                  */ brew install node && npm install -g @anthropic-ai/claude-code
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Linux
/* 通过终端              */ sudo apt update && sudo apt install -y nodejs npm
/* 通过终端              */ npm install -g @anthropic-ai/claude-code
/* 通过终端              */ curl -fsSL https://claude.ai/install.sh | bash
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Arch
/* 通过终端              */ yay -S claude-code*/
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Docker
/* Windows (CMD)        */ docker run -it --rm -v "%cd%:/workspace" -e ANTHROPIC_API_KEY="sk-your-key" node:20-slim bash -lc "npm i -g @anthropic-ai/claude-code && cd /workspace && claude"
/* macOS/Linux (bash/zsh)*/ docker run -it --rm -v "$PWD:/workspace" -e ANTHROPIC_API_KEY="sk-your-key" node:20-slim bash -lc 'npm i -g @anthropic-ai/claude-code && cd /workspace && claude'
/* 无 bash 备选方案      */ docker run -it --rm -v "$PWD:/workspace" -e ANTHROPIC_API_KEY="sk-your-key" node:20-slim sh -lc 'npm i -g @anthropic-ai/claude-code && cd /workspace && claude'
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# 检查 claude 是否正确安装
/* Linux                */ which claude
/* Windows              */ where claude
/* 通用                  */ claude --version
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# 常用管理命令
/*claude config         */ 配置设置
/*claude mcp list       */ 设置 MCP 服务器，也可以用 add/remove 替换 "list"
/*claude /agents        */ 配置/设置子代理用于不同任务
/*claude update         */ 更新到最新版本
```

---

> [!Tip]
> <ins>**通过终端打开项目到 VS Code / Cursor**</ins>
>  ### $ - <kbd>cd /path/to/project</kbd>
>  ### $ - <kbd>code .</kbd>
>
**确保您在 VS Code / Cursor 中安装了 <mark>(Claude Code 扩展)</mark>**

---

<h2 id="system-requirements">系统要求</h2>

> - 操作系统: macOS 10.15+, Ubuntu 20.04+/Debian 10+, 或 Windows 10/11 或 WSL

> - 硬件: 最低 4GB RAM，推荐 8GB+

> - 软件: Node.js 18+ 或 git 2.23+ (可选) 以及 GitHub 或 GitLab CLI 用于 PR 工作流 (可选)

> - 网络: 需要互联网连接进行 API 调用

> - Node.js 18+


---

<h2 id="initial-setup">初始设置</h2>

> [!Tip]
> **从 [Anthropic 控制台](https://console.anthropic.com) 获取 API 密钥**
>
> **不要提交真实密钥，使用 git-ignored 文件、操作系统密钥存储或密钥管理器**
```C
# 通用
/* 开始登录流程                      */ claude /login
/* 设置长期认证令牌                   */ claude setup-token
----------------------------------------------------------------------------------------------------------------------------------
# Windows
/* 设置-api-key       */ set ANTHROPIC_API_KEY=sk-your-key-here-here
/* cmd-masked-check  */ echo OK: %ANTHROPIC_API_KEY:~0,8%***
/* 设置-持久-key      */ setx ANTHROPIC_API_KEY "sk-your-key-here-here"
/* cmd-unset-key     */ set ANTHROPIC_API_KEY=
----------------------------------------------------------------------------------------------------------------------------------
# Linux
/* 设置-api-key       */ export ANTHROPIC_API_KEY="sk-your-key-here-here"
/* masked-check      */ echo "OK: ${ANTHROPIC_API_KEY:0:8}***"
/* remove-session    */ unset ANTHROPIC_API_KEY
----------------------------------------------------------------------------------------------------------------------------------
# Powershell
/* ps-session        */ $env:ANTHROPIC_API_KEY = "sk-your-key-here-here"
/* ps-masked-check   */ "OK: $($env:ANTHROPIC_API_KEY.Substring(0,8))***"
/* ps-persist        */ [Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY","sk-your-key-here-here","User")
/* ps-rotate         */ $env:ANTHROPIC_API_KEY = "sk-new-key"
/* ps-remove         */ Remove-Item Env:\ANTHROPIC_API_KEY
----------------------------------------------------------------------------------------------------------------------------------
# 其他...
# persist-bash/*     */ echo 'export ANTHROPIC_API_KEY="sk-your-key-here-here"' >> ~/.bashrc && source ~/.bashrc
# persist-zsh /*     */ echo 'export ANTHROPIC_API_KEY="sk-your-key-here-here"' >> ~/.zshrc  && source ~/.zshrc
# persist-fish/*     */ fish -lc 'set -Ux ANTHROPIC_API_KEY sk-your-key-here-here'
----------------------------------------------------------------------------------------------------------------------------------
```

---

<h1 id="configuration--environment">配置与环境</h1>

<h2 id="environment-variables">环境变量</h2>

> **您也可以在 settings.json 的 "env" 键下设置这些变量以便自动应用。**

> [!Important]
> **Windows 用户将 <kbd>export</kbd> 替换为 <kbd>set</kbd> 或 <kbd>setx</kbd> 用于永久设置**
```bash
# 环境开关 (放在 ~/.bashrc 或 ~/.zshrc 中)
export ANTHROPIC_API_KEY="sk-your-key-here-here"      # API 密钥作为 X-Api-Key 头发送 (交互使用: /login)
export ANTHROPIC_AUTH_TOKEN="my-auth-token"           # 自定义 Authorization 头; Claude 自动添加 "Bearer " 前缀
export ANTHROPIC_CUSTOM_HEADERS="X-Trace-Id: 12345"   # 额外的请求头 (格式: "Name: Value")

export ANTHROPIC_MODEL="claude-sonnet-4-20250514"                # 使用的自定义模型名称
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-20250514" # 默认 Sonnet 模型别名
export ANTHROPIC_DEFAULT_OPUS_MODEL="claude-opus-4-20250514"     # 默认 Opus 模型别名
export ANTHROPIC_SMALL_FAST_MODEL="haiku-model"                  # 用于后台任务的 Haiku 类模型 (占位符)
export ANTHROPIC_SMALL_FAST_MODEL_AWS_REGION="REGION"            # 在 Bedrock 上覆盖小型/快速模型的 AWS 区域 (占位符)

export AWS_BEARER_TOKEN_BEDROCK="bedrock_..."         # 用于认证的 Amazon Bedrock API 密钥/令牌

export BASH_DEFAULT_TIMEOUT_MS=60000                  # 长时间运行 bash 命令的默认超时时间 (毫秒)
export BASH_MAX_TIMEOUT_MS=300000                     # 长时间运行 bash 命令的最大超时时间 (毫秒)
export BASH_MAX_OUTPUT_LENGTH=20000                   # bash 输出在中间截断前的最大字符数

export CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR=1     # (0 或 1) 每个 Bash 命令后返回原始项目目录
export CLAUDE_CODE_API_KEY_HELPER_TTL_MS=600000       # 使用 apiKeyHelper 时刷新凭证的间隔 (毫秒)
export CLAUDE_CODE_IDE_SKIP_AUTO_INSTALL=1            # (0 或 1) 跳过 IDE 扩展的自动安装
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=4096             # 大多数请求的最大输出令牌数

export CLAUDE_CODE_USE_BEDROCK=1                      # (0 或 1) 使用 Amazon Bedrock
export CLAUDE_CODE_USE_VERTEX=0                       # (0 或 1) 使用 Google Vertex AI
export CLAUDE_CODE_SKIP_BEDROCK_AUTH=0                # (0 或 1) 跳过 Bedrock 的 AWS 认证 (例如，通过 LLM 网关)
export CLAUDE_CODE_SKIP_VERTEX_AUTH=0                 # (0 或 1) 跳过 Vertex 的 Google 认证 (例如，通过 LLM 网关)

export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=0     # (0 或 1) 禁用非必要流量 (等同于下面的 DISABLE_*)
export CLAUDE_CODE_DISABLE_TERMINAL_TITLE=0           # (0 或 1) 禁用自动终端标题更新

export DISABLE_AUTOUPDATER=0                          # (0 或 1) 禁用自动更新 (覆盖 autoUpdates 设置)
export DISABLE_BUG_COMMAND=0                          # (0 或 1) 禁用 /bug 命令
export DISABLE_COST_WARNINGS=0                        # (0 或 1) 禁用成本警告消息
export DISABLE_ERROR_REPORTING=0                      # (0 或 1) 选择退出 Sentry 错误报告
export DISABLE_NON_ESSENTIAL_MODEL_CALLS=0            # (0 或 1) 禁用非关键路径的模型调用
export DISABLE_TELEMETRY=0                            # (0 或 1) 选择退出 Statsig 遥测

export HTTP_PROXY="http://proxy:8080"                 # HTTP 代理服务器 URL
export HTTPS_PROXY="https://proxy:8443"               # HTTPS 代理服务器 URL

export MAX_THINKING_TOKENS=0                          # (0 或 1 关闭/开启) 为模型强制思考预算
export MCP_TIMEOUT=120000                             # MCP 服务器启动超时时间 (毫秒)
export MCP_TOOL_TIMEOUT=60000                         # MCP 工具执行超时时间 (毫秒)
export MAX_MCP_OUTPUT_TOKENS=25000                    # MCP 工具响应中允许的最大令牌数 (默认 25000)

export USE_BUILTIN_RIPGREP=0                          # (0 或 1) 设置为 0 使用系统安装的 rg 而非捆绑版本

export VERTEX_REGION_CLAUDE_3_5_HAIKU="REGION"        # Vertex AI 上 Claude 3.5 Haiku 的区域覆盖
export VERTEX_REGION_CLAUDE_3_5_SONNET="REGION"       # Vertex AI 上 Claude 3.5 Sonnet 的区域覆盖
export VERTEX_REGION_CLAUDE_3_7_SONNET="REGION"       # Vertex AI 上 Claude 3.7 Sonnet 的区域覆盖
export VERTEX_REGION_CLAUDE_4_0_OPUS="REGION"         # Vertex AI 上 Claude 4.0 Opus 的区域覆盖
export VERTEX_REGION_CLAUDE_4_0_SONNET="REGION"       # Vertex AI 上 Claude 4.0 Sonnet 的区域覆盖
export VERTEX_REGION_CLAUDE_4_1_OPUS="REGION"         # Vertex AI 上 Claude 4.1 Opus 的区域覆盖
```

<h2 id="global-config-options">全局配置选项</h2>

```bash
claude config set -g theme dark                               # 主题: dark | light | light-daltonized | dark-daltonized
claude config set -g preferredNotifChannel iterm2_with_bell   # 通知渠道: iterm2 | iterm2_with_bell | terminal_bell | notifications_disabled
claude config set -g autoUpdates true                         # 自动下载和安装更新 (重启时应用)
claude config set -g verbose true                             # 显示完整的 bash/命令输出

claude config set -g includeCoAuthoredBy false                # 在 git 提交/PR 中省略 "co-authored-by Claude"
claude config set -g forceLoginMethod console                 # 限制登录到 Anthropic 控制台 (API 计费)
claude config set -g model "claude-3-5-sonnet-20241022"       # 默认模型覆盖
claude config set -g statusLine '{"type":"command","command":"~/.claude/statusline.sh"}'  # 自定义状态栏

claude config set -g enableAllProjectMcpServers true              # 自动批准来自 .mcp.json 的所有 MCP 服务器
claude config set -g enabledMcpjsonServers '["memory","github"]'  # 批准特定的 MCP 服务器
claude config set -g disabledMcpjsonServers '["filesystem"]'      # 拒绝特定的 MCP 服务器
```
> [!Important]
> **Windows 用户将 <kbd>export</kbd> 替换为 <kbd>set</kbd>**
```bash
export DISABLE_AUTOUPDATER=1                      # 全局关闭自动更新 (覆盖 autoUpdates)
export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1 # 禁用非必要流量 (等同于下面的 DISABLE_* 开关)
export DISABLE_TELEMETRY=1                        # 选择退出 Statsig 遥测
export DISABLE_ERROR_REPORTING=1                  # 选择退出 Sentry 错误报告
export DISABLE_BUG_COMMAND=1                      # 禁用 /bug 命令
export DISABLE_COST_WARNINGS=0                    # 保留成本警告 (设置为 1 隐藏)
export DISABLE_NON_ESSENTIAL_MODEL_CALLS=1        # 跳过非关键模型调用 (风格文本等)

export CLAUDE_CODE_DISABLE_TERMINAL_TITLE=1       # 停止自动更新终端标题
export CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR=1 # 每个 Bash 命令后返回原始项目目录
export CLAUDE_CODE_IDE_SKIP_AUTO_INSTALL=1        # 跳过 IDE 扩展的自动安装
export USE_BUILTIN_RIPGREP=0                      # 使用系统 'rg' (0) 而非捆绑的 'rg'

export MAX_THINKING_TOKENS=0                      # (0 或 1 关闭/开启) 为模型强制思考预算
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=4096         # 限制典型响应大小 (示例值)

export HTTP_PROXY="http://proxy.company:8080"     # HTTP 代理 (如果需要)
export HTTPS_PROXY="https://proxy.company:8443"   # HTTPS 代理 (如果需要)
```

<h2 id="configuration-files">配置文件</h2>

**(内存类型) Claude Code 在分层结构中提供四个内存位置，每个都有不同的用途:**

| 内存类型                    | 位置                                                                                                                                                | 用途                                             | 使用案例示例                                                    | 共享对象                        |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- | -------------------------------------------------------------------- | ------------------------------- |
| **企业策略**               | macOS: `/Library/Application Support/ClaudeCode/CLAUDE.md`<br />Linux: `/etc/claude-code/CLAUDE.md`<br />Windows: `C:\ProgramData\ClaudeCode\CLAUDE.md` | 由 IT/DevOps 管理的组织范围指令                     | 公司编码标准、安全策略、合规要求                                      | 组织中的所有用户                |
| **项目内存**               | `./CLAUDE.md`                                                                                                                                           | 项目的团队共享指令                                   | 项目架构、编码标准、常见工作流                                        | 通过源代码控制的团队成员         |
| **用户内存**               | `~/.claude/CLAUDE.md`                                                                                                                                   | 所有项目的个人偏好                                   | 代码样式偏好、个人工具快捷方式                                        | 只有您 (所有项目)               |
| **项目内存 (本地)**        | `./CLAUDE.local.md`                                                                                                                                     | 个人项目特定偏好                                     | *(已弃用，见下文)* 您的沙盒 URL、首选测试数据                         | 只有您 (当前项目)               |

>所有内存文件在启动 Claude Code 时自动加载到上下文中。层次结构中较高的文件优先并首先加载，为更具体的内存构建基础。

---

<h1 id="commands--usage">命令与使用</h1>

<h2 id="claude-commands">Claude 命令</h2>

| 命令                      | 用途                                                                                                                                      |
| :------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------- |
| `/add-dir`                | 添加额外的工作目录                                                                                                                        |
| `/agents`                 | 管理专门任务的自定义 AI 子代理                                                                                                             |
| `/bug`                    | 报告错误 (将对话发送给 Anthropic)                                                                                                         |
| `/clear`                  | 清除对话历史                                                                                                                              |
| `/compact [instructions]` | 压缩对话并可选提供焦点指令                                                                                                                |
| `/config`                 | 查看/修改配置                                                                                                                             |
| `/cost`                   | 显示令牌使用统计和计费信息                                                                                                                |
| `/doctor`                 | 检查您的 Claude Code 安装健康状态                                                                                                         |
| `/help`                   | 获取使用帮助                                                                                                                              |
| `/init`                   | 使用 CLAUDE.md 指南初始化项目                                                                                                              |
| `/login`                  | 切换 Anthropic 账户                                                                                                                       |
| `/logout`                 | 从您的 Anthropic 账户登出                                                                                                                 |
| `/mcp`                    | 管理 MCP 服务器连接和 OAuth 认证                                                                                                           |
| `/memory`                 | 编辑 CLAUDE.md 内存文件                                                                                                                    |
| `/model`                  | 选择或更改 AI 模型                                                                                                                         |
| `/permissions`            | 查看或更新工具权限                                                                                                                        |
| `/pr_comments`            | 查看拉取请求评论                                                                                                                          |
| `/review`                 | 请求代码审查                                                                                                                              |
| `/status`                 | 查看账户和系统状态                                                                                                                        |
| `/terminal-setup`         | 为换行安装 Shift+Enter 键绑定 (仅 iTerm2 和 VSCode)                                                                                        |
| `/vim`                    | 进入 vim 模式以便在插入和命令模式之间切换                                                                                                  |

<h2 id="command-line-flags">命令行标志</h2>

| 标志 / 命令                            | 描述                                                                                                                                              | 示例                                                     |
| :----------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------- |
| `-d, --debug`                              | 启用调试模式 (显示详细调试输出)。  | `claude -d -p "query"`                   |
| `--include-partial-messages`                | 通过 CLI 标志支持部分消息流  |
| `--mcp-debug`                               | [已弃用] MCP 调试模式 (显示 MCP 服务器错误)。请改用 `--debug`。                                                                             | `claude --mcp-debug`                                        |
| `--verbose`                                 | 从配置覆盖详细模式设置 (显示扩展日志/逐轮输出)。                                                                | `claude --verbose`                                          |
| `-p, --print`                               | 打印响应并退出 (对管道输出有用)。                                                                                                                     | `claude -p "query"`                                         |
| `--output-format <format>`                  | 输出格式 (仅适用于 `--print`): `text` (默认), `json` (单个结果), 或 `stream-json` (实时流)。                              | `claude -p "query" --output-format json`                    |
| `--input-format <format>`                   | 输入格式 (仅适用于 `--print`): `text` (默认) 或 `stream-json` (实时流输入)。                                                  | `claude -p --output-format stream-json --input-format stream-json` |
| `--replay-user-messages`                    | 将来自 stdin 的用户消息重新发送到 stdout 进行确认 — **仅适用于** `--input-format=stream-json` **和** `--output-format=stream-json`。 | `claude --input-format stream-json --output-format stream-json --replay-user-messages` |
| `--allowedTools`, `--allowed-tools <tools...>`  | 允许的工具名称的逗号/空格分隔列表 (例如 `"Bash(git:*) Edit"`)。                                                                           | `--allowed-tools "Bash(git:*)" Edit"`                       |
| `--disallowedTools`, `--disallowed-tools <tools...>` | 拒绝的工具名称的逗号/空格分隔列表 (例如 `"Bash(git:*) Edit"`)。                                                                            | `--disallowed-tools "Edit"`                                 |
| `--mcp-config <configs...>`                 | 从 JSON 文件或字符串加载 MCP 服务器 (空格分隔)。                                                                                          | `claude --mcp-config ./mcp-servers.json`                    |
| `--strict-mcp-config`                       | 仅使用来自 `--mcp-config` 的 MCP 服务器，忽略其他 MCP 配置。                                                                             | `claude --mcp-config ./a.json --strict-mcp-config`          |
| `--append-system-prompt <prompt>`           | 将系统提示追加到默认系统提示 (在打印模式下有用)。                                                                              | `claude -p --append-system-prompt "Do X then Y"`            |
| `--permission-mode <mode>`                  | 会话的权限模式 (选择包括 `acceptEdits`, `bypassPermissions`, `default`, `plan`)。                                                 | `claude --permission-mode plan`                             |
| `--permission-prompt-tool <tool>`           | 指定一个 MCP 工具来处理非交互模式下的权限提示。                                                                               | `claude -p --permission-prompt-tool mcp_auth_tool "query"`  |
| `--fallback-model <model>`                  | 当默认模型过载时启用自动回退到指定模型 (注意: 根据帮助仅适用于 `--print`)。                                 | `claude -p --fallback-model claude-haiku-20240307 "query"`  |
| `--model <model>`                            | 当前会话的模型。接受别名如 `sonnet`/`opus` 或完整模型名称 (例如 `claude-sonnet-4-20250514`)。                               | `claude --model sonnet`                                     |
| `--settings <file-or-json>`                  | 从 JSON 文件或 JSON 字符串加载额外设置。                                                                                              | `claude --settings ./settings.json`                         |
| `--add-dir <directories...>`                 | 允许工具访问的额外目录。                                                                                                          | `claude --add-dir ../apps ../lib`                           |
| `--ide`                                      | 如果恰好有一个有效的 IDE 可用，则在启动时自动连接到 IDE。                                                                        | `claude --ide`                                              |
| `-c, --continue`                             | 继续当前目录中最近的对话。                                                                                          | `claude --continue`                                         |
| `-r, --resume [sessionId]`                   | 恢复对话；提供会话 ID 或交互式选择一个。                                                                                 | `claude -r "abc123"`                                        |
| `--session-id <uuid>`                        | 为对话使用特定的会话 ID (必须是有效的 UUID)。                                                                                   | `claude --session-id 123e4567-e89b-12d3-a456-426614174000`  |
| `--dangerously-skip-permissions`             | 绕过所有权限检查 (仅用于受信任的沙盒)。                                                                                               | `claude --dangerously-skip-permissions`                     |
| `-v, --version`                              | 显示已安装的 `claude` CLI 版本。                                                                                                                 | `claude --version`                                          |
| `-h, --help`                                 | 显示帮助/使用信息。                                                                                                                                     | `claude --help`                                             |


> `--output-format json` 标志对于脚本和自动化特别有用，允许您以编程方式解析 Claude 的响应。

<h2 id="cheat-sheet">速查表</h2>

```md
## Claude 速查表
# 基础 / 交互式
claude                                 # 启动交互式 REPL
claude "explain this project"          # 启动带种子提示的 REPL
claude -p "summarize README.md"        # 非交互式打印模式 (SDK 支持)
cat logs.txt | claude -p "explain"     # 将输入通过管道传递给 Claude 并退出
claude -c                              # 继续最近的对话 (--continue 的别名)
claude -r "<session-id>" "finish this" # 通过 ID 恢复特定会话 (--resume 的别名)
claude --model claude-sonnet-4-20250514# 为本次运行选择模型
claude --max-turns 3 -p "lint this"    # 在打印模式下限制代理轮数
claude --replay-user-messages          # 将用户消息重播到 stdout 用于调试/SDK 工作流

# 更新和安装
claude update                          # 手动更新 Claude Code
claude doctor                          # 诊断安装/版本和设置
claude install                         # 启动原生二进制安装程序 (测试版)
claude migrate-installer               # 从全局 npm 迁移到本地安装程序

# 配置: 交互式向导 + 直接操作
claude config                          # 交互式配置向导
claude config get <key>                # 获取值 (例如, claude config get theme)
claude config set <key> <val>          # 设置值 (例如, claude config set theme dark)
claude config add <key> <vals…>        # 追加到数组类型键 (例如, claude config add env DEV=1)
claude config remove <key> <vals…>     # 从列表类型键中删除项目
claude config list                     # 显示项目的所有当前设置 (项目范围是默认)

# 项目范围设置示例
claude config set model "claude-3-5-sonnet-20241022"   # 为此项目覆盖默认模型
claude config set includeCoAuthoredBy false            # 在 git/PR 中禁用 "co-authored-by Claude" 署名
claude config set forceLoginMethod claudeai            # 限制登录流程: claudeai | console
claude config set enableAllProjectMcpServers true      # 自动批准来自 .mcp.json 的所有 MCP 服务器
claude config set defaultMode "acceptEdits"            # 设置默认权限模式
claude config set disableBypassPermissionsMode disable # 阻止 bypassPermissions 模式 (示例键)

# 管理列表设置 (项目范围)
claude config add enabledMcpjsonServers github         # 批准来自 .mcp.json 的特定 MCP 服务器
claude config add enabledMcpjsonServers memory         # 添加另一个
claude config remove enabledMcpjsonServers memory      # 删除一个条目
claude config add disabledMcpjsonServers filesystem    # 明确拒绝特定的 MCP 服务器

# 全局范围 (使用 -g 或 --global)
claude config set -g autoUpdates false                 # 全局关闭自动更新
claude config set --global preferredNotifChannel iterm2_with_bell
claude config set -g theme dark                        # 主题: dark | light | light-daltonized | dark-daltonized
claude config set -g verbose true                      # 在任何地方显示完整的 bash/命令输出
claude config get -g theme                             # 确认全局值

# MCP (模型上下文协议) 管理
claude mcp                          # 启动 MCP 向导 / 配置 MCP 服务器
claude mcp list                     # 列出已配置的 MCP 服务器
claude mcp get <name>               # 显示服务器详细信息
claude mcp remove <name>            # 删除服务器
claude mcp add <name> <command> [args...]                 # 添加本地 stdio 服务器
claude mcp add --transport sse <name> <url>               # 添加远程 SSE 服务器
claude mcp add --transport http <name> <url>              # 添加远程 HTTP 服务器
claude mcp add <name> --env KEY=VALUE -- <cmd> [args...]  # 将环境传递给服务器命令
claude mcp add --transport sse private-api https://api.example/mcp \
  --header "Authorization: Bearer TOKEN"                  # 使用认证头添加
claude mcp add-json <name> '<json>'                       # 通过 JSON blob 添加服务器
claude mcp add-from-claude-desktop                        # 从 Claude Desktop 导入服务器
claude mcp reset-project-choices                          # 重置项目 .mcp.json 服务器的批准
claude mcp serve                                          # 将 Claude Code 本身作为 MCP stdio 服务器运行

# 其他有用的标志 (打印 / SDK 模式)
claude --add-dir ../apps ../lib                     # 添加额外的工作目录
claude --allowedTools "Bash(git log:*)" "Read"      # 允许列出的工具而无需权限提示
claude --disallowedTools "Edit"                     # 不允许列出的工具而无需权限提示
claude --append-system-prompt "Custom instruction"  # 追加到系统提示 (仅适用于 -p)
claude -p "query" --output-format json --input-format stream-json  # 控制脚本的 IO 格式
claude --verbose                                    # 详细日志 (逐轮)
claude --dangerously-skip-permissions               # 跳过权限提示 (谨慎使用)

# 快速验证 / 注释
# - 项目范围是 'claude config' 的默认; 使用 -g/--global 影响所有项目。
# - 设置优先级: 企业 > CLI 参数 > 本地项目 > 共享项目 > 用户 (~/.claude)。
# - 仅对列表类型键使用 'add' / 'remove' (例如, enabledMcpjsonServers)。
# - CLI 参考和发布说明是标志和最新添加的权威来源。
```

---

<h1 id="interface--input">界面与输入</h1>

<h2 id="keyboard-shortcuts">键盘快捷键</h2>

| 快捷键           | 描述                        | 上下文                     |
| :--------------- | :--------------------------------- | :------------------------- |
| `Ctrl+C`         | 取消当前输入或生成              | 标准中断                   |
| `Ctrl+D`         | 退出 Claude Code 会话           | EOF 信号                   |
| `Ctrl+L`         | 清除终端屏幕                    | 保留对话历史               |
| `Up/Down arrows` | 导航命令历史                    | 回忆之前的输入             |
| `Esc` + `Esc`    | 编辑上一条消息                  | 双击 escape 修改           |

<h3 id="multiline-input">多行输入</h3>

| 方法             | 快捷键         | 上下文                            |
| :--------------- | :------------- | :-------------------------------- |
| 快速转义         | `\` + `Enter`  | 在所有终端中工作                  |
| macOS 默认       | `Option+Enter` | macOS 上的默认设置                |
| 终端设置         | `Shift+Enter`  | 执行 `/terminal-setup` 后         |
| 控制序列         | `Ctrl+J`       | 多行的换行符                      |
| 粘贴模式         | 直接粘贴       | 对于代码块、日志                  |

<h3 id="quick-commands">快速命令</h3>

| 快捷键       | 描述                        | 注释                                                     |
| :----------- | :--------------------------------- | :-------------------------------------------------------- |
| `#` 开头     | 内存快捷方式添加到 CLAUDE.md        | 提示文件选择                                              |
| `/` 开头     | 斜杠命令                           |

<h2 id="vim-mode">Vim 模式</h2>

> [!Note]
>  使用 `/vim` 命令启用 vim 风格编辑或通过 `/config` 永久配置。

<h3 id="vim-mode-switching">Vim 模式切换</h3>

| 命令    | 动作                        | 来源模式 |
| :------ | :-------------------------- | :-------- |
| `Esc`   | 进入 NORMAL 模式            | INSERT    |
| `i`     | 在光标前插入                | NORMAL    |
| `I`     | 在行首插入                  | NORMAL    |
| `a`     | 在光标后插入                | NORMAL    |
| `A`     | 在行尾插入                  | NORMAL    |
| `o`     | 在下方开新行                | NORMAL    |
| `O`     | 在上方开新行                | NORMAL    |

<h3 id="vim-navigation">Vim 导航</h3>

| 命令            | 动作                      |
| :-------------- | :------------------------ |
| `h`/`j`/`k`/`l` | 向左/下/上/右移动         |
| `w`             | 下一个单词                |
| `e`             | 单词末尾                  |
| `b`             | 上一个单词                |
| `0`             | 行首                      |
| `$`             | 行尾                      |
| `^`             | 第一个非空白字符          |
| `gg`            | 输入开头                  |
| `G`             | 输入结尾                  |

<h3 id="vim-editing">Vim 编辑</h3>

| 命令           | 动作                    |
| :------------- | :---------------------- |
| `x`            | 删除字符                |
| `dd`           | 删除行                  |
| `D`            | 删除到行尾              |
| `dw`/`de`/`db` | 删除单词/到末尾/向后    |
| `cc`           | 更改行                  |
| `C`            | 更改到行尾              |
| `cw`/`ce`/`cb` | 更改单词/到末尾/向后    |
| `.`            | 重复上次更改            |

> [!Tip]
> 在终端设置中配置您首选的换行行为。运行 `/terminal-setup` 为 iTerm2 和 VS Code 终端安装 Shift+Enter 绑定。

<h2 id="command-history">命令历史</h2>

> Claude Code 为当前会话维护命令历史:
```
* 历史记录按工作目录存储
* 使用 `/clear` 命令清除
* 使用 Up/Down 箭头导航 (参见上面的键盘快捷键)
* **Ctrl+R**: 通过历史反向搜索 (如果终端支持)
* **注意**: 历史扩展 (`!`) 默认禁用
```

---

<h1 id="advanced-features">高级功能</h1>

<h2 id="thinking-keywords">思考关键词</h2>

> [!Note]
> **通过在提示中添加这些关键词之一，为 Claude 提供额外的预答案规划时间。**
> **顺序 (最低 → 最高) 令牌消耗**
> <table><tr><td>
>
> > **<kbd>think</kbd> -------------> 最低**
>
> > **<kbd>think hard</kbd>**
>
> > **<kbd>think harder</kbd>**
>
> > **<kbd>ultrathink</kbd> --------> 最高**
>
> </td></tr></table>

<h3 id="this-makes-claude-spend-more-time">这使 Claude 花费更多时间:</h3>

1. **规划解决方案**
2. #### 分解步骤
3. #### 权衡替代方案/权衡
4. #### 检查约束和边缘情况
> > #### 更高级别通常会增加 **延迟** 和 **令牌使用量**，选择有效的最小级别。


<h5 id="thinking-examples">示例</h5>

```md
# 小幅提升
claude -p "Think. Outline a plan to refactor the auth module."

# 中等提升
claude -p "Think harder. Draft a migration plan from REST to gRPC."

# 最大提升
claude -p "Ultrathink. Propose a step-by-step strategy to fix flaky payment tests and add guardrails."
```

<h2 id="sub-agents">子代理</h2>

> 子代理是专用助手，具有自己的**提示、工具和隔离的上下文窗口**。将此视为您为每个仓库**组合**的"专家混合"。

**何时使用它们**
> - 您需要高信号响应 (计划、审查、差异) 而无需偏离主题。
> - 您希望版本控制的提示和工具策略与代码库一起。
> - 您在 PR 驱动的团队中工作，希望按角色进行范围编辑。

<h3 id="each-sub-agent-has-its-own-context">每个子代理都有自己的上下文</h3>

**为您的阵容设计规则**
> - 为每个代理定义**一个明确的职责**。
> - 保持该角色所需的**最小**工具集。
> - 对于分析/审查任务，优先使用**只读**代理。
> - 尽可能少地给予代理编辑权限。

<img width="700" height="160" alt="image" src="https://github.com/user-attachments/assets/42767417-20aa-4bd4-aaf2-cfa0e515b54b" />

*说明: 终端中的代理选择 UI。*

<h3 id="configure-agents">配置代理</h3>

> 将代理**保留在项目中**，以便它们与仓库进行版本控制并通过 PR 演进。

<h3 id="agents-quick-start">快速开始</h3>

> 更新 CLI 并打开代理面板
```bash
claude update
/agents
```

<h3 id="create-your-core-agents">创建您的核心代理</h3>

> - **planner** (只读): 将功能/问题转换为小的、可测试的任务；输出任务列表或 plan.md。
> - **codegen** (具有编辑能力): 实现任务；限制为 `src/` + `tests/`。
> - **tester** (只读或仅补丁): 编写*一个*失败测试或最小重现。
> - **reviewer** (只读): 留下结构化审查评论；从不编辑。
> - **docs** (具有编辑能力): 仅更新 `README.md`/`docs/`。

***策略** 提示: 对于具有编辑能力的代理，优先使用**补丁输出**，以便更改通过您的正常 Git 工作流进行。*

<img width="700" height="173" alt="image" src="https://github.com/user-attachments/assets/84bc80de-35b8-4ef7-9b27-f74f7d4a51f9" />

*说明: 仅选择代理真正需要的工具 (例如，咨询 vs 编辑访问)。*

<h3 id="example-prompts">示例提示</h3>

> 保持提示简短、可测试且特定于仓库。将它们签入 `agents/`:

<img width="700" height="217" alt="image" src="https://github.com/user-attachments/assets/b4f92591-ff5c-4775-aec2-051f145b9616" />

*说明: **test‑coverage‑analyzer** 代理的示例提示。*

**tester.prompt.md (示例)**
```
角色: 为我描述的特定场景编写单个、专注的失败测试。
范围: 仅在 tests/ 下创建/修改测试。不要更改 src/。
输出: 简短理由 + 统一差异或补丁。
如果场景不清楚，请准确询问一个澄清问题。
```

<h3 id="expected-output">期望输出</h3>

> 您的测试代理应该产生一个小的差异或补丁加上简短的理由:

<img width="700" height="273" alt="image" src="https://github.com/user-attachments/assets/839151ce-02c9-4283-a53b-9dd105802ada" />

*说明: 来自 **test‑coverage‑analyzer** 代理的示例响应。*

<h3 id="why-this-shift-matters">为什么这种转变很重要</h3>

**操作优势**
> - **减少上下文切换:** 您保持在一种心理模式下；代理做其余工作。
> - **更清洁的 PR:** 狭窄的提示 + 有限的工具 → 更小、可审查的差异。
> - **更少的回归:** 测试者/审查者代理在合并前捕获差距。
> - **可重复性:** 提示 + 策略存在于仓库中并与分支一起移动。

**安全和治理**
> - 按路径限制写访问 (例如，`src/`、`tests/`、`docs/`)。
> - 对于高风险区域，优先进行只读分析。
> - 记录/提交助手输出作为补丁以供审计。

<h3 id="a-mindset-shift">思维转变</h3>

**要做**
> - 将代理视为具有职位描述的队友。
> - 从只读开始；*最后*授予写访问权限。
> - 在版本控制中保留提示，并通过 PR 迭代。

**不要**
> - 要求一个代理在单轮中规划、编码和测试。
> - 给予全面的写权限。
> - 当您要求一个测试时接受多文件差异。

<h2 id="mcp-integration">MCP 集成</h2>

<h3 id="understanding-mcp-model-context-protocol">理解 MCP (模型上下文协议)</h3>

#### 什么是 MCP?
> MCP 通过连接到外部服务、数据库、API 和工具来扩展 Claude 的能力 (文件系统、Puppeteer、GitHub、Context7 等...)


###### **MCP 架构:**
```
Claude Code ←→ MCP 协议 ←→ MCP 服务器 ←→ 外部服务
```

<h3 id="mcp-setup--configuration">MCP 设置与配置</h3>

> MCP 服务器可以通过多种方式连接:
> - **Stdio**: 本地命令行程序
> - **HTTP**: REST API 端点
> - **SSE**: 服务器发送事件流

```bash
# MCP 管理
claude mcp                    # 启动 MCP 配置向导
claude mcp list               # 查看已配置的服务器
claude mcp add <name> <cmd>   # 添加 stdio 服务器
claude mcp remove <name>      # 删除服务器
```

<h3 id="popular-mcp-servers">流行的 MCP 服务器</h3>

| 服务器              | 用途                         | 安装                                    |
| :------------------ | :--------------------------- | :-------------------------------------- |
| **filesystem**      | 文件系统操作                 | 内置                                    |
| **github**          | GitHub API 集成              | `claude mcp add github github-mcp`     |
| **memory**          | 持久内存和笔记               | `claude mcp add memory memory-server`  |
| **puppeteer**       | 浏览器自动化                 | `claude mcp add puppeteer puppeteer`   |
| **context7**        | 文档和库搜索                 | 通过 Upstash                           |

<h2 id="hooks-system">钩子系统</h2>

> 钩子允许您在 Claude Code 事件发生时自动运行自定义脚本。

<h3 id="hooks-configuration">配置</h3>

钩子在 `settings.json` 中配置:

```json
{
  "hooks": {
    "toolCallBlocked": {
      "commands": [
        {
          "type": "bash",
          "command": "echo 'Tool blocked: $TOOL_NAME'"
        }
      ]
    },
    "toolUse": {
      "commands": [
        {
          "type": "bash",
          "command": "log-tool-usage.sh",
          "runInBackground": true
        }
      ]
    }
  }
}
```

<h3 id="hook-events">钩子事件</h3>

支持的钩子事件:

| 事件                      | 何时触发                     | 可用变量                                  |
| :------------------------ | :--------------------------- | :---------------------------------------- |
| `toolUse`                 | 工具被使用时                 | `$TOOL_NAME`, `$TOOL_ARGS`              |
| `toolCallBlocked`         | 工具调用被阻止时             | `$TOOL_NAME`, `$BLOCK_REASON`           |
| `conversationStart`       | 新对话开始时                 | `$SESSION_ID`                            |
| `conversationEnd`         | 对话结束时                   | `$SESSION_ID`, `$DURATION`              |
| `userPromptSubmitHook`    | 用户提交提示前               | `$USER_PROMPT`                           |

<h3 id="hook-input">钩子输入</h3>

钩子通过以下方式接收输入:
- **环境变量**: 事件特定数据
- **Stdin**: JSON 格式的详细事件数据
- **命令行参数**: 可通过钩子配置传递

<h3 id="hook-output">钩子输出</h3>

钩子可以影响 Claude Code 的行为:
- **阻止操作**: 通过非零退出代码
- **修改输入**: 通过 stdout 返回修改的数据
- **记录/通知**: 用于审计和监控

<h3 id="working-with-mcp-tools">使用 MCP 工具</h3>

Claude Code 自动发现和使用 MCP 工具:

```bash
# 查看可用的 MCP 工具
claude mcp list

# 使用特定 MCP 服务器的工具
claude --mcp-config ./servers.json

# 调试 MCP 连接
claude --debug
```

<h3 id="hooks-examples">示例</h3>

**记录所有工具使用:**

```bash
#!/bin/bash
# log-tool-usage.sh
echo "$(date): Tool $TOOL_NAME used with args: $TOOL_ARGS" >> ~/.claude/tool-usage.log
```

<h3 id="security-considerations">安全考虑</h3>

> - 钩子以您的用户权限运行
> - 验证钩子脚本和权限
> - 使用 `runInBackground` 用于非阻塞操作
> - 避免在钩子中暴露敏感数据

<h3 id="hook-execution-details">钩子执行详细信息</h3>

- 钩子按配置顺序执行
- 失败的钩子 (非零退出) 可以阻止操作
- 后台钩子不会阻止 Claude Code

<h3 id="hooks-debugging">调试</h3>

使用 `--debug` 标志查看钩子执行:

```bash
claude --debug
```

---

<h1 id="security--permissions">安全与权限</h1>

> Claude Code 使用分层权限系统来控制工具访问。

**权限模式:**

| 模式                  | 描述                         | 何时使用                     |
| :-------------------- | :--------------------------- | :--------------------------- |
| `default`             | 为每个工具使用提示           | 正常开发                     |
| `acceptEdits`         | 自动批准编辑操作             | 可信环境                     |
| `bypassPermissions`   | 跳过所有权限检查             | 自动化/沙盒                  |
| `plan`                | 只允许规划，不允许执行       | 代码审查                     |

<h3 id="dangerous-mode">危险模式</h3>

> **警告**: 仅在可信环境中使用

```bash
claude --dangerously-skip-permissions
```

<h2 id="security-best-practices-main">安全最佳实践</h2>

<h3 id="start-restrictive">从限制性开始</h3>

> - 首先使用默认权限模式
> - 逐步授予所需的工具访问权限
> - 定期审查权限配置

<h3 id="protect-sensitive-data">保护敏感数据</h3>

> - 使用 `.gitignore` 排除敏感文件
> - 通过环境变量传递 API 密钥
> - 避免在提示中包含密钥

---

<h1 id="automation--integration">自动化与集成</h1>

<h2 id="automation--scripting-with-claude-code">使用 Claude Code 进行自动化和脚本</h2>

> Claude Code 提供强大的 CLI 用于自动化常见开发任务。

**基本自动化模式:**

```bash
# 非交互式脚本
claude -p "查看代码质量问题" --output-format json > report.json

# 管道集成
cat logs.txt | claude -p "总结错误" > summary.md

# 条件执行
if claude -p "检查测试是否通过" | grep -q "PASS"; then
  git push origin main
fi
```

<h2 id="auto-pr-review-inline-comments">自动 PR 审查 (内联评论)</h2>

GitHub Actions 工作流示例:

```yaml
name: Claude Code Review
on:
  pull_request:
    types: [opened, synchronize]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
      with:
        fetch-depth: 0

    - name: Install Claude Code
      run: npm install -g @anthropic-ai/claude-code

    - name: Review Changes
      env:
        ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      run: |
        claude -p "审查此 PR 的代码更改并提供内联评论" \
          --output-format json \
          --allowed-tools "Read,Grep,Bash(git:*)" > review.json

        # 处理审查结果并创建 PR 评论
        gh pr comment ${{ github.event.number }} --body-file review.json
```

<h2 id="security-review-on-every-pr">每个 PR 的安全审查</h2>

```yaml
name: Security Review
on:
  pull_request:
    types: [opened, synchronize]

jobs:
  security-review:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3

    - name: Security Scan
      env:
        ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
      run: |
        claude -p "扫描安全漏洞和敏感数据泄露" \
          --permission-mode plan \
          --output-format json > security-report.json

        # 如果发现关键问题则失败
        if jq -e '.criticalIssues | length > 0' security-report.json; then
          echo "发现关键安全问题"
          exit 1
        fi
```

<h2 id="issue-triage-suggest-labels--severity">问题分类 (建议标签和严重性)</h2>

```bash
#!/bin/bash
# issue-triage.sh - 自动问题分类脚本

ISSUE_BODY="$1"
ISSUE_TITLE="$2"

# 使用 Claude 分析问题
ANALYSIS=$(claude -p "
分析此 GitHub 问题并建议:
1. 适当的标签 (bug, feature, enhancement, documentation)
2. 优先级 (low, medium, high, critical)
3. 估计工作量 (1-5 点)

标题: $ISSUE_TITLE
描述: $ISSUE_BODY
" --output-format json)

# 提取建议
LABELS=$(echo "$ANALYSIS" | jq -r '.labels[]')
PRIORITY=$(echo "$ANALYSIS" | jq -r '.priority')
EFFORT=$(echo "$ANALYSIS" | jq -r '.effort')

# 应用标签 (需要 GitHub CLI)
for label in $LABELS; do
  gh issue edit "$ISSUE_NUMBER" --add-label "$label"
done

gh issue edit "$ISSUE_NUMBER" --add-label "priority:$PRIORITY"
gh issue edit "$ISSUE_NUMBER" --add-label "effort:$EFFORT"
```

---

<h1 id="help--troubleshooting">帮助与故障排除</h1>

> 遇到问题? 这里是最常见问题的解决方案。

**首先尝试这些快速修复:**

```bash
# 检查安装和连接
claude doctor

# 更新到最新版本
claude update

# 重置配置
claude config reset

# 清除缓存
rm -rf ~/.claude/cache
```

<h2 id="debug-quick-commands">调试快速命令</h2>

```bash
# 诊断系统
claude doctor                    # 健康检查
claude --version                 # 版本信息
claude config list               # 当前配置
claude mcp list                  # MCP 服务器状态

# 详细调试
claude --debug                   # 详细日志
claude --verbose                 # 扩展输出
claude /status                   # 账户状态

# 网络诊断
curl -I https://api.anthropic.com # API 连接测试
echo $ANTHROPIC_API_KEY | cut -c1-8 # 检查 API 密钥
```

<h2 id="linuxpath">路径临时修复</h2>

如果 `claude` 未在 PATH 中找到:

```bash
# 查找 Claude 安装位置
which claude
npm list -g @anthropic-ai/claude-code

# 临时添加到 PATH
export PATH="$PATH:$(npm bin -g)"

# 永久修复 (添加到 ~/.bashrc 或 ~/.zshrc)
echo 'export PATH="$PATH:$(npm bin -g)"' >> ~/.bashrc
source ~/.bashrc
```

<h2 id="windowspath">Windows 路径永久修复</h2>

**PowerShell (以管理员身份运行):**

```powershell
# 查找 npm 全局路径
npm prefix -g

# 添加到系统 PATH
$oldPath = [Environment]::GetEnvironmentVariable("Path", "Machine")
$newPath = "$oldPath;C:\Users\%USERNAME%\AppData\Roaming\npm"
[Environment]::SetEnvironmentVariable("Path", $newPath, "Machine")

# 重启终端以应用更改
```

**命令提示符:**

```cmd
# 查看当前 PATH
echo %PATH%

# 永久添加 npm 全局目录
setx PATH "%PATH%;C:\Users\%USERNAME%\AppData\Roaming\npm"
```

<h3 id="installation--nodejs-issues">安装 / Node.js 问题</h3>

**Node.js 版本问题:**

```bash
# 检查 Node.js 版本 (需要 18+)
node --version

# 更新 Node.js (使用 nvm)
nvm install node
nvm use node

# 或使用包管理器
sudo apt update && sudo apt install nodejs npm  # Ubuntu/Debian
brew install node                                # macOS
```

**权限问题:**

```bash
# 修复 npm 权限 (Linux/macOS)
sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}

# 或配置不同的 npm 前缀
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.profile
```

<h3 id="authentication-issues">认证问题</h3>

**API 密钥问题:**

```bash
# 验证 API 密钥格式
echo $ANTHROPIC_API_KEY | grep -E "^sk-[a-zA-Z0-9-]+"

# 测试 API 连接
curl -H "Authorization: Bearer $ANTHROPIC_API_KEY" \
     -H "Content-Type: application/json" \
     https://api.anthropic.com/v1/models

# 重新登录
claude logout
claude login
```

**网络/代理问题:**

```bash
# 配置代理 (如果需要)
export HTTP_PROXY=http://proxy.company.com:8080
export HTTPS_PROXY=https://proxy.company.com:8080

# 跳过 SSL 验证 (仅用于调试)
export NODE_TLS_REJECT_UNAUTHORIZED=0
```

<h3 id="permission--allowed-tools-issues">权限 / 允许工具问题</h3>

**工具被阻止:**

```bash
# 检查权限设置
claude /permissions

# 重置权限
claude config set defaultMode "default"

# 允许特定工具
claude --allowed-tools "Bash,Edit,Read"

# 跳过权限 (谨慎使用)
claude --dangerously-skip-permissions
```

**文件访问问题:**

```bash
# 检查文件权限
ls -la /path/to/file

# 添加工作目录
claude --add-dir /additional/directory

# 检查当前工作目录设置
claude config get workingDirectories
```

<h3 id="mcp-model-context-protocol-issues">MCP (模型上下文协议) 问题</h3>

**MCP 服务器不工作:**

```bash
# 调试 MCP 连接
claude --debug mcp list

# 重置 MCP 配置
claude mcp reset-project-choices

# 测试特定服务器
claude mcp get <server-name>

# 删除有问题的服务器
claude mcp remove <server-name>
```

<h2 id="full-clean-reinstall-windows--powershell">完全清洁重新安装 (Windows / PowerShell)</h2>

```powershell
# 1. 卸载当前安装
npm uninstall -g @anthropic-ai/claude-code

# 2. 清除缓存和配置
Remove-Item -Recurse -Force $env:APPDATA\claude-code -ErrorAction SilentlyContinue
Remove-Item -Recurse -Force $env:LOCALAPPDATA\claude-code -ErrorAction SilentlyContinue
Remove-Item -Recurse -Force $env:USERPROFILE\.claude -ErrorAction SilentlyContinue

# 3. 清除 npm 缓存
npm cache clean --force

# 4. 重新安装
npm install -g @anthropic-ai/claude-code

# 5. 验证安装
claude --version
claude doctor
```

<h2 id="one-shot-health-check-copypaste">一键健康检查 (复制/粘贴)</h2>

```bash
#!/bin/bash
# Claude Code 健康检查脚本

echo "=== Claude Code 健康检查 ==="
echo

# 基本系统信息
echo "系统信息:"
echo "OS: $(uname -s)"
echo "Node.js: $(node --version 2>/dev/null || echo 'Not found')"
echo "npm: $(npm --version 2>/dev/null || echo 'Not found')"
echo

# Claude Code 状态
echo "Claude Code 状态:"
echo "版本: $(claude --version 2>/dev/null || echo 'Not installed')"
echo "位置: $(which claude 2>/dev/null || echo 'Not in PATH')"
echo

# API 密钥
echo "API 密钥:"
if [ -n "$ANTHROPIC_API_KEY" ]; then
    echo "设置: ${ANTHROPIC_API_KEY:0:8}***"
else
    echo "未设置: ANTHROPIC_API_KEY 环境变量"
fi
echo

# 网络连接
echo "网络连接:"
if curl -s --max-time 5 https://api.anthropic.com > /dev/null; then
    echo "API 连接: OK"
else
    echo "API 连接: FAILED"
fi
echo

# 配置
echo "配置:"
claude config list 2>/dev/null || echo "无法读取配置"
echo

# MCP 服务器
echo "MCP 服务器:"
claude mcp list 2>/dev/null || echo "无法列出 MCP 服务器"

echo "=== 健康检查完成 ==="
```

<h2 id="appendix-useful-paths">附录: 有用的路径</h2>

**配置位置:**

| 平台    | 路径                                           |
| :------ | :--------------------------------------------- |
| macOS   | `~/.claude/`                                   |
| Linux   | `~/.claude/`                                   |
| Windows | `%USERPROFILE%\.claude\`                      |

**日志位置:**

| 平台    | 路径                                           |
| :------ | :--------------------------------------------- |
| macOS   | `~/Library/Logs/claude-code/`                  |
| Linux   | `~/.local/share/claude-code/logs/`             |
| Windows | `%LOCALAPPDATA%\claude-code\logs\`             |

<h2 id="effective-prompting">有效提示</h2>

**最佳实践:**

> - **明确具体**: "重构 auth.js 中的登录函数" 而不是 "修复代码"
> - **提供上下文**: 包含错误消息、预期行为、尝试的解决方案
> - **设置约束**: "仅修改测试文件" 或 "保持向后兼容"
> - **使用例子**: 显示输入/输出示例或所需格式

**有效提示模式:**

```md
# 问题描述模板
**问题**: [简要描述问题]
**期望结果**: [您想要发生什么]
**当前行为**: [实际发生什么]
**错误消息**: [如果有的话，包含完整错误]
**尝试的解决方案**: [您已经尝试的内容]

# 功能请求模板
**功能**: [您想要什么功能]
**用例**: [为什么需要它]
**验收标准**: [如何知道它是否有效]
**约束**: [任何限制或要求]
```

<h2 id="security-best-practices-main">安全最佳实践</h2>

**API 密钥安全:**

> - **永远不要**将 API 密钥提交到版本控制
> - 使用环境变量或安全密钥管理器
> - 定期轮换 API 密钥
> - 监控 API 使用情况是否有异常

**权限管理:**

> - 从最限制性权限开始
> - 仅在需要时授予编辑权限
> - 在生产环境中定期审查权限
> - 为自动化使用专用服务账户

**代码安全:**

> - 审查 Claude 的代码更改然后再提交
> - 在可信环境中使用 `--dangerously-skip-permissions`
> - 监控敏感文件的意外更改
> - 使用 `.gitignore` 保护敏感数据

**网络安全:**

```bash
# 验证 HTTPS 连接
curl -I https://api.anthropic.com

# 使用公司代理
export HTTPS_PROXY=https://proxy.company.com:8080

# 检查 TLS 版本
openssl s_client -connect api.anthropic.com:443 -tls1_2
```

**审计和监控:**

```bash
# 启用详细日志记录
export CLAUDE_CODE_VERBOSE=1

# 监控 API 使用情况
claude /cost

# 检查最近的活动
claude /status

# 审查配置更改
git log --oneline .claude/
```

<h2 id="performance-tips">性能提示</h2>

**优化响应时间:**

> - 使用 **thinking keywords** 处理复杂任务: `think`, `think hard`, `think harder`, `ultrathink`
> - 为大型项目配置 **Sub Agents** 以减少上下文切换
> - 使用 **MCP servers** 进行高效的外部数据访问
> - 限制大文件的并发工具使用

**令牌管理:**

```bash
# 监控令牌使用情况
claude /cost

# 使用更小的模型进行简单任务
claude --model claude-3-haiku-20240307

# 压缩长对话
claude /compact

# 限制输出长度
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=2048
```

**内存优化:**

> - 定期使用 `/clear` 清除对话历史
> - 对于长期项目使用项目特定的 CLAUDE.md
> - 避免在提示中包含大文件
> - 使用 `/compact` 而不是 `/clear` 保留重要上下文

**网络优化:**

```bash
# 减少非必要流量
export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1

# 禁用遥测 (如果需要)
export DISABLE_TELEMETRY=1

# 使用本地缓存
export CLAUDE_CODE_CACHE_ENABLED=1
```

**工作流优化:**

> - 为常见任务设置 **aliases**
> - 使用 **hooks** 实现自动化工作流
> - 配置 **status line** 用于快速信息
> - 批量处理相似任务

<h2 id="monitoring--alerting">监控与警报</h2>

**成本监控:**

```bash
# 检查令牌使用情况
claude /cost

# 设置成本警告阈值
claude config set costWarningThreshold 100

# 监控 API 使用情况趋势
claude --output-format json /cost | jq '.dailyUsage'
```

**性能监控:**

```bash
# 启用性能指标
export CLAUDE_CODE_PERFORMANCE_METRICS=1

# 监控响应时间
time claude -p "简单查询"

# 检查系统健康状况
claude doctor --json
```

**错误监控:**

```bash
# 启用错误报告
export DISABLE_ERROR_REPORTING=0

# 查看本地错误日志
tail -f ~/.claude/logs/error.log

# 监控失败的工具调用
grep "tool_error" ~/.claude/logs/claude.log
```

**自定义警报:**

```bash
#!/bin/bash
# claude-monitor.sh - 自定义监控脚本

# 检查 API 连接
if ! claude /status >/dev/null 2>&1; then
    echo "警报: Claude Code API 连接失败" | mail admin@company.com
fi

# 检查成本阈值
COST=$(claude /cost --json | jq '.currentBill')
if (( $(echo "$COST > 100" | bc -l) )); then
    echo "警报: Claude Code 成本超过阈值: $COST" | mail admin@company.com
fi

# 检查磁盘空间
CACHE_SIZE=$(du -s ~/.claude/cache | cut -f1)
if [ "$CACHE_SIZE" -gt 1000000 ]; then  # 1GB
    echo "警报: Claude Code 缓存过大: ${CACHE_SIZE}KB" | mail admin@company.com
fi
```

<h2 id="collaboration-best-practices">协作最佳实践</h2>

<h3 id="team-workflows">团队工作流</h3>

**共享配置管理:**

> - 在项目根目录维护 `CLAUDE.md`
> - 使用版本控制的 `.mcp.json` 进行 MCP 服务器配置
> - 为团队标准化建立企业级 CLAUDE.md
> - 通过 PR 审查配置更改

**协作代码审查:**

```bash
# 团队审查工作流
# 1. 开发者使用 Claude 进行初始实现
claude "实现用户认证功能"

# 2. 请求 Claude 代码审查
claude /review

# 3. 团队成员审查 Claude 的建议
git diff HEAD~1

# 4. 整合反馈并迭代
claude "根据审查评论解决问题"
```

**共享子代理:**

> - 将代理配置保留在 `agents/` 目录中
> - 为不同角色创建专门的代理 (tester, reviewer, docs)
> - 通过团队输入迭代代理提示
> - 在 README 中记录代理用法

**知识共享模式:**

```md
# 团队 CLAUDE.md 模板
## 项目特定指导
- 架构模式: [描述主要模式]
- 编码标准: [链接到风格指南]
- 测试策略: [测试方法]
- 部署流程: [CI/CD 详细信息]

## 常见任务
- 添加新功能: [步骤模板]
- 错误修复流程: [调试指南]
- 性能优化: [分析工具]
- 文档更新: [文档标准]

## 团队约定
- 分支命名: feature/*, bugfix/*, hotfix/*
- 提交消息: [约定式提交]
- PR 模板: [必需的检查项]
- 代码审查: [审查者指南]
```

<h3 id="knowledge-sharing">知识分享</h3>

**最佳实践文档:**

> - 维护 Claude 提示和模式的团队知识库
> - 分享有效的 CLAUDE.md 配置
> - 记录常见故障排除解决方案
> - 创建特定于项目的使用指南

**培训和入职:**

> - 为新团队成员创建 Claude Code 入职指南
> - 分享高效提示技巧的示例
> - 记录团队特定的工作流和约定
> - 提供故障排除和调试的培训

**度量和改进:**

```bash
# 跟踪团队使用情况指标
claude /cost --team-view

# 分析常见模式
grep -r "claude" .git/logs/ | awk '{print $3}' | sort | uniq -c

# 收集改进反馈
claude /feedback --team-survey
```

<h2 id="common-pitfalls-to-avoid">常见陷阱避免</h2>

<h3 id="security-pitfalls">安全</h3>

**❌ 避免这些做法:**

> - 在代码或提示中硬编码 API 密钥
> - 对不可信代码使用 `--dangerously-skip-permissions`
> - 忽略工具权限警告
> - 在公共仓库中提交敏感的 CLAUDE.md

**✅ 推荐做法:**

> - 使用环境变量进行密钥管理
> - 从限制性权限开始
> - 定期审计工具访问日志
> - 使用 `.gitignore` 保护敏感配置

<h3 id="performance-pitfalls">性能</h3>

**❌ 避免这些做法:**

> - 在提示中包含超大文件
> - 为简单任务过度使用 "ultrathink"
> - 忽略令牌使用警告
> - 在单个会话中运行过多并发工具

**✅ 推荐做法:**

> - 针对任务复杂性使用适当的思考级别
> - 监控并优化令牌使用
> - 将大任务分解为较小的块
> - 使用 `/compact` 管理长对话

<h3 id="workflow-pitfalls">工作流</h3>

**❌ 避免这些做法:**

> - 在没有审查的情况下盲目接受所有 Claude 建议
> - 对所有任务使用相同的通用提示
> - 忽略错误消息和警告
> - 跳过备份重要代码

**✅ 推荐做法:**

> - 在提交前始终审查代码更改
> - 制作具体的、与上下文相关的提示
> - 读取并响应 Claude 的警告
> - 维护适当的版本控制实践

---

<h1 id="third-party-integrations">第三方集成</h1>

<h2 id="deepseek-integration">DeepSeek 集成</h2>

> Claude Code 支持通过兼容的 API 端点与 DeepSeek 等第三方模型集成。

**设置 DeepSeek:**

```bash
# 配置 DeepSeek API 端点
export ANTHROPIC_API_BASE="https://api.deepseek.com/v1"
export ANTHROPIC_API_KEY="your-deepseek-api-key"

# 使用特定的 DeepSeek 模型
claude --model deepseek-chat

# 验证连接
claude -p "测试 DeepSeek 连接" --debug
```

**支持的第三方提供商:**

| 提供商      | API 兼容性 | 设置说明                          |
| :---------- | :--------- | :-------------------------------- |
| DeepSeek    | ✅         | 设置 `ANTHROPIC_API_BASE`        |
| OpenRouter  | ✅         | 使用 OpenRouter API 端点          |
| 本地模型    | ⚠️         | 需要兼容的 API 包装器            |

**注意事项:**

> - 第三方集成可能不支持所有 Claude Code 功能
> - 验证 API 兼容性和模型能力
> - 某些工具可能需要调整第三方模型
> - 查阅具体提供商的文档了解限制

---

<div align="center">

**✨ 感谢使用 Claude Code! ✨**

[开始使用](https://claude.ai/code) • [社区指南](#content) • [故障排除](#help--troubleshooting)

*有问题或建议? 请访问我们的 [GitHub Issues](https://github.com/zebbern/claude-code-guide/issues)*

</div>
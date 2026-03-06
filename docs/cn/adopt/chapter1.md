# 第一章 十分钟上手 OpenClaw

这一章会带你完成 OpenClaw 的安装，从下载到打开控制面板，整个过程不超过 10 分钟。我们会覆盖 Windows、macOS 和 Linux 三个平台的安装方法，以及首次配置的关键步骤。

## 1. 系统要求

在开始之前，确保你的系统满足以下要求：

- **操作系统**：Windows 10/11、macOS 10.15+、或主流 Linux 发行版（Ubuntu 20.04+、Debian 11+、Fedora 35+）
- **Python**：3.10 或更高版本（macOS 和 Linux 通常预装，Windows 需要手动安装）
- **网络**：稳定的互联网连接（用于下载依赖和调用 LLM API）
- **磁盘空间**：至少 500MB 可用空间

如果你不确定 Python 版本，可以在终端或命令提示符中运行 `python --version` 或 `python3 --version` 来检查。

## 2. Windows 安装

Windows 用户需要先确保 Python 已正确安装。如果还没有安装 Python，访问 [python.org](https://www.python.org/downloads/) 下载最新版本，安装时记得勾选"Add Python to PATH"选项。

打开 PowerShell（按 Win+X，选择"Windows PowerShell"或"终端"），然后执行：

```powershell
pip install openclaw
```

安装完成后，运行初始化命令：

```powershell
openclaw init
```

这会启动配置向导，引导你完成 API 密钥设置和基础配置。

## 3. macOS 安装

macOS 通常预装了 Python，但版本可能较旧。建议使用 Homebrew 安装最新版本。如果还没有 Homebrew，先访问 [brew.sh](https://brew.sh) 安装。

在终端中执行：

```bash
brew install python3
pip3 install openclaw
openclaw init
```

如果遇到权限问题，可能需要在命令前加 `sudo`，但通常不推荐这样做。更好的方式是使用虚拟环境或用户级安装。

## 4. Linux 安装

大多数 Linux 发行版都预装了 Python 3。在终端中执行：

```bash
pip3 install openclaw --user
openclaw init
```

如果 `pip3` 命令不存在，先安装 pip：

```bash
# Ubuntu/Debian
sudo apt update && sudo apt install python3-pip

# Fedora
sudo dnf install python3-pip

# Arch Linux
sudo pacman -S python-pip
```

安装完成后运行 `openclaw init` 开始配置。

## 5. 首次配置向导

运行 `openclaw init` 后，会看到交互式配置向导。它会依次询问几个关键问题：

**选择 LLM 提供商**：支持 Claude（Anthropic）、GPT（OpenAI）、或本地模型（Ollama）。如果你有 Claude API 密钥，推荐选择 Claude，因为 OpenClaw 最初就是为 Claude 优化的。

**输入 API 密钥**：根据你选择的提供商，输入对应的 API 密钥。如果暂时没有，可以先跳过，后续在配置文件中手动添加。获取 Claude API 密钥可以访问 [console.anthropic.com](https://console.anthropic.com)，OpenAI 的在 [platform.openai.com](https://platform.openai.com)。

**设置工作目录**：OpenClaw 会询问你希望它在哪个目录下工作。默认是当前用户的主目录，你也可以指定项目目录。这个目录会用来存储对话历史、记忆文件和技能配置。

**启用 Web 控制面板**：建议选择"是"，这样可以通过浏览器访问可视化界面。默认端口是 8080，如果端口被占用会自动选择其他端口。

**配置工具权限（重要）**：向导会询问 Tools Profile 设置。这是 2026.3.2 版本后的新特性，用于控制 OpenClaw 的操作权限：

- `messaging` - 只能发消息和管理会话（**默认值，但会导致无法执行命令**）
- `default` - 默认工具集，基础文件读取
- `coding` - 编程相关工具
- `full` - 完整工具集，包含命令执行、文件操作
- `all` - 所有工具全开

> **重要提示**
>
> 如果你发现 OpenClaw 只会聊天不干活（比如让它列出文件却只给建议），很可能是 profile 设置成了 `messaging`。
>
> **推荐配置**：选择 `full` 以获得完整功能。
>
> **安全警告**：`full` 和 `all` 模式下，OpenClaw 可以读取、创建、修改甚至删除文件，也能执行任意系统命令。请确保：
> - 在可信环境下使用
> - 不要在生产服务器上随意授权
> - 定期检查操作日志
> - 重要数据做好备份

配置完成后，向导会自动启动 OpenClaw 服务。

## 6. 打开控制面板

配置向导完成后，终端会显示类似这样的信息：

```
✓ OpenClaw is running
✓ Web dashboard: http://localhost:8080
✓ Press Ctrl+C to stop
```

在浏览器中打开 `http://localhost:8080`，你会看到 OpenClaw 的 Web 控制面板。界面分为几个主要区域：左侧是对话历史列表，中间是聊天窗口，右侧是系统状态和快捷操作。

在聊天窗口输入"你好"或"帮我列出当前目录的文件"，OpenClaw 会立即响应。如果它能正确执行命令并返回结果，说明安装成功。

## 7. 切换和配置模型

OpenClaw 支持多种 LLM 模型，你可以根据任务类型和成本考虑选择不同的模型。

### 7.1 查看和切换模型

运行配置命令：

```bash
openclaw configure
```

会进入交互式配置界面，你可以：
- 切换 LLM 提供商（Claude、GPT、Ollama）
- 修改 API 密钥
- 调整模型参数（温度、最大 token 等）

### 7.2 推荐配置：使用 Coding Plan 模式

**重要提示**：OpenClaw 在执行复杂任务时会消耗大量 token。如果对话持续很久，上下文会变得很长，API 费用会快速增加。为了控制成本和提高效率，强烈推荐启用 **Coding Plan** 模式。

在配置文件 `~/.openclaw/config.yaml` 中添加：

```yaml
llm:
  provider: claude
  model: claude-sonnet-4-6
  coding_plan: true  # 启用编码计划模式
  max_context_tokens: 50000  # 限制上下文长度
```

Coding Plan 模式的优势：
- **分步执行**：将复杂任务拆解成多个小步骤，每步独立执行
- **上下文隔离**：避免上下文无限增长导致的高额费用
- **更清晰的执行流程**：你可以看到每一步的计划和结果

没有启用 Coding Plan 时，一个复杂任务可能消耗 10 万+ token。启用后，同样的任务可能只需要 2-3 万 token，成本降低 70% 以上。

## 8. 常用命令

除了 Web 控制面板，你也可以直接在终端使用 OpenClaw：

```bash
# 启动服务（带 Web 面板）
openclaw start

# 命令行模式（不启动 Web 面板）
openclaw chat

# 查看配置
openclaw config

# 安装技能
openclaw skill install <skill-name>

# 停止服务
openclaw stop
```

命令行模式适合快速执行单个任务，Web 面板则更适合需要查看历史记录或管理多个对话的场景。

## 9. 常见问题

**Q: OpenClaw 只会聊天不干活，让它执行命令却只给建议？**

A: 这是 2026.3.2 版本后最常见的问题，原因是 Tools Profile 被设置成了 `messaging`。有两种修复方法：

方法一：命令行修复（推荐）

```bash
# 查看当前 profile
openclaw config get tools

# 如果不是 full，切换成 full
openclaw config set tools.profile full

# 重启 gateway
openclaw gateway restart
```

方法二：Web 界面修复

1. 访问 `http://localhost:18789`（本地模式默认端口）
2. 点击左侧"配置"或"Agents"
3. 找到对应的 Agent，点击旁边的"tools"
4. 选择"Full"选项
5. 保存并重启

或者直接编辑配置文件，找到 tools 部分改成：

```json
"tools": {
  "profile": "full"
}
```

**Q: 提示"API key not found"怎么办？**

A: 编辑配置文件 `~/.openclaw/config.yaml`，在对应的提供商下添加 API 密钥。例如：

```yaml
llm:
  provider: claude
  api_key: sk-ant-xxxxx
```

**Q: Web 面板无法访问？**

A: 检查防火墙设置，确保端口 8080 未被占用。可以在配置文件中修改端口号。

**Q: 命令执行失败？**

A: 确认 OpenClaw 有足够的文件系统权限。某些操作可能需要明确授权。

---

**下一步**：[第二章 移动端接入](/cn/adopt/chapter2)


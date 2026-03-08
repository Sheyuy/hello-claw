# Chapter 1: Quick Start with OpenClaw

This chapter walks you through installing OpenClaw, from preparing your environment to running the configuration wizard — all in under 10 minutes.

## 1. System Requirements

- **Operating System**: macOS, Linux, or Windows (WSL2 recommended)
- **Node.js**: Version 22 or higher
- **Memory**: At least 1GB, 4GB recommended
- **Port**: 18789 must be available

<details>
<summary>Windows Users: What is WSL2 and how to install it?</summary>

WSL2 (Windows Subsystem for Linux 2) lets you run a full Linux environment on Windows. Many development tools work better under Linux. **If you prefer not to set this up, you can use PowerShell directly and skip this step.**

**Installation steps** (requires Windows 10 2004 or later, or Windows 11):

1. Open PowerShell as Administrator (right-click Start Menu → "Terminal (Admin)" or "PowerShell (Admin)")
2. Run the following command to install WSL2 and Ubuntu in one step:

```powershell
wsl --install
```

3. **Restart your computer** after installation
4. After restarting, an Ubuntu window will pop up automatically — follow the prompts to set up a username and password
5. Once set up, you have a Linux terminal environment

You can open the WSL2 terminal anytime by searching "Ubuntu" in the Start Menu. All `bash` commands in this tutorial can be run in this terminal.

> **Tip**: If `wsl --install` fails, you may need to first enable "Windows Subsystem for Linux" and "Virtual Machine Platform" in "Control Panel → Programs → Turn Windows features on or off", then restart and try again.

</details>

Check your Node.js version:

```bash
node --version
```

If the version is below 22, you need to upgrade Node.js first.

> **What is a Terminal?**
>
> Many operations in this tutorial require typing commands in a "terminal". A terminal is a text-based interface where you type commands for your computer to execute. Here's how to open one on different operating systems:
>
> - **Windows**: Press `Win + X` and select "Terminal" or "PowerShell"; or search "PowerShell" in the Start Menu
> - **macOS**: Press `Cmd + Space`, search for "Terminal" and open it; or find it in "Applications → Utilities"
> - **Linux**: Press `Ctrl + Alt + T`; or search "Terminal" in your application menu
>
> You'll see a window (dark or light) with a blinking cursor — that's your terminal. All commands in `bash` code blocks throughout this tutorial should be entered here.

## 2. Installing Node.js

### Windows Users

**Option 1: One-click install script (recommended)**

Open PowerShell (as Administrator) and run:

```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

This script automatically installs Node.js and OpenClaw. If you encounter a permission error, first run:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

**Option 2: Manual installation**

1. Download nvm-windows: Visit [github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases) and download `nvm-setup.exe`
2. After installation, reopen PowerShell (as Administrator)
3. Install Node.js 22:

```powershell
nvm install 22
nvm use 22
```

### macOS Users

Install using Homebrew:

```bash
brew install node@22
```

### Linux Users

Install using nvm (recommended):

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc
nvm install 22
nvm use 22
```

## 3. Installing OpenClaw

Install the OpenClaw CLI globally:

```bash
npm install -g openclaw@latest
```

Verify the installation:

```bash
openclaw --version
```

If you see a version number, the installation was successful.

## 4. Running the Configuration Wizard

After installation, run the configuration wizard:

```bash
openclaw onboard --install-daemon
```

This command starts an interactive setup wizard and installs the background daemon.

### 4.1 Choosing a Model Provider

The wizard first asks which AI model you want to use.

**For users in China, SiliconFlow is strongly recommended** — new users get **16 CNY in free credits**, enough to complete all exercises in this tutorial, with no international credit card required.

| Recommended Path | Best For | Cost |
|-----------------|----------|------|
| **SiliconFlow** | Users in China (first choice) | 16 CNY free for new users |
| DeepSeek | Users in China (alternative) | Pay-as-you-go via Alipay |
| Qwen (Tongyi Qianwen) | Users in China (alternative) | Alibaba Cloud ecosystem, enterprise support |
| Kimi / StepFun / MiniMax | Users in China (other options) | Alipay supported |

**For international users**, you can use any OpenAI-compatible API provider, or configure a custom endpoint. Popular options include OpenRouter (access multiple models with one key) and direct provider APIs.

### 4.2 Getting an API Key: SiliconFlow Example

> If you already have an API Key from another provider, skip to section 4.3.

**Step 1: Create an account**

1. Visit [SiliconFlow](https://cloud.siliconflow.cn)
2. Click "Sign Up" in the top right corner — register with your phone number (WeChat login also supported)
3. After registration, you automatically receive **16 CNY in free credits**

**Step 2: Create an API key**

1. After logging in, go to the [Console](https://cloud.siliconflow.cn/account/ak)
2. Select "API Keys" from the left menu
3. Click "Create New API Key"
4. Copy the generated key (starts with `sk-`)

> **Important**: The API key is only shown once. Copy and save it immediately in a secure location. If lost, you'll need to create a new one.

**Step 3: Top up (optional)**

After the free credits are used up, top up in the console's "Billing Center" — Alipay and WeChat Pay are supported.

> **Cost reference**: Using the DeepSeek V3 model, 16 CNY covers approximately 800–1500 conversations. Light daily usage costs about 10–30 CNY per month.

<details>
<summary>API Key setup for other providers</summary>

- **DeepSeek**: Visit https://platform.deepseek.com — register and create a key in the console, supports Alipay top-up
- **Qwen (Tongyi Qianwen)**: Visit https://dashscope.console.aliyun.com — under Alibaba Cloud, strong Chinese language support, enterprise-grade
- **Kimi (Moonshot)**: Visit https://platform.moonshot.cn — domestic team, strong Chinese comprehension
- **StepFun**: Visit https://platform.stepfun.com — strong multimodal capabilities, supports long context
- **MiniMax**: Visit https://platform.minimaxi.com — supports voice and multimodal
- **OpenRouter**: Visit https://openrouter.ai — one key for accessing multiple models

</details>

### 4.3 Configuring in the Wizard

Select your provider in the wizard and enter your API Key:

```
◇  Model/auth provider
│  ○ DeepSeek
│  ○ Kimi (Moonshot)
│  ○ OpenRouter
│  ● Custom (custom API endpoint) ← Select this for SiliconFlow
```

After selecting `Custom`, enter the following when prompted:

- **API Base URL**: `https://api.siliconflow.cn/v1`
- **API Key**: Paste the key you copied earlier
- **Default Model**: `deepseek-ai/DeepSeek-V3` (recommended)

You can also skip the wizard and configure manually via the command line:

```bash
openclaw config set llm.provider "siliconflow"
openclaw config set llm.baseUrl "https://api.siliconflow.cn/v1"
openclaw config set llm.apiKey "sk-xxxxx"
openclaw config set llm.default "deepseek-ai/DeepSeek-V3"
```

### 4.4 Configuring Chat Channels (Optional)

The wizard will ask whether to configure Slack, Telegram, or other chat channels. If you don't need them yet, skip this step — you can add channels later with `openclaw configure`.

### 4.5 Configuring Skills (Optional)

The wizard displays a list of available skills and asks whether to install them. We recommend skipping this for now and installing skills after you're familiar with the basics.

Once configuration is complete, the wizard automatically starts the Gateway daemon.

## 5. Verifying the Installation

Check the Gateway status:

```bash
openclaw status
```

If you see `Gateway service: running`, the installation was successful.

Open the Web dashboard:

```bash
openclaw dashboard
```

Your browser will automatically open `http://localhost:18789`, where you can chat with OpenClaw.

## 6. Your First Conversation

Try the following prompt in the dashboard:

```
Create a file called hello.txt with today's date and "Hello from OpenClaw!"
```

If OpenClaw successfully creates the file and confirms completion, everything is working. Try something more interesting:

```
Write a number guessing game in Python, save it as game.py and run it
```

> **Tip**: If OpenClaw only gives suggestions instead of executing commands, see the "Tools Profile" issue in the FAQ at the end of this chapter.

## 7. Cost and Budget Control

SiliconFlow's 16 CNY free credits are enough to complete the first few chapters. Daily usage costs depend on your call frequency and model choice.

**Cost-saving tips**:
- Use smaller models (e.g., Qwen2.5-7B) for simple tasks, and larger models (e.g., DeepSeek V3) only for complex tasks
- Chapter 8 covers multi-model routing and cost optimization strategies in detail

<details>
<summary>Advanced: Coding Plan subscriptions (for heavy users)</summary>

If you use OpenClaw heavily every day, pay-per-token pricing may not be economical. Some platforms offer fixed monthly Coding Plan subscriptions (e.g., Alibaba Cloud Bailian, Zhipu GLM) that provide access to coding-optimized models at a flat rate.

To configure: Run `openclaw configure`, select a Coding Plan provider in the wizard, and enter your subscription API Key. You can also add it manually in the Web dashboard under "Settings" → "All Settings".

> For most users, SiliconFlow's pay-as-you-go pricing is already cost-effective enough — no need for a Coding Plan subscription.

</details>

## 8. Common Commands

### Basic Commands

```bash
# Check overall status
openclaw status

# Deep health check
openclaw status --deep

# System diagnostics and repair
openclaw doctor

# Check version
openclaw --version

# View help
openclaw --help
```

### Gateway Management

```bash
# Check Gateway status
openclaw gateway status

# Start Gateway
openclaw gateway start

# Stop Gateway
openclaw gateway stop

# Restart Gateway (required after config changes)
openclaw gateway restart

# Run in foreground with logs (for debugging)
openclaw gateway run --verbose
```

### Model Management

```bash
# List available models
openclaw models list

# Check model status
openclaw models status

# Set default model
openclaw models set <provider/model>

# Check API authentication
openclaw models auth
```

### Channel Management

```bash
# List all channels
openclaw channels list

# Check channel connection status
openclaw channels status

# Add a new channel
openclaw channels add

# Log in to a channel (e.g., scan QR code for WhatsApp)
openclaw channels login

# Log out of a channel
openclaw channels logout
```

### Logs and Debugging

```bash
# Follow logs in real time
openclaw logs --follow

# View recent logs
openclaw logs
```

## 9. FAQ

**Q: OpenClaw only chats but doesn't take action — it gives suggestions instead of executing commands?**

A: This is the most common issue since version 2026.3.2, caused by the Tools Profile being set to "messaging". Two ways to fix it:

Method 1: Command line fix (recommended)

```bash
# Check current profile
openclaw config get tools

# If it's not "full", switch to full
openclaw config set tools.profile full

# Restart the gateway
openclaw gateway restart
```

Method 2: Web UI fix

1. Visit http://localhost:18789 (default local port)
2. Click "Settings" or "Agents" in the sidebar
3. Find the relevant Agent, click "tools" next to it
4. Select the "Full" option
5. Save and restart

Or edit the config file directly and change the tools section to:

```json
"tools": {
  "profile": "full"
}
```

**Q: Getting "API key not found" — what should I do?**

A: Edit the config file `openclaw.json` and make sure the API key is configured correctly. For example, using SiliconFlow:

```json
{
  "llm": {
    "provider": "siliconflow",
    "baseUrl": "https://api.siliconflow.cn/v1",
    "apiKey": "sk-xxxxx",
    "default": "deepseek-ai/DeepSeek-V3"
  }
}
```

**Q: Can't access the web dashboard?**

A: Check your firewall settings and make sure port 18789 is not in use by another application. You can change the port number in the config file.

**Q: Commands fail to execute?**

A: Make sure OpenClaw has sufficient file system permissions. Some operations may require explicit authorization.

---

**Next**: [Chapter 2: Understanding OpenClaw](/en/adopt/chapter2/)

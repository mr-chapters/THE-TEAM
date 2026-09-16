# 01-opencode/README.md

# OpenCode — The Model-Neutral Agent

OpenCode is the recommended starting point for The Team. It is a free, open-source terminal agent that works with virtually any AI model — including the free ones.

---

## What is OpenCode?

OpenCode is a terminal-first AI coding agent built by the team behind SST. It is deliberately **model-agnostic**: it does not lock you into Anthropic, OpenAI, or any single provider. You can point it at DeepSeek, Qwen, Groq, Gemini, local Ollama models, or any OpenAI-compatible endpoint.

It is not a chat window. It is a full agent that reads your project structure, plans changes, edits files, runs commands, and reviews diffs before touching your code.

**Key facts:**

| Feature | Detail |
|---------|--------|
| License | MIT (the tool itself is free) |
| Providers supported | 75+ out of the box |
| Privacy | Stores no code or context data on external servers |
| GitHub Stars | 172,000+ as of 2026 |
| Platform | macOS, Linux, Windows (WSL) |

---

## Why OpenCode for The Team?

| Reason | Why It Matters |
|--------|----------------|
| Model-neutral | You are not locked to one AI company |
| Free tool | You only pay for model inference (or use free models) |
| Privacy-first | Your code does not leave your machine (except to your chosen provider) |
| Plan then Build | Review changes before they happen — safer for beginners |
| Multi-session | Run parallel agents on separate tasks |
| Active development | Pushes updates daily |

---

## Installation

### Option 1: One-Line Install (Recommended)

```bash
curl -fsSL https://opencode.ai/install | bash
```

### Option 2: npm Global Install

```bash
npm install -g opencode-ai
```

### Option 3: Homebrew (macOS/Linux)

```bash
brew install sst/tap/opencode
```

### Option 4: Windows (Scoop)

```bash
scoop install opencode
```

### Option 5: Windows (WSL) — Recommended

```bash
wsl --install
wsl
curl -fsSL https://opencode.ai/install | bash
```

---

## First Launch

1. Open your terminal
2. Navigate to your project: `cd /path/to/your/project`
3. Run: `opencode`

On first launch, OpenCode will prompt you to select a model. It ships with **built-in free models** — pick one and you are running immediately, no API key required.

---

## Connecting Free Models

### Rung 1: Built-in Free Models (No Account)

OpenCode ships with free models built in. Just select one on first launch. This is the fastest way to start.

### Rung 2: OpenRouter Free Models

1. Create a free account at `openrouter.ai`
2. Generate an API key
3. In OpenCode, type `/connect` and select OpenRouter
4. Paste your key
5. Type `/models` and select a free model (look for `:free` suffix)

### Rung 3: Fully Local (Ollama)

Maximum privacy. Nothing leaves your machine.

```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama pull qwen2.5-coder:14b
```

Then configure OpenCode:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "ollama": {
      "npm": "ollama-ai-provider",
      "options": { "baseURL": "http://localhost:11434/v1" }
    }
  },
  "model": "ollama/qwen2.5-coder:14b"
}
```

---

## Core Workflow

### Plan vs Build

OpenCode has two modes. Toggle with `Tab`.

| Mode | What It Does |
|------|--------------|
| Plan | The agent drafts how it intends to implement something. No file changes. |
| Build | The agent makes the actual changes. |

**Always review the plan before switching to Build.** This is how you stay in control.

### AGENTS.md

OpenCode auto-loads `AGENTS.md` from your project root. This file gives the agent persistent context about your architecture and conventions.

Create one with:

```bash
opencode init
```

Commit `AGENTS.md` to your repo.

### Useful Commands

| Command | What It Does |
|---------|--------------|
| `/help` | List commands and keybinds |
| `/connect` | Connect a provider |
| `/models` | Switch models |
| `/new` | Start a new session |
| `/sessions` | List and switch sessions |
| `/share` | Share a session |
| `Tab` | Toggle Plan/Build mode |
| `Esc` | Interrupt the running agent |

---

## Quick Test

After setup, try this in your project:

```
Explain the structure of this project and suggest one improvement.
```

If OpenCode responds with an analysis of your code, you are running.

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| `opencode: command not found` | Restart terminal or add install path to PATH |
| Model not found | Check provider config and model ID spelling |
| Rate limits on free models | Switch to another free model with `/models` |
| Slow responses | Try a smaller local model or Groq (fast inference) |

---

## What Now?

Next: `02-miii/` for a fully local, offline agent.

> **Ethical Use Only**
> Only use these tools for lawful purposes.
> Never send sensitive code to free cloud models.

---

# 01-opencode/install.md

# OpenCode — Installation Guide

This guide covers every way to install OpenCode on your machine.

---

## Prerequisites

| Requirement | Details |
|-------------|---------|
| OS | macOS, Linux, or Windows (WSL recommended) |
| Node.js | Optional. Only needed for npm install method |
| Internet | Required for install and model access |

---

## Method 1: One-Line Install (Recommended)

Works on macOS and Linux. No prerequisites.

```bash
curl -fsSL https://opencode.ai/install | bash
```

The script detects your OS and architecture, downloads the correct binary, and configures your PATH.

**After install:**

```bash
source ~/.bashrc
# or
source ~/.zshrc
```

Verify:

```bash
opencode --version
```

If you see a version number, you are done.

---

## Method 2: npm Global Install

Requires Node.js 18 or higher.

```bash
npm install -g opencode-ai@latest
```

**Note:** The package name is `opencode-ai`, not `opencode`.

Alternative package managers:

```bash
bun install -g opencode-ai@latest
pnpm add -g opencode-ai@latest
yarn global add opencode-ai@latest
```

---

## Method 3: Homebrew (macOS and Linux)

**Official tap (recommended — updates faster):**

```bash
brew install anomalyco/tap/opencode
```

**Official formula (updates less often):**

```bash
brew install opencode
```

---

## Method 4: Windows

### Option A: WSL2 (Recommended)

OpenCode works best in WSL2 on Windows. The official team recommends this approach.

1. Install WSL2 if you have not already
2. Open your WSL terminal (Ubuntu, etc.)
3. Run the one-line install:

```bash
curl -fsSL https://opencode.ai/install | bash
```

**Tip:** Keep your project files inside the WSL filesystem (e.g., `~/projects`), not in `/mnt/c`. It is much faster.

### Option B: Scoop (No Admin Required)

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
scoop install git
scoop install opencode
```

### Option C: Chocolatey (Admin Required)

```powershell
choco install opencode
```

---

## Method 5: Desktop App (Beta)

OpenCode also has a desktop application.

**macOS:**

```bash
brew install --cask opencode-desktop
```

**Windows:**

```powershell
scoop bucket add extras
scoop install extras/opencode-desktop
```

**Direct downloads:** Available from the releases page or `opencode.ai/download`.

| Platform | File |
|----------|------|
| macOS (Apple Silicon) | `opencode-desktop-mac-arm64.dmg` |
| macOS (Intel) | `opencode-desktop-mac-x64.dmg` |
| Windows | `opencode-desktop-windows-x64.exe` |
| Linux | `.deb`, `.rpm`, or `.AppImage` |

---

## Method 6: Arch Linux

**Stable:**

```bash
sudo pacman -S opencode
```

**Latest from AUR:**

```bash
paru -S opencode-bin
# or
yay -S opencode-bin
```

---

## Method 7: Nix

```bash
nix run nixpkgs#opencode
```

For the latest dev branch:

```bash
nix run github:anomalyco/opencode
```

---

## Custom Install Directory

The install script follows this priority order:

1. `$OPENCODE_INSTALL_DIR`
2. `$XDG_BIN_DIR`
3. `$HOME/bin`
4. `$HOME/.opencode/bin`

**Example:**

```bash
OPENCODE_INSTALL_DIR=/usr/local/bin curl -fsSL https://opencode.ai/install | bash
```

---

## Verification

After any install method, verify:

```bash
opencode --version
```

If you see a version number, the install succeeded.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `opencode: command not found` | Restart terminal or source your shell config |
| Permission denied (npm) | Run `npm config set prefix "$HOME/.npm-global"` and add `$HOME/.npm-global/bin` to PATH |
| Slow in WSL | Move project files to `~/projects` instead of `/mnt/c` |
| Version too old | Remove versions older than 0.1.x before installing |

---

## What Now?

Next: `01-opencode/free-models.md` to connect free AI models.

> **Ethical Use Only**
> Only use these tools for lawful purposes.

---

# 01-opencode/free-models.md

# OpenCode — Free Models Guide

OpenCode is model-neutral. You can point it at free AI models without paying for a subscription. This guide covers every free route.

---

## Free Model Options

| Provider | Free Tier | API Key Needed? | Best For |
|----------|-----------|-----------------|----------|
| OpenCode Zen | Free models built-in | No | Easiest start |
| OpenRouter | 50 requests/day free | Yes | Variety |
| Groq | 14,400 requests/day | Yes | Speed |
| Gemini | 1,500 requests/day | Yes | Google models |
| DeepSeek | Paid (very cheap) | Yes | Quality coding |
| Ollama | Unlimited (local) | No | Privacy |

---

## Rung 1: OpenCode Zen (Built-in Free Models)

OpenCode ships with free models built in. No account, no API key, no credit card.

**How to use:**

1. Start OpenCode:

```bash
opencode
```

2. Type `/models`
3. Look for models with `-free` suffix
4. Select one

**Available free models (as of 2026):**

| Model | Context | Notes |
|-------|---------|-------|
| DeepSeek V4 Flash Free | 200K | SWE-bench ~79% |
| Nemotron 3 Ultra Free | 1M | NVIDIA flagship |
| MiMo V2.5 Free | 200K | Xiaomi coding model |
| Muse Spark 1.2 Free | 1M | Contributor free |

**Warning:** Free models may collect data to improve the model. Do not send sensitive code.

---

## Rung 2: OpenRouter Free Models

OpenRouter is a gateway to many models. Some are free.

**Setup:**

1. Create a free account at `openrouter.ai`
2. Generate an API key
3. In OpenCode, type `/connect` and select OpenRouter
4. Paste your key
5. Type `/models` and select a model with `:free` suffix

**Free tier limits:**

- 50 requests/day without credits
- 1,000 requests/day if you add $10 credit once

---

## Rung 3: Groq (Fast Inference)

Groq offers very fast inference on free models.

**Setup:**

1. Create account at `console.groq.com`
2. Generate API key
3. Add to OpenCode config

**Free tier limits:**

- 30 requests/minute
- 14,400 requests/day

**Models:** Llama, Qwen, GPT-OSS, and more.

**Why Groq:** Fastest inference available. Great for quick coding tasks.

---

## Rung 4: Gemini (Google)

Google offers free API access via AI Studio.

**Setup:**

1. Go to `aistudio.google.com`
2. Get API key (no credit card)
3. Add to OpenCode

**Free tier limits:**

- 10-15 requests/minute
- 1,500 requests/day (varies)

**Models:** Flash-class models.

**Warning:** Google may use free-tier data to improve products. Do not send sensitive code.

---

## Rung 5: DeepSeek (Cheapest Paid)

DeepSeek does not have a free API tier, but it is extremely cheap.

**Pricing (off-peak, per 1M tokens):**

| Type | Cost |
|------|------|
| Input (cache hit) | $0.007 |
| Input (cache miss) | $0.22 |
| Output | $0.66 |

**Setup:**

1. Create account at `platform.deepseek.com`
2. Add $2 credit (goes a long way)
3. Generate API key
4. Add to OpenCode

**Why DeepSeek:** Among the cheapest frontier-class APIs. Excellent for coding.

---

## Rung 6: Ollama (Fully Local, Free Forever)

Run models on your own machine. No API keys, no limits, no cost.

**Setup:**

1. Install Ollama:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

2. Pull a coding model:

```bash
ollama pull qwen2.5-coder:14b
```

3. Configure OpenCode (`opencode.json`):

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "ollama": {
      "npm": "ollama-ai-provider",
      "options": { "baseURL": "http://localhost:11434/v1" }
    }
  },
  "model": "ollama/qwen2.5-coder:14b"
}
```

**Requirements:**

- 16GB+ RAM
- Decent GPU (optional but faster)
- 10GB+ free disk space

**Why Ollama:** 100% private. Nothing leaves your machine. Unlimited use.

---

## Configuring OpenCode

### Default model in project

Create `opencode.json` in your project root:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "provider_id/model_id"
}
```

**Example (OpenCode Zen free model):**

```json
{
  "model": "opencode/deepseek-v4-flash-free"
}
```

**Example (Ollama):**

```json
{
  "model": "ollama/qwen2.5-coder:14b"
}
```

### Full provider config (for custom providers)

If you use a provider not built-in, you need full config:

```json
{
  "provider": {
    "example": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Example AI",
      "options": {
        "baseURL": "https://api.example.com/v1",
        "apiKey": "YOUR_KEY"
      },
      "models": {
        "example-coder": {
          "name": "Example Coder"
        }
      }
    }
  },
  "model": "example/example-coder"
}
```

**Key fields:**

| Field | Meaning |
|-------|---------|
| `example` | Provider ID (must match what you entered in `/connect`) |
| `npm` | The AI SDK package to use |
| `baseURL` | API endpoint |
| `example-coder` | Real model ID from the provider |
| `name` | Display name in OpenCode UI |

---

## Quick Comparison

| Route | Cost | Privacy | Speed | Setup |
|-------|------|---------|-------|-------|
| OpenCode Zen | Free | Low | Medium | None |
| OpenRouter | Free | Low | Medium | Easy |
| Groq | Free | Low | Very Fast | Easy |
| Gemini | Free | Low | Medium | Easy |
| DeepSeek | ~$1/mo | Low | Medium | Easy |
| Ollama | Free | High | Varies | Medium |

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Model not found | Check provider ID and model ID spelling |
| 404 error | Check `baseURL` and API protocol (`/v1/chat/completions`) |
| Rate limited | Switch to another free model |
| Slow responses | Use Groq or a smaller local model |
| Ollama not working | Check Ollama is running: `ollama list` |

---

## What Now?

Next: `02-miii/README.md` for the local agent.

> **Ethical Use Only**
> Never send sensitive code to free cloud models.
> Use Ollama for private work.

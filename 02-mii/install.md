# miii — Installation Guide

This guide covers every step to install miii on your machine, from Node.js to your first prompt.

---

## Prerequisites

| Requirement | Details |
|-------------|---------|
| **Node.js** | 18 or higher |
| **npm** | Comes with Node.js |
| **Ollama** | Must be installed and running |
| **OS** | Linux, macOS, or Windows (WSL recommended) |
| **RAM** | 16GB+ recommended |
| **GPU** | Optional but strongly recommended |

---

## Step 1: Install Node.js

### Linux (Ubuntu/Debian)

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

### macOS (Homebrew)

```bash
brew install node
```

### Windows

Download from `nodejs.org` or use winget:

```powershell
winget install OpenJS.NodeJS.LTS
```

**Verify:**

```bash
node --version
npm --version
```

You should see Node 18 or higher.

---

## Step 2: Install Ollama

miii uses Ollama by default.

### Linux

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### macOS

```bash
brew install ollama
```

### Windows

Download from `ollama.com/download/windows`.

**Verify:**

```bash
ollama --version
```

**Start the service (Linux):**

```bash
sudo systemctl start ollama
sudo systemctl enable ollama
```

---

## Step 3: Pull a Coding Model

| VRAM | Recommended Model | Pull Command |
|------|-------------------|--------------|
| 6 GB | Qwen2.5-Coder 7B | `ollama pull qwen2.5-coder:7b` |
| 10 GB | Qwen2.5-Coder 14B | `ollama pull qwen2.5-coder:14b` |
| 24 GB | Qwen3-Coder 30B | `ollama pull qwen3-coder:30b` |
| 16 GB RAM (no GPU) | GPT-OSS 20B | `ollama pull gpt-oss:20b` |

**Example:**

```bash
ollama pull qwen2.5-coder:14b
```

**Verify:**

```bash
ollama list
```

---

## Step 4: Install miii

```bash
npm install -g miii-agent
```

**If you get permission errors:**

```bash
npm config set prefix "$HOME/.npm-global"
export PATH="$HOME/.npm-global/bin:$PATH"
npm install -g miii-agent
```

Add the export line to your shell config to make it permanent:

```bash
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

**Verify:**

```bash
miii --version
```

---

## Step 5: First Launch

```bash
miii
```

A model picker opens. Select your Ollama model from the list. Start coding.

**Try this prompt:**

```
Explain the structure of this project and suggest one improvement.
```

If miii responds with an analysis of your code, setup is complete.

---

## Configuration

### Config File Location

| Scope | Path |
|-------|------|
| Project | `.miii.json` in project root |
| User | `~/.config/miii/config.json` |

### Example Config

```json
{
  "model": "qwen2.5-coder:14b",
  "provider": "ollama",
  "baseUrl": "http://localhost:11434"
}
```

### Switching Providers

**Ollama (default):**

```json
{
  "model": "llama3.2",
  "provider": "ollama",
  "baseUrl": "http://localhost:11434"
}
```

**OpenAI-compatible:**

```json
{
  "model": "gpt-4o",
  "provider": "openai",
  "baseUrl": "https://api.openai.com/v1",
  "apiKey": "sk-xxx"
}
```

---

## Sessions

Every conversation is saved automatically.

```bash
miii                          # resumes "default" session
miii --session feature-auth   # resumes or creates named session
miii -s work -m llama3.2      # short flags
```

Sessions stored at `~/.config/miii/sessions/`.

---

## Custom Slash Commands

Create `.miii/commands/review.md`:

```markdown
---
description: review the staged diff
---
Review the staged diff for bugs and unhandled errors. Focus on $ARGUMENTS.
```

This becomes `/review` inside miii.

- Project commands: `.miii/commands/` (check into git)
- Personal commands: `~/.miii/commands/`

---

## Verification

Run these checks:

```bash
# Node.js
node --version

# Ollama
ollama --version
ollama list

# miii
miii --version

# Test prompt
miii
# Inside miii: "What files are in this project?"
```

If all commands return results, installation is complete.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `miii: command not found` | Add npm global bin to PATH |
| `npm install` permission denied | Set npm prefix to `$HOME/.npm-global` |
| Ollama not running | Run `ollama serve` |
| Model not found | Pull it first: `ollama pull <model>` |
| Slow responses | Use a smaller model (7b instead of 14b) |
| Connection refused | Check Ollama is running on port 11434 |
| Node version too old | Install Node 18 or higher |

---

## What Now?

Return to `02-miii/README.md` for the full workflow guide, or move to `03-aider/install.md`.

> **Ethical Use Only**
> Only use these tools for lawful purposes.

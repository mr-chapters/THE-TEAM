# Ollama — Fully Local, Zero Cost

Ollama is the privacy-first option in The Team. It runs open-weight AI models directly on your machine. No API keys, no cloud, no cost, no data leaving your computer.

---

## What is Ollama?

Ollama is a local runtime for large language models. It downloads open-weight models and serves them through a local API that coding agents can connect to. Nothing ever leaves your machine.

**Key facts:**

- **License:** MIT (open source)
- **Cost:** Free forever
- **Privacy:** 100% local
- **Platforms:** Linux, macOS, Windows
- **API:** OpenAI-compatible and Anthropic-compatible

---

## Why Ollama for The Team?

| Reason | Why It Matters |
|--------|----------------|
| Zero cost | No subscriptions, no per-token billing |
| 100% private | Your code never leaves your machine |
| No API keys | No accounts, no credit cards |
| Unlimited use | No rate limits, no daily quotas |
| Works offline | No internet required after model download |

---

## Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| RAM | 16 GB | 32 GB |
| Disk | 15 GB free | 25 GB free |
| GPU | Not required (CPU works) | NVIDIA 8GB+ VRAM |
| OS | Windows 10+, macOS 12+, Linux | — |

---

## Installation

### Linux

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

Start the service:

```bash
sudo systemctl start ollama
sudo systemctl enable ollama
```

### macOS

Download from `ollama.com/download/mac` or use Homebrew:

```bash
brew install ollama
```

Ollama runs as a background service automatically after installation.

### Windows

Download the installer from `ollama.com/download/windows` and run it. Ollama starts automatically.

Or use winget:

```powershell
winget install Ollama.Ollama
```

---

## Pulling Models

### Recommended Coding Models

| Model | Size | Context | Best For |
|-------|------|---------|----------|
| qwen3-coder:30b | 19 GB | 256K | Best quality-per-VRAM |
| devstral:24b | 14 GB | 128K | Benchmarked agentic coding |
| gpt-oss:20b | 14 GB | 128K | Runs on 16GB RAM without GPU |

**Pull a model:**

```bash
ollama pull qwen3-coder:30b
```

**Verify:**

```bash
ollama list
```

---

## The Context Length Trap

This is the most important thing to configure. Ollama chooses a default context length based on available VRAM:

| VRAM | Default Context |
|------|----------------|
| Under 24 GB | 4,096 tokens |
| 24-48 GB | 32,768 tokens |
| 48 GB+ | 262,144 tokens |

**The problem:** A coding agent passes 4,096 tokens before it does any work. System prompt, tool definitions, repository listing, and the first file it opens already exceed that. Ollama silently discards the oldest tokens. No error. The model answers confidently about a file it can no longer see.

**The fix:** Set context length on the server, not the agent.

```bash
sudo systemctl edit ollama.service
```

Add:

```
[Service]
Environment="OLLAMA_CONTEXT_LENGTH=64000"
```

Reload and restart:

```bash
sudo systemctl daemon-reload
sudo systemctl restart ollama
```

**Verify:**

```bash
ollama ps
```

The CONTEXT column shows what the model actually received.

---

## Keeping Models Loaded

By default, Ollama unloads a model 5 minutes after the last request. For agent work, this is wrong — you pause to read a diff, the timer runs out, and the next request reloads tens of gigabytes.

**Fix:**

```
[Service]
Environment="OLLAMA_KEEP_ALIVE=-1"
```

`-1` keeps the model loaded indefinitely.

---

## Connecting to The Team Tools

### OpenCode

OpenCode has native Ollama integration:

```bash
ollama launch opencode
```

This starts OpenCode with Ollama config inline.

Or set the base URL manually:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "ollama": {
      "npm": "ollama-ai-provider",
      "options": { "baseURL": "http://localhost:11434/v1" }
    }
  },
  "model": "ollama/qwen3-coder:30b"
}
```

### Aider

Aider recommends the `ollama_chat/` prefix:

```bash
export OLLAMA_API_BASE=http://127.0.0.1:11434
aider --model ollama_chat/qwen3-coder:30b
```

Pin the context window per model:

```yaml
# .aider.model.settings.yml
- name: ollama_chat/qwen3-coder:30b
  extra_params:
    num_ctx: 65536
```

### miii

miii uses Ollama by default. No configuration needed:

```bash
miii
# Select your Ollama model from the picker
```

### Claude Code

Ollama provides an Anthropic-compatible endpoint:

```bash
export ANTHROPIC_BASE_URL=http://localhost:11434
ollama launch claude --model qwen3-coder:30b
```

---

## Available Models

| Model | Pull Command | VRAM Needed |
|-------|--------------|-------------|
| Qwen3-Coder 30B | `ollama pull qwen3-coder:30b` | 24 GB |
| Devstral 24B | `ollama pull devstral:24b` | 16 GB |
| GPT-OSS 20B | `ollama pull gpt-oss:20b` | 16 GB RAM (no GPU) |
| Qwen2.5-Coder 14B | `ollama pull qwen2.5-coder:14b` | 10 GB |
| Qwen2.5-Coder 7B | `ollama pull qwen2.5-coder:7b` | 6 GB |

**Rule:** Pick the largest model that fits your GPU. Bigger is better for coding.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `ollama: command not found` | Restart terminal or check install path |
| Model not found | Pull it first: `ollama pull <model>` |
| Slow responses | Check `ollama ps` — if PROCESSOR shows CPU, model is too big |
| Context truncated | Set `OLLAMA_CONTEXT_LENGTH=64000` |
| Model unloads constantly | Set `OLLAMA_KEEP_ALIVE=-1` |
| Connection refused | Start service: `sudo systemctl start ollama` |

---

## What Now?

You have finished all provider guides. Return to `01-opencode/`, `02-miii/`, or `03-aider/` to connect a provider and start coding.

> **Ethical Use Only**
> Only use these tools for lawful purposes.

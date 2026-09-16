# Free AI Providers

This folder contains setup guides for every free AI provider supported by The Team. Each guide covers signup, API key setup, free tier limits, and how to connect the provider to OpenCode, miii, or Aider.

---

## Provider Overview

| Provider | Free Tier | API Key | Best For |
|----------|-----------|---------|----------|
| OpenCode Zen | Built-in free models | No | Easiest start |
| OpenRouter | 50 requests/day | Yes | Model variety |
| Groq | 14,400 requests/day | Yes | Speed |
| Gemini | 1,500 requests/day | Yes | Google models |
| DeepSeek | Paid (very cheap) | Yes | Quality coding |
| Ollama | Unlimited (local) | No | Privacy |

---

## Guides in This Folder

| File | What It Covers |
|------|----------------|
| `deepseek.md` | Cheapest frontier-class API |
| `qwen.md` | Free coding models from Alibaba |
| `groq.md` | Fastest inference available |
| `gemini.md` | Google's free API tier |
| `ollama.md` | Fully local, zero cost |

---

## How to Use These Guides

1. Pick a provider that matches your needs
2. Follow the setup steps in its guide
3. Add the API key to your agent (OpenCode, miii, or Aider)
4. Start coding

---

## Provider Comparison

### Cost

| Provider | Cost Model |
|----------|------------|
| OpenCode Zen | Free |
| OpenRouter | Free tier (50/day) |
| Groq | Free tier (14,400/day) |
| Gemini | Free tier (1,500/day) |
| DeepSeek | ~$0.22 per 1M input tokens |
| Ollama | Free (your hardware) |

### Privacy

| Provider | Data Privacy |
|----------|--------------|
| OpenCode Zen | May use data for training |
| OpenRouter | Varies by model |
| Groq | Check terms |
| Gemini | May use data for training |
| DeepSeek | Check terms |
| Ollama | 100% private |

### Speed

| Provider | Latency |
|----------|---------|
| Groq | Very fast |
| Ollama | Depends on hardware |
| OpenCode Zen | Medium |
| OpenRouter | Medium |
| Gemini | Medium |
| DeepSeek | Medium |

---

## Quick Start

### Easiest (No Setup)

Use OpenCode Zen built-in free models:

```bash
opencode
/models
# Select a model with "-free" suffix
```

### Best Free Tier

Use Groq:

```bash
export GROQ_API_KEY=your_key
aider --model groq/llama-3.3-70b-versatile
```

### Best Privacy

Use Ollama:

```bash
ollama pull qwen2.5-coder:14b
aider --model ollama/qwen2.5-coder:14b
```

---

## What Now?

Pick a provider guide from the table above and follow the setup steps.

> **Ethical Use Only**
> Never send sensitive code to free cloud models.
> Use Ollama for private work.

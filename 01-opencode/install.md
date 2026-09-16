# OpenCode — Free Models Guide

This guide shows you how to connect free AI models to OpenCode. No subscriptions. No paid API keys required if you use the right setup.

---

## The Free Model Ladder

Start at Rung 0. Move up only if you need more power or privacy.

| Rung | Setup | Cost | Privacy | Setup Time |
|------|-------|------|---------|------------|
| 0 | Built-in free models | Free | Cloud | 0 minutes |
| 1 | OpenRouter free tier | Free | Cloud | 5 minutes |
| 2 | Groq free tier | Free | Cloud | 5 minutes |
| 3 | Google Gemini free tier | Free | Cloud | 5 minutes |
| 4 | Local Ollama | Free | 100% local | 20 minutes |

---

## Rung 0: Built-in Free Models (No Account)

OpenCode ships with free models built in. No API key. No account. No setup.

**How to use:**

1. Open your terminal
2. Navigate to your project: `cd /path/to/project`
3. Run: `opencode`
4. On first launch, select a built-in free model from the list
5. Start coding

**Pros:**
- Zero setup
- Works instantly
- No account needed

**Cons:**
- Rate limits
- Less powerful than paid models
- Model availability changes

---

## Rung 1: OpenRouter Free Models

OpenRouter is a gateway to many AI models. Several are free at any given time.

**Step 1: Create account**

1. Go to `openrouter.ai`
2. Sign up with email or Google
3. Verify your email

**Step 2: Get API key**

1. Go to `openrouter.ai/keys`
2. Click **Create Key**
3. Name it "OpenCode"
4. Copy the key (starts with `sk-or-`)

**Step 3: Connect to OpenCode**

1. Open OpenCode: `opencode`
2. Type `/connect`
3. Select **OpenRouter**
4. Paste your API key
5. Press Enter

**Step 4: Select a free model**

1. Type `/models`
2. Look for models with `:free` suffix
3. Select one

**Free model examples:**

| Model | Context | Best For |
|-------|---------|----------|
| `deepseek/deepseek-chat:free` | 64K | General coding |
| `qwen/qwen-2.5-coder-32b:free` | 32K | Code generation |
| `google/gemini-flash-1.5:free` | 1M | Large files |
| `meta-llama/llama-3.3-70b:free` | 128K | General purpose |

**Rate limits:**
- 50 requests/day without credits
- 1,000 requests/day if you buy $10 credits once

**Pros:**
- Many models
- Easy to switch
- Free tier available

**Cons:**
- Daily limits
- Some models get rate-limited at peak times
- Requires account

---

## Rung 2: Groq Free Tier

Groq offers extremely fast inference on open-source models. Free tier with no credit card required.

**Step 1: Create account**

1. Go to `console.groq.com`
2. Sign up with email or Google
3. Verify your email

**Step 2: Get API key**

1. Go to **API Keys** in the console
2. Click **Create API Key**
3. Copy the key (starts with `gsk_`)

**Step 3: Connect to OpenCode**

1. Open OpenCode: `opencode`
2. Type `/connect`
3. Select **Groq**
4. Paste your API key

**Step 4: Select a model**

1. Type `/models`
2. Select a Groq model

**Available models:**

| Model | Context | Speed | Best For |
|-------|---------|-------|----------|
| `llama-3.3-70b-versatile` | 128K | Very fast | General coding |
| `llama-3.1-8b-instant` | 128K | Fastest | Quick tasks |
| `mixtral-8x7b-32768` | 32K | Fast | Code review |
| `gemma2-9b-it` | 8K | Fast | Simple tasks |

**Rate limits:**
- 14,400 requests/day
- No credit card required

**Pros:**
- Very fast
- Generous free tier
- No credit card

**Cons:**
- Fewer models than OpenRouter
- Rate limits on larger models

---

## Rung 3: Google Gemini Free Tier

Google offers free Gemini API access with generous limits.

**Step 1: Create account**

1. Go to `aistudio.google.com`
2. Sign in with Google account
3. Accept terms

**Step 2: Get API key**

1. Click **Get API Key**
2. Create a new key
3. Copy the key

**Step 3: Connect to OpenCode**

1. Open OpenCode: `opencode`
2. Type `/connect`
3. Select **Google**
4. Paste your API key

**Step 4: Select a model**

| Model | Context | Best For |
|-------|---------|----------|
| `gemini-2.0-flash` | 1M | Fast, general coding |
| `gemini-2.0-flash-lite` | 1M | Lightweight tasks |
| `gemini-1.5-pro` | 2M | Complex reasoning |

**Rate limits:**
- 1,500 requests/day
- 1M tokens/minute
- No credit card required

**Pros:**
- Very large context window
- Fast
- Free tier generous

**Cons:**
- Google account required
- Some models region-locked

---

## Rung 4: Local Ollama (100% Private)

Run models entirely on your own machine. No cloud. No API keys. No rate limits.

**Requirements:**

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| RAM | 8 GB | 16 GB |
| Storage | 10 GB | 50 GB |
| GPU | Optional | NVIDIA 8GB+ |

**Step 1: Install Ollama**

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Windows:** Download from `ollama.com/download`

**Step 2: Pull a coding model**

```bash
# Small, fast, good for most tasks
ollama pull qwen2.5-coder:7b

# Bigger, better quality
ollama pull qwen2.5-coder:14b

# Best quality (needs 16GB+ RAM)
ollama pull qwen2.5-coder:32b

# DeepSeek alternative
ollama pull deepseek-coder-v2:16b
```

**Step 3: Configure OpenCode**

Edit your config file. Location depends on OS:

| OS | Path |
|----|------|
| Linux | `~/.config/opencode/opencode.json` |
| macOS | `~/.config/opencode/opencode.json` |
| Windows | `%APPDATA%\opencode\opencode.json` |

Add this:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "ollama": {
      "npm": "ollama-ai-provider",
      "options": {
        "baseURL": "http://localhost:11434/v1"
      }
    }
  },
  "model": "ollama/qwen2.5-coder:14b"
}
```

**Step 4: Test**

```bash
opencode
```

Type a prompt. If it responds, Ollama is connected.

**Recommended models by RAM:**

| RAM | Model | Quality |
|-----|-------|---------|
| 8 GB | `qwen2.5-coder:7b` | Good |
| 16 GB | `qwen2.5-coder:14b` | Better |
| 32 GB | `qwen2.5-coder:32b` | Best |
| 64 GB+ | `deepseek-coder-v2:33b` | Excellent |

**Pros:**
- 100% private
- No rate limits
- No internet needed
- Free forever

**Cons:**
- Needs good hardware
- Slower than cloud
- Smaller models than cloud

---

## Switching Models

In OpenCode, type `/models` at any time to switch.

**Quick tips:**
- Use a small model for simple tasks
- Use a large model for complex reasoning
- Use Ollama when offline or for sensitive code

---

## Model Comparison

| Model | Speed | Quality | Privacy | Free |
|-------|-------|---------|---------|------|
| OpenCode built-in | Medium | Good | Cloud | ✅ |
| DeepSeek (OpenRouter) | Medium | Very good | Cloud | ✅ |
| Qwen (OpenRouter) | Medium | Very good | Cloud | ✅ |
| Llama 3.3 (Groq) | Very fast | Good | Cloud | ✅ |
| Gemini Flash | Fast | Very good | Cloud | ✅ |
| Qwen Coder (Ollama) | Slow | Good | Local | ✅ |

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Model not found | Check spelling and provider config |
| Rate limit hit | Switch to another free model with `/models` |
| Ollama connection refused | Make sure Ollama is running: `ollama serve` |
| Slow responses | Use Groq or a smaller local model |
| API key rejected | Regenerate key on provider site |

---

## What Now?

Next: `02-miii/README.md` for a fully local offline agent.

> **Ethical Use Only**
> Only use these tools for lawful purposes.
> Never send sensitive code to free cloud models.

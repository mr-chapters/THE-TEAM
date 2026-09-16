# Groq — Fastest Free Inference

Groq is the speed king. Their custom LPU hardware delivers 280-1,000 tokens per second, and their free tier requires no credit card. If you want fast coding with zero cost, this is the best option.

---

## What is Groq?

Groq (not to be confused with Grok from xAI) is a cloud inference platform built around custom LPU (Language Processing Unit) hardware. They don't train their own models — they host open-weight models from Meta, OpenAI, Qwen, and others at extremely high speed.

**Key facts:**

- **Free tier:** No credit card, access to every model
- **Speed:** 280-1,000 tokens/second depending on model
- **Models:** Llama, GPT-OSS, Qwen, Kimi, Whisper
- **API:** OpenAI-compatible
- **Best for:** Fast, free coding with generous limits

---

## Is Groq Free?

Yes. Groq's free tier is genuinely free — no credits system, no per-token charge, no credit card required. Access is gated only by rate limits [citation:1][citation:19].

| Tier | Cost | Limits |
|------|------|--------|
| **Free** | $0 | 30 req/min, 14,400 req/day |
| **Developer** | Free (add card) | 10x higher limits + 25% discount |

Rate limits apply at the organization level. Adding more API keys does not raise them [citation:19].

---

## Free Tier Limits

| Limit | Value |
|-------|-------|
| Requests per minute | 30 |
| Requests per day | 14,400 |
| Tokens per minute | ~6,000 (varies by model) |
| Tokens per day | Varies by model |

**Per-model example (Qwen3.6-27B):** 30 RPM, 1,000 RPD, 8K TPM, 200K TPD [citation:7].

---

## Available Models

| Model | Context | Speed | Best For |
|-------|---------|-------|----------|
| `llama-3.3-70b-versatile` | 131K | Fast | General coding |
| `llama-3.1-8b-instant` | 131K | Very fast | Quick tasks |
| `openai/gpt-oss-120b` | 128K | Fast | Reasoning |
| `openai/gpt-oss-20b` | 128K | Very fast | Budget tasks |
| `qwen/qwen3.8-27b` | 131K | Fast | Multimodal |
| `moonshotai/kimi-k2-instruct` | 262K | Fast | Agentic coding |
| `whisper-large-v3-turbo` | — | Ultra fast | Voice transcription |

---

## Setup for The Team Tools

### OpenCode

Groq has native OpenCode support [citation:16].

```bash
# Inside OpenCode TUI
/connect
# Search for Groq, select it, enter your API key

/models
# Select a Groq model
```

Or set the environment variable:

```bash
export GROQ_API_KEY=gsk_xxx
opencode
```

### Aider

Aider's official docs confirm Groq support. Llama 3 70B on Groq is comparable to GPT-3.5 in code editing [citation:3][citation:9].

```bash
export GROQ_API_KEY=gsk_xxx
aider --model groq/llama3-70b-8192
```

List available models:

```bash
aider --list-models groq/
```

### miii

miii uses Ollama by default. To use Groq API instead, configure an OpenAI-compatible provider:

```json
{
  "model": "llama-3.3-70b-versatile",
  "provider": "openai",
  "baseUrl": "https://api.groq.com/openai/v1",
  "apiKey": "gsk_xxx"
}
```

---

## Getting an API Key

1. Go to `console.groq.com/keys`
2. Create an account (email or GitHub)
3. Click "Create API Key"
4. Copy the key (starts with `gsk_`)
5. Set it:

```bash
export GROQ_API_KEY="gsk_your-key-here"
```

**Tip:** Add the export to `~/.bashrc` or `~/.zshrc` to make it permanent.

---

## Privacy

Groq does not use API data for model training by default. Customer data is not retained for inference requests unless needed for abuse monitoring or system reliability (up to 30 days) [citation:6].

| Feature | Policy |
|---------|--------|
| Training on your data | No |
| Data retention (default) | None |
| Zero Data Retention (ZDR) | Available in settings |
| Data location | Google Cloud US |

**For sensitive code:** Enable Zero Data Retention in Data Controls settings, or use Ollama (local) [citation:6].

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| 401 Invalid API Key | Check key starts with `gsk_`, verify export |
| 429 Too Many Requests | Wait for rate limit reset, or switch models |
| Model silently skips tool calls | Use Llama 3.3 70B or newer for reliable tool use [citation:17] |
| Slow responses | Try a smaller model like `llama-3.1-8b-instant` |
| `GROQ_API_KEY` not found | Restart shell after adding to config |

---

## What Now?

Next: `04-providers/gemini.md` for Google's free API tier.

> **Ethical Use Only**
> Never send sensitive code to free cloud models.
> Use Ollama for private work.

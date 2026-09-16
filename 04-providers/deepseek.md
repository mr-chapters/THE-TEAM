# DeepSeek — Cheapest Frontier-Class API

DeepSeek is the cheapest way to get frontier-level coding quality without paying flagship prices. The API is not free, but it is so cheap that hobby projects run on pocket change.

---

## What is DeepSeek?

DeepSeek is a Chinese AI company that builds open-weight and proprietary models. Their coding models (V4 Flash and V4 Pro) are competitive with much more expensive Western models at a fraction of the cost.

**Key facts:**

- **Models:** DeepSeek V4 Flash (budget), DeepSeek V4 Pro (flagship)
- **License:** MIT for open weights (self-hosting)
- **API:** OpenAI-compatible and Anthropic-compatible
- **Context:** 1M tokens
- **Best for:** Cost-effective coding without sacrificing quality

---

## Is DeepSeek Free?

Three honest answers:

| Use Case | Free? |
|----------|-------|
| Web chat (chat.deepseek.com) | Yes, free forever |
| API | No, but very cheap |
| Self-hosted (MIT weights) | Free to license, expensive to run |

The web chat is free but has no API. The API is paid. The weights are open source but require serious hardware to run locally.

---

## API Pricing (August 2026)

DeepSeek uses peak/off-peak pricing. Off-peak is half of peak. Peak hours are 01:00-04:00 and 06:00-10:00 UTC on weekdays.

### DeepSeek V4 Flash (Budget)

| Token Type | Off-Peak | Peak |
|------------|----------|------|
| Input (cache hit) | $0.003 | $0.006 |
| Input (cache miss) | $0.15 | $0.30 |
| Output | $0.60 | $1.20 |

### DeepSeek V4 Pro (Flagship)

| Token Type | Off-Peak | Peak |
|------------|----------|------|
| Input (cache hit) | $0.022 | $0.044 |
| Input (cache miss) | $0.66 | $1.32 |
| Output | $1.98 | $3.96 |

### Real-World Cost Example

A hobby project that sends 5M tokens of fresh input and generates 1M tokens of output per month, running off-peak on Flash:

- Input: 5M × $0.15 = $0.75
- Output: 1M × $0.60 = $0.60
- **Total: $1.35/month**

That is pocket change for a coding agent that runs all month.

---

## Free Options

### Web Chat (Free)

Visit `chat.deepseek.com`. No credit card. Full model access. No API.

**Limitation:** Cannot be scripted or wired into your terminal agent.

### OpenCode Zen Free Models

OpenCode ships with DeepSeek V4 Flash Free built in. No API key required.

```bash
opencode
/models
# Select a model with "-free" suffix
```

**Warning:** Data during the free period may be used to improve the model. Do not send sensitive code.

### OpenRouter (Limited Free)

OpenRouter offers 50 free requests/day on select models. DeepSeek's free variants were pulled from the pool by mid-2026, so current DeepSeek listings are paid.

---

## Setup for The Team Tools

### OpenCode

**Option A: Free model (no key)**

```bash
opencode
/models
# Select opencode/deepseek-v4-flash-free
```

**Option B: Paid API**

```bash
export DEEPSEEK_API_KEY=sk-xxx
opencode
/models
# Select deepseek/deepseek-chat
```

### Aider

```bash
export DEEPSEEK_API_KEY=sk-xxx
aider --model deepseek/deepseek-chat
```

### miii

miii uses Ollama by default. To use DeepSeek API instead, configure an OpenAI-compatible provider:

```json
{
  "model": "deepseek-chat",
  "provider": "openai",
  "baseUrl": "https://api.deepseek.com"
}
```

---

## Getting an API Key

1. Go to `platform.deepseek.com`
2. Create an account
3. Top up your balance (minimum $2)
4. Generate an API key
5. Set it as `DEEPSEEK_API_KEY`

**Note:** New accounts may receive trial credits, but this is not guaranteed. Treat it as a top-up-required service.

---

## Privacy

| Route | Privacy |
|-------|---------|
| Web chat | Data may be used for training |
| Free API (OpenCode Zen) | Data may be used for training |
| Paid API | Check DeepSeek's terms |
| Self-hosted | 100% private |

**For sensitive code:** Use Ollama (local) or a provider with a zero-retention policy.

---

## Model Comparison

| Model | Best For | Cost |
|-------|----------|------|
| deepseek-flash | Daily coding, high volume | Cheap |
| deepseek-v4-pro | Complex reasoning, architecture | Moderate |

Start with Flash. Move to Pro only when you need the extra capability.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| API key not working | Verify key and check balance |
| 402 Payment Required | Top up your balance |
| Rate limited | Wait or switch to off-peak hours |
| Model not found | Check model ID (`deepseek-chat` or `deepseek-v4-pro`) |

---

## What Now?

Next: `04-providers/qwen.md` for free coding models from Alibaba.

> **Ethical Use Only**
> Never send sensitive code to free cloud models.

# Qwen — Free Coding Models from Alibaba

Qwen is Alibaba's AI model family. It includes some of the best open-weight coding models available, and Alibaba gives new users a generous free API quota.

---

## What is Qwen?

Qwen (short for Tongyi Qianwen) is Alibaba's large language model family. The Qwen Coder models are specifically optimized for coding tasks, agentic workflows, and tool use.

**Key facts:**

- **Developer:** Alibaba Cloud
- **Coder models:** Qwen3-Coder-30B, Qwen3-Coder-Next, Qwen3.8-Coder
- **License:** Apache 2.0 for open-weight models
- **Context:** Up to 262K tokens (1M with YaRN extension)
- **Best for:** Free coding with strong agentic capabilities

---

## Is Qwen Free?

Three honest answers:

| Use Case | Free? |
|----------|-------|
| Qwen Chat (chat.qwen.ai) | Yes, free forever |
| Model Studio API (new users) | Yes, 1M free tokens |
| Self-hosted (open weights) | Free license, expensive hardware |

The web chat is free but has no API. The API gives new users **1 million free tokens** valid for 90 days. The open weights are free to download but need serious hardware to run.

---

## Free Tier Details

### Model Studio Free Quota

New Alibaba Cloud Model Studio accounts receive **1 million free tokens** (input + output combined) valid for **90 days** [citation:14][citation:16].

**Important restrictions:**

| Restriction | Details |
|-------------|---------|
| Region | Singapore (International) only [citation:16] |
| Endpoint | `dashscope-intl.aliyuncs.com` [citation:16] |
| Expiry | 90 days from activation [citation:14] |
| Coverage | Most Qwen models combined, not per-model [citation:14] |

**Warning:** If you use the Beijing or US-Virginia endpoints, you pay from the first token. The free quota only works on the Singapore endpoint [citation:16].

### After Free Quota

Once your 1M tokens are used or expire, billing kicks in automatically:

- Input: **$2 per million tokens**
- Output: **$6 per million tokens** [citation:16]

### Qwen Chat (Free Forever)

Visit `chat.qwen.ai`. No account required for basic use. No API access.

**Limitation:** Cannot be scripted or wired into your terminal agent.

---

## Setup for The Team Tools

### OpenCode

```bash
export DASHSCOPE_API_KEY=sk-xxx
opencode
/models
# Select qwen3.8-coder or similar
```

### Aider

```bash
export DASHSCOPE_API_KEY=sk-xxx
aider --model openai/qwen3.8-coder \
  --openai-api-base https://dashscope-intl.aliyuncs.com/compatible-mode/v1 \
  --openai-api-key $DASHSCOPE_API_KEY
```

### miii

miii uses Ollama by default. To use Qwen API instead, configure an OpenAI-compatible provider:

```json
{
  "model": "qwen3.8-coder",
  "provider": "openai",
  "baseUrl": "https://dashscope-intl.aliyuncs.com/compatible-mode/v1",
  "apiKey": "sk-xxx"
}
```

### Ollama (Local, Free Forever)

Qwen models are available for local use through Ollama:

```bash
# Qwen3-Coder 30B (needs ~18GB VRAM)
ollama pull qwen3-coder:30b

# Smaller option (needs ~6GB VRAM)
ollama pull qwen2.5-coder:7b
```

**Why local:** 100% private. No API keys. Unlimited use. No 90-day expiry [citation:9][citation:15].

---

## Getting an API Key

1. Go to `bailian.console.alibabacloud.com` (international) [citation:4]
2. Create an account and verify email + phone [citation:14]
3. Activate Model Studio and accept terms [citation:14]
4. Go to API Keys page and click "Create API Key" [citation:14]
5. Copy the key (starts with `sk-`) [citation:14]
6. Set as environment variable:

```bash
export DASHSCOPE_API_KEY="sk-your-key-here"
```

**Tip:** Add the export to `~/.bashrc` or `~/.zshrc` to make it permanent [citation:14].

---

## Model Comparison

| Model | Context | Best For | Local VRAM |
|-------|---------|----------|------------|
| Qwen3.8-Coder | 1M | Agentic coding, long repos | Server |
| Qwen3-Coder-Next | 262K | Local dev, CLI agents | ~44GB (3-bit) |
| Qwen3-Coder-30B | 262K | Best local balance | ~17-20GB [citation:15] |
| Qwen2.5-Coder-14B | 128K | Comfortable local coding | ~10GB |
| Qwen2.5-Coder-7B | 128K | Budget local coding | ~6GB |

**For most users:** Qwen3-Coder-30B is the sweet spot for local coding. It fits on a 24GB GPU, handles 262K context, and scores well on agentic benchmarks [citation:15].

---

## Privacy

| Route | Privacy |
|-------|---------|
| Qwen Chat | Data may be used for training |
| Model Studio free quota | Check Alibaba's terms |
| Paid API | Check Alibaba's terms |
| Self-hosted (Ollama) | 100% private |

**For sensitive code:** Use Ollama with a local Qwen model [citation:9].

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| API key not working | Verify key and check you're using Singapore endpoint |
| Free quota not applying | Check region is Singapore, not Beijing |
| 401 Unauthorized | Key may be expired or invalid |
| Rate limited | Wait or switch to local Ollama |
| `DASHSCOPE_API_KEY` not found | Add export to shell config and restart terminal |

---

## What Now?

Next: `04-providers/groq.md` for the fastest free inference available.

> **Ethical Use Only**
> Never send sensitive code to free cloud models.
> Use Ollama for private work.

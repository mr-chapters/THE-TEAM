# Gemini — Google's Free API Tier

Gemini is Google's AI model family. The API free tier is generous and requires no credit card. But there is a critical privacy catch you must understand before using it.

---

## What is Gemini?

Gemini is Google's flagship AI model family. It includes Flash-class models (fast, cheap) and Pro-class models (powerful, expensive). The API is OpenAI-compatible, which means it works with most coding agents.

**Key facts:**

- **Developer:** Google
- **Free tier:** Yes, no credit card required
- **API compatibility:** OpenAI-compatible
- **Models:** Flash (free), Pro (paid)
- **Best for:** Free prototyping and learning

---

## Is Gemini Free?

Yes, with important limits.

| Surface | Free? | Notes |
|---------|-------|-------|
| Gemini app (web/mobile) | Yes | Daily prompt caps |
| Google AI Studio | Yes | Browser-based prototyping |
| Gemini API | Yes | Rate-limited, no credit card |
| Gemini CLI | No longer free | Discontinued June 18, 2026 |

---

## Free Tier Details

### Rate Limits

Google no longer publishes static rate limit tables. You must check the live dashboard in AI Studio for your project's current numbers.

**Reported free-tier figures (as of mid-2026):**

| Limit | Value |
|-------|-------|
| Requests per minute | 10-15 |
| Requests per day | 1,500 |
| Models | Flash and Flash-Lite only |

Pro-class models moved behind billing. The free tier centers on Flash-class workhorses.

### The Critical Privacy Warning

**On the free tier, Google may use your prompts and outputs to improve its products.** Paid tiers do not.

This means:
- Do not send sensitive code
- Do not send customer data
- Do not send proprietary information
- Treat the free tier as a public sandbox

The paid API does not train on your inputs. If privacy matters, either pay or use Ollama.

### The Billing Catch

**Enabling billing on a project removes the free tier for that project entirely.** If you want free experimentation alongside a paid production key, keep them in separate Google Cloud projects.

---

## Setup for The Team Tools

### OpenCode

```bash
export GEMINI_API_KEY=AIza_xxx
opencode
/models
# Select a Gemini model
```

### Aider

```bash
export GEMINI_API_KEY=AIza_xxx
aider --model gemini/gemini-2.5-flash
```

### miii

miii uses Ollama by default. To use Gemini API instead, configure an OpenAI-compatible provider:

```json
{
  "model": "gemini-2.5-flash",
  "provider": "openai",
  "baseUrl": "https://generativelanguage.googleapis.com/v1beta/openai/",
  "apiKey": "AIza_xxx"
}
```

---

## Getting an API Key

1. Go to `aistudio.google.com`
2. Sign in with a Google account
3. Click "Get API key"
4. Create a key against a Google Cloud project
5. Copy the key (starts with `AIza`)
6. Set it:

```bash
export GEMINI_API_KEY="AIza_your-key-here"
```

**Tip:** Add the export to `~/.bashrc` or `~/.zshrc` to make it permanent.

---

## Model Comparison

| Model | Free Tier | Best For |
|-------|-----------|----------|
| gemini-2.5-flash | Yes | Fast coding, prototyping |
| gemini-2.5-flash-lite | Yes | Budget tasks |
| gemini-3.6-flash | Yes | Latest workhorse |
| gemini-2.5-pro | No | Complex reasoning |
| gemini-3-pro | No | Flagship |

Start with Flash. Move to Pro only when you need the extra capability and are willing to pay.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| API key not working | Verify key starts with `AIza`, check it's enabled |
| 429 Too Many Requests | Hit rate limit, wait for reset |
| Free tier not applying | Check billing is NOT enabled on the project |
| Model not found | Check model name, Pro models require billing |
| `GEMINI_API_KEY` not found | Restart shell after adding to config |

---

## What Now?

Next: `04-providers/ollama.md` for the fully local, private option.

> **Ethical Use Only**
> Never send sensitive code to free cloud models.
> Use Ollama for private work.

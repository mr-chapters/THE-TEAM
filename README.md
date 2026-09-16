# The Team

A free AI coding agent for your terminal. No subscriptions. No brand confusion. No lies.

---

## What is The Team?

The Team is a setup guide that helps you install a free AI coding agent in your terminal using open-source tools and free AI models.

You get:
- A real coding agent (not a chatbot)
- Free AI models (DeepSeek, Qwen, Groq, Gemini, local Ollama)
- No API keys required if you use Ollama
- No subscriptions
- No "unofficial" wrapper around someone else's product

---

## What You Actually Get

| Tool | What It Is | Free? |
|------|-----------|-------|
| OpenCode | Model-neutral terminal agent, 75+ providers | Yes [citation:12] |
| miii | Local/offline agent, runs on your GPU | Yes [citation:13] |
| Aider | Git-native coding agent | Yes [citation:4] |

| Model | Free Tier |
|-------|-----------|
| DeepSeek | Free credits on sign-up, OpenRouter free tier [citation:6][citation:15] |
| Qwen | 1M free tokens per model on Model Studio [citation:7] |
| Groq | 14,400 requests/day, no credit card [citation:8] |
| Gemini | 1,500 requests/day, free API key [citation:9] |
| Ollama | 100% local, unlimited [citation:10] |

---

## Quick Start

### Easiest: OpenCode + Free Models

```bash
# Install OpenCode
curl -fsSL https://opencode.ai/install | bash

# Configure a free model (example: DeepSeek via OpenRouter)
opencode config set provider openrouter
opencode config set model deepseek/deepseek-chat

# Start coding
opencode# THE-TEAM

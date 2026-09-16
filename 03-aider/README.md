# Aider — The Git-Native Agent

Aider is the Git-native option in The Team. Every change it makes is automatically committed to your repository, so you can review, diff, and roll back anything with standard Git commands.

---

## What is Aider?

Aider is an open-source CLI AI coding tool that lets you pair program with LLMs directly in your terminal. Its defining feature is being **Git-native** — every edit is auto-committed, giving you full version control over everything the AI does.

**Key facts:**

- **License:** Open source
- **Model support:** Virtually all major LLMs (Claude, GPT, DeepSeek, Qwen, Ollama)
- **Installation:** `pip install aider-chat`
- **Best for:** Developers who want precise control and rollback capability

---

## Why Aider for The Team?

| Reason | Why It Matters |
|--------|----------------|
| Git-native | Every change auto-committed, roll back anytime |
| Multi-model support | Works with Claude, GPT, DeepSeek, Qwen, Ollama |
| Precise file control | Only modifies files you explicitly add |
| Three chat modes | code, ask, architect for different tasks |
| Auto lint & test | Built-in verification after changes |
| Free local models | Works with Ollama for zero-cost usage |

---

## How It Compares

| Dimension | Aider | Claude Code | Gemini CLI |
|-----------|-------|-------------|------------|
| Git integration | Excellent (auto-commit) | Good (manual) | Basic |
| Model flexibility | Excellent (almost any LLM) | Limited (Anthropic only) | Limited (Google only) |
| Local model support | Yes (Ollama) | No | No |
| Cost control | High (choose cheap/free models) | Subscription required | Subscription required |

---

## Requirements

| Requirement | Details |
|-------------|---------|
| Python | 3.9 or higher |
| Git | Must be installed |
| API Key | For cloud models (DeepSeek, Groq, etc.) |
| Ollama | Optional, for free local models |

---

## Installation

### Step 1: Install Aider

```bash
python -m pip install aider-install
aider-install
```

Or directly:

```bash
pip install aider-chat
```

### Step 2: Set an API Key

Pick one provider:

```bash
# Claude (paid)
export ANTHROPIC_API_KEY=sk-xxx

# GPT (paid)
export OPENAI_API_KEY=sk-xxx

# DeepSeek (cheap)
export DEEPSEEK_API_KEY=sk-xxx

# Groq (free tier)
export GROQ_API_KEY=sk-xxx

# Gemini (free tier)
export GEMINI_API_KEY=sk-xxx
```

### Step 3: Start Coding

```bash
cd /your/project
aider
```

---

## Connecting Free Models

### DeepSeek (Cheapest Paid)

```bash
export DEEPSEEK_API_KEY=sk-xxx
aider --model deepseek/deepseek-chat
```

DeepSeek is extremely cheap — roughly $0.22 per million input tokens and $0.66 per million output tokens (off-peak).

### Groq (Free Tier)

```bash
export GROQ_API_KEY=sk-xxx
aider --model groq/llama-3.3-70b-versatile
```

Free tier: 14,400 requests/day, very fast inference.

### Gemini (Free Tier)

```bash
export GEMINI_API_KEY=sk-xxx
aider --model gemini/gemini-2.0-flash-exp
```

Free tier: 1,500 requests/day.

### Ollama (Fully Local, Free Forever)

```bash
ollama pull qwen2.5-coder:14b
aider --model ollama/qwen2.5-coder:14b
```

No API key. No cost. Everything stays on your machine.

---

## Core Workflow

### Three Chat Modes

| Mode | What It Does | How to Use |
|------|--------------|------------|
| **code** | Directly edits code | `/code Add retry decorator` |
| **ask** | Read-only, no changes | `/ask What's the time complexity?` |
| **architect** | Design first, implement later | `/architect Design a task queue system` |

### Adding Files to Context

Aider only modifies files you explicitly add:

```bash
# Add specific files
/add src/models/user.py src/api/auth.py

# Add an entire directory
/add src/services/

# Remove files you don't need
/drop src/legacy/old_auth.py
```

### Auto Git Commits

Every change gets its own commit:

```bash
git log --oneline    # View Aider's commit history
git diff HEAD~1      # See the last change
git revert HEAD      # Roll back if unhappy
```

Set a custom commit prefix:

```bash
aider --commit-prefix "[ai] "
```

### Project Configuration

Create `.aider.conf.yml` in your project root:

```yaml
model: deepseek/deepseek-chat
auto-commits: true
auto-lint: true
auto-test: true
test-cmd: pytest
lint-cmd: ruff check
```

### Lint + Test Automation

Aider can automatically run linters and tests after every change:

```yaml
auto-lint: true
lint-cmd: "ruff check --fix"
test-cmd: "pytest -x"
```

If either fails, Aider will attempt to fix the issue and retry.

---

## Advanced Tips

### Multi-Model Strategy

```bash
# Complex architecture — use the strongest model
aider --model claude-sonnet-4-5
/architect Design a microservices split plan

# Daily coding — use a cost-effective model
aider --model deepseek/deepseek-chat
/code Implement user-service according to the plan

# Code review — use a free local model
aider --model ollama/qwen2.5-coder
/ask Any issues with this code?
```

### Git Workflow Integration

```bash
# Work on a feature branch
git checkout -b feature/add-notifications
aider

# Every Aider change stays on this branch
# When done, follow your normal PR process
git push -u origin feature/add-notifications
```

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `aider: command not found` | Check Python scripts directory is in PATH |
| API key not working | Verify the environment variable name |
| Model not found | Check model ID spelling (`aider --list-models`) |
| Slow responses | Use a smaller model or Groq |
| Ollama not working | Ensure Ollama is running: `ollama list` |

---

## What Now?

Next: `04-providers/README.md` for detailed provider setup guides.

> **Ethical Use Only**
> Only use these tools for lawful purposes.

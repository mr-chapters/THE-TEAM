# Aider — Installation Guide

This guide covers every step to install Aider, from Python to your first commit.

---

## Prerequisites

| Requirement | Details |
|-------------|---------|
| **Python** | 3.9 or higher |
| **Git** | Must be installed and configured |
| **API Key** | For cloud models (DeepSeek, Groq, Gemini, etc.) |
| **Ollama** | Optional, for free local models |
| **OS** | Linux, macOS, or Windows |

---

## Step 1: Install Python

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install -y python3 python3-pip python3-venv
```

### macOS (Homebrew)

```bash
brew install python
```

### Windows

Download from `python.org` or use winget:

```powershell
winget install Python.Python.3.12
```

**Verify:**

```bash
python3 --version
pip --version
```

You should see Python 3.9 or higher.

---

## Step 2: Install Git

### Linux

```bash
sudo apt install -y git
```

### macOS

```bash
brew install git
```

### Windows

Download from `git-scm.com` or use winget:

```powershell
winget install Git.Git
```

**Configure Git:**

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

**Verify:**

```bash
git --version
```

---

## Step 3: Install Aider

### Option A: Official Installer (Recommended)

```bash
python -m pip install aider-install
aider-install
```

### Option B: Direct pip Install

```bash
python -m pip install aider-chat
```

### Option C: Using pipx (Isolated Environment)

```bash
pipx install aider-chat
```

**If you get permission errors:**

```bash
python -m pip install --user aider-chat
```

**Verify:**

```bash
aider --version
```

---

## Step 4: Get an API Key

Pick one provider. See the `04-providers/` folder for detailed setup guides.

| Provider | Cost | Environment Variable |
|----------|------|----------------------|
| DeepSeek | Very cheap | `DEEPSEEK_API_KEY` |
| Groq | Free tier | `GROQ_API_KEY` |
| Gemini | Free tier | `GEMINI_API_KEY` |
| Qwen | 1M free tokens | `DASHSCOPE_API_KEY` |
| Ollama | Free local | None needed |

**Example (DeepSeek):**

```bash
export DEEPSEEK_API_KEY="sk-your-key-here"
```

Add to your shell config to make it permanent:

```bash
echo 'export DEEPSEEK_API_KEY="sk-your-key-here"' >> ~/.bashrc
source ~/.bashrc
```

---

## Step 5: First Launch

```bash
cd /your/project
aider
```

Aider will:

1. Detect your Git repository
2. Ask which model to use (or use the one you specify)
3. Open an interactive prompt

**Try this prompt:**

```
Add a retry decorator to the fetch_data function in utils.py
```

If Aider edits the file and commits the change, setup is complete.

---

## Configuration

### Global Config File

Create `~/.aider.conf.yml`:

```yaml
model: deepseek/deepseek-chat
auto-commits: true
auto-lint: true
auto-test: true
```

### Project Config File

Create `.aider.conf.yml` in your project root:

```yaml
model: deepseek/deepseek-chat
test-cmd: pytest
lint-cmd: ruff check
```

### Full Config Options

| Option | What It Does |
|--------|--------------|
| `model` | Default model to use |
| `auto-commits` | Auto-commit every change |
| `auto-lint` | Run linter after changes |
| `auto-test` | Run tests after changes |
| `test-cmd` | Command to run tests |
| `lint-cmd` | Command to run linter |
| `commit-prefix` | Prefix for commit messages |

---

## Chat Modes

Switch modes with slash commands:

| Mode | Command | What It Does |
|------|---------|--------------|
| code | `/code` | Directly edits code |
| ask | `/ask` | Read-only, no changes |
| architect | `/architect` | Design first, implement later |

**Example:**

```bash
/architect Design a task queue system
/code Implement the design you just made
/ask What's the time complexity of this?
```

---

## Adding Files to Context

Aider only modifies files you explicitly add:

```bash
# Add specific files
/add src/models/user.py src/api/auth.py

# Add an entire directory
/add src/services/

# Remove files you don't need
/drop src/legacy/old_auth.py
```

---

## Git Workflow

### Auto Commits

Every Aider change gets its own commit:

```bash
git log --oneline    # View Aider's commits
git diff HEAD~1      # See the last change
git revert HEAD      # Roll back if unhappy
```

### Custom Commit Prefix

```bash
aider --commit-prefix "[ai] "
```

### Feature Branch Workflow

```bash
git checkout -b feature/add-notifications
aider
# Every Aider change stays on this branch
git push -u origin feature/add-notifications
```

---

## Lint + Test Automation

Aider can automatically run linters and tests after every change:

```yaml
auto-lint: true
lint-cmd: "ruff check --fix"
auto-test: true
test-cmd: "pytest -x"
```

If either fails, Aider attempts to fix the issue and retry.

---

## Verification

Run these checks:

```bash
# Python
python3 --version

# Git
git --version

# Aider
aider --version

# Test run
cd /your/project
aider --model deepseek/deepseek-chat
```

If all commands return results, installation is complete.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `aider: command not found` | Check Python scripts directory is in PATH |
| `pip install` permission denied | Use `--user` flag or pipx |
| API key not working | Verify environment variable name |
| Model not found | Check model ID spelling (`aider --list-models`) |
| Git not configured | Run `git config --global user.name` and `user.email` |
| Slow responses | Use a smaller model or Groq |
| Ollama not working | Ensure Ollama is running: `ollama list` |

---

## What Now?

Return to `03-aider/README.md` for the full workflow guide, or move to `04-providers/README.md` for provider setup.

> **Ethical Use Only**
> Only use these tools for lawful purposes.

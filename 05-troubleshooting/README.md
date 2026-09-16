
# Troubleshooting

Common problems and how to fix them. If your issue is not here, check the provider-specific guide in `04-providers/`.

---

## Installation Problems

### `command not found` after install

**Symptom:**

```bash
opencode: command not found
miii: command not found
aider: command not found
```

**Cause:** The install directory is not in your PATH.

**Fix:**

For OpenCode:

```bash
export PATH="$HOME/.opencode/bin:$PATH"
echo 'export PATH="$HOME/.opencode/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

For miii and Aider (npm global):

```bash
export PATH="$HOME/.npm-global/bin:$PATH"
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Restart your terminal after adding the line.

---

### npm permission denied

**Symptom:**

```bash
npm ERR! Error: EACCES: permission denied
```

**Cause:** npm is trying to install globally to a system directory.

**Fix:**

```bash
npm config set prefix "$HOME/.npm-global"
export PATH="$HOME/.npm-global/bin:$PATH"
npm install -g miii-agent
```

Add the export to `~/.bashrc` or `~/.zshrc` to make it permanent.

---

### pip install permission denied

**Symptom:**

```bash
ERROR: Could not install packages due to an EnvironmentError: [Errno 13] Permission denied
```

**Fix:**

Option A — install to user directory:

```bash
python -m pip install --user aider-chat
```

Option B — use pipx:

```bash
pipx install aider-chat
```

Option C — use a virtual environment:

```bash
python3 -m venv ~/aider-env
source ~/aider-env/bin/activate
pip install aider-chat
```

---

### Node version too old

**Symptom:**

```bash
error: miii-agent requires Node.js 18 or higher
```

**Fix:**

Check your version:

```bash
node --version
```

If lower than 18, upgrade:

**Ubuntu/Debian:**

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

**macOS:**

```bash
brew upgrade node
```

**Windows:** Download the latest LTS from `nodejs.org`.

---

## Model Connection Problems

### Model not found

**Symptom:**

```bash
Error: model "deepseek-chat" not found
```

**Cause:** The model ID is misspelled, or the provider is not configured.

**Fix:**

For Aider:

```bash
aider --list-models
```

For OpenCode:

```bash
/models
```

Check the exact model ID in the provider's guide in `04-providers/`.

---

### 401 Unauthorized

**Symptom:**

```bash
Error: 401 Unauthorized
```

**Cause:** API key is wrong, expired, or missing.

**Fix:**

1. Verify the key is set:

```bash
echo $DEEPSEEK_API_KEY
echo $GROQ_API_KEY
echo $GEMINI_API_KEY
```

2. If empty, set it:

```bash
export DEEPSEEK_API_KEY="sk-your-key"
```

3. If still failing, regenerate the key on the provider dashboard.

---

### 402 Payment Required

**Symptom:**

```bash
Error: 402 Payment Required
```

**Cause:** Your provider balance is empty.

**Fix:**

- DeepSeek: Top up at `platform.deepseek.com`
- OpenAI: Add credit at `platform.openai.com`
- Anthropic: Add credit at `console.anthropic.com`

For free alternatives, switch to Groq, Gemini, or Ollama.

---

### 429 Too Many Requests

**Symptom:**

```bash
Error: 429 Too Many Requests
```

**Cause:** You hit the rate limit for your provider.

**Fix:**

1. Wait for the limit to reset (usually 1 minute)
2. Switch to another model with `/models`
3. Switch to another provider
4. Use Ollama for unlimited local use

**Rate limit reference:**

| Provider | Free Limit |
|----------|------------|
| OpenRouter | 50 requests/day |
| Groq | 30 requests/minute |
| Gemini | 10-15 requests/minute |
| Qwen | 1M tokens (90 days) |

---

### Ollama connection refused

**Symptom:**

```bash
Error: connection refused to http://localhost:11434
```

**Cause:** Ollama is not running.

**Fix:**

**Linux:**

```bash
sudo systemctl start ollama
sudo systemctl enable ollama
```

**macOS:** Ollama runs automatically after install. If not, open the Ollama app.

**Windows:** Open the Ollama app from the Start menu.

**Verify:**

```bash
curl http://localhost:11434
```

If you see "Ollama is running", the service is up.

---

## Performance Problems

### Slow responses

**Symptom:** The agent takes 30+ seconds to respond.

**Cause:** Model is too large for your hardware, or the cloud provider is overloaded.

**Fix:**

For local models:

```bash
ollama ps
```

Check the PROCESSOR column. If it shows CPU, your model does not fit on your GPU. Use a smaller model:

| VRAM | Use Instead |
|------|-------------|
| 6 GB | qwen2.5-coder:7b |
| 10 GB | qwen2.5-coder:14b |
| 24 GB | qwen3-coder:30b |

For cloud models, switch to Groq for fastest inference.

---

### Context truncated / model forgets files

**Symptom:** The model answers confidently about a file it cannot see.

**Cause:** Ollama's default context length is too small (4,096 tokens). The agent's system prompt and tool definitions already exceed that.

**Fix:**

```bash
sudo systemctl edit ollama.service
```

Add:

```
[Service]
Environment="OLLAMA_CONTEXT_LENGTH=64000"
Environment="OLLAMA_KEEP_ALIVE=-1"
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

### Model unloads between requests

**Symptom:** Every request reloads tens of gigabytes of model weights.

**Cause:** Ollama unloads models 5 minutes after the last request by default.

**Fix:**

```
[Service]
Environment="OLLAMA_KEEP_ALIVE=-1"
```

`-1` keeps the model loaded indefinitely.

---

## Agent-Specific Problems

### Aider modifies files I did not add

**Cause:** Files were added with `/add` earlier and never removed.

**Fix:**

```bash
/drop src/unwanted/file.py
```

List currently added files with `/ls`.

---

### Aider commits too often

**Cause:** Auto-commit is enabled by default.

**Fix:**

Disable auto-commit:

```bash
aider --no-auto-commits
```

Or set in config:

```yaml
auto-commits: false
```

---

### OpenCode does not see my project files

**Cause:** You are running OpenCode in the wrong directory.

**Fix:**

```bash
cd /path/to/your/project
opencode
```

Or use `@` to fuzzy-search files:

```
❯ review the auth logic in @src/auth/middleware.ts
```

---

### miii permission errors

**Symptom:** miii asks for permission every time it edits a file.

**Cause:** You are in normal mode.

**Fix:**

Cycle permission mode with `shift+tab`:

| Mode | What It Does |
|------|--------------|
| normal | Asks before writing |
| plan mode | Read-only |
| auto-accept edits | Writes without asking |
| bypass permissions | Runs everything (sandbox only) |

---

## Git Problems

### Git not configured

**Symptom:**

```bash
*** Please tell me who you are.
```

**Fix:**

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

---

### Git not initialized

**Symptom:**

```bash
Error: not a git repository
```

**Fix:**

```bash
git init
git add .
git commit -m "Initial commit"
```

Aider requires a Git repository. OpenCode and miii work without one.

---

### Roll back an Aider change

**Fix:**

```bash
git log --oneline    # Find the commit
git revert <hash>    # Revert it
```

Or:

```bash
git reset --hard HEAD~1
```

---

## Provider-Specific Issues

| Provider | Common Issue | Fix |
|----------|--------------|-----|
| DeepSeek | 402 Payment Required | Top up balance |
| Qwen | Free quota not applying | Use Singapore endpoint |
| Groq | 429 Too Many Requests | Wait 1 minute |
| Gemini | Free tier removed | Check billing is OFF |
| Ollama | Context truncated | Set `OLLAMA_CONTEXT_LENGTH` |

See `04-providers/` for full provider guides.

---

## Still Stuck?

1. Check the provider guide in `04-providers/`
2. Check the agent guide in `01-opencode/`, `02-miii/`, or `03-aider/`
3. Search the error message online
4. Ask in the community

---

> **Ethical Use Only**
> Only use these tools for lawful purposes.

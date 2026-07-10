# DeepSeek API + Claude Code in VS Code

Use the Claude Code VS Code extension with DeepSeek API — no Anthropic account needed.

![Shortest setup flow](images/image-1.png)

## tl;dr

Don't click the three login buttons. Enable **Disable Login Prompt**, then configure `~/.claude/settings.json`.

![How to handle the login screen](images/image-2.png)

---

## 1. VS Code Extension Setting

Open VS Code Settings: **Ctrl + ,** (Mac: **Cmd + ,**).

Search `Claude Code login`, then enable **Disable Login Prompt**.

```json
"claudeCode.disableLoginPrompt": true
```

## 2. Create Shared Settings

**Linux / Mac:**

```bash
mkdir -p ~/.claude
nano ~/.claude/settings.json
```

**Windows:** `C:\Users\<username>\.claude\settings.json`

## 3. Configuration Template

Replace `<your DeepSeek API Key>` with your real key:

```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",
  "env": {
    "ANTHROPIC_BASE_URL": "https://api.deepseek.com/anthropic",
    "ANTHROPIC_AUTH_TOKEN": "<your DeepSeek API Key>",
    "ANTHROPIC_MODEL": "deepseek-v4-pro[1m]",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "deepseek-v4-pro[1m]",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "deepseek-v4-pro[1m]",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "deepseek-v4-flash",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "CLAUDE_CODE_EFFORT_LEVEL": "max",
    "CLAUDE_CODE_SUBAGENT_MODEL": "deepseek-v4-flash"
  }
}
```

> ⚠️ Do not commit this file to Git — it contains your API key.

## 4. Reload and Start

- **Ctrl + Shift + P** → `Developer: Reload Window`
- Click the Claude Code icon in the sidebar → **New session**

![Claude Code New Session](images/image-3.png)

## Terminal Fallback

If the extension doesn't work, use the CLI directly:

```bash
npm install -g @anthropic-ai/claude-code
claude --version

cd /path/to/my-project
claude
```

## Quick Troubleshooting

| Problem | Check | Fix |
|---|---|---|
| Still shows login page | `disableLoginPrompt` isn't `true` | Reload window, confirm VS Code settings |
| API key error | `ANTHROPIC_AUTH_TOKEN` | Re-copy your DeepSeek API key |
| New session unresponsive | CLI might not work either | Run `claude` in terminal first to verify |

## Sources

- [DeepSeek API Docs — Integrate with Claude Code](https://api-docs.deepseek.com/guides/claude_code)
- [awesome-deepseek-agent — claude_code.md](https://github.com/deepseek-ai/awesome-deepseek-agent/blob/main/claude_code.md)
- [Claude Code Docs — Use in VS Code](https://docs.anthropic.com/en/docs/claude-code/ide-integrations#vs-code)

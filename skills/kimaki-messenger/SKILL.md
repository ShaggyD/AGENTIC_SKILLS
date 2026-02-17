---
name: kimaki-messenger
description: Send prompts and manage sessions via Kimaki CLI for Discord
license: MIT
compatibility: opencode
metadata:
  audience: developers
  workflow: automation
  platform: any
  requires: kimaki
---

## What I do

Send prompts to Discord channels, create sessions, manage threads, and trigger AI-powered workflows using the Kimaki CLI.

## When to use me

- Send prompts to Discord channels programmatically
- Create new AI sessions/threads
- Continue existing sessions
- Upload files to sessions
- Set up automated prompts (paired with **macos-task-scheduler**)

## Installation

```bash
# Run via npx (no install needed)
npx -y kimaki@latest [command]

# Or install globally
npm install -g kimaki
```

## Related Skill

For scheduling recurring tasks on macOS, see: **macos-task-scheduler**

---

## Send Command (Most Used)

### Basic usage

```bash
# Send prompt to channel (creates new thread)
npx -y kimaki@latest send --channel CHANNEL_ID --prompt "Your prompt"

# Continue existing thread
npx -y kimaki@latest send --thread THREAD_ID --prompt "Follow-up"

# Continue existing session
npx -y kimaki@latest send --session SESSION_ID --prompt "Prompt"
```

### Options

| Option | Description |
|--------|-------------|
| `-c, --channel` | Discord channel ID |
| `-p, --prompt` | Message/prompt content |
| `-d, --project` | Project directory |
| `-n, --name` | Thread name (optional) |
| `--thread` | Continue existing thread |
| `--session` | Continue existing session |
| `--notify-only` | Create notification thread without starting AI session |
| `--wait` | Wait for completion |
| `--worktree` | Create git worktree |
| `--model` | Specify model (format: provider/model) |
| `--agent` | Specify agent type |

### Notify-Only Mode

Use `--notify-only` to create a notification thread without starting an AI session. Useful for scheduled tasks:

```bash
npx -y kimaki@latest send --channel CHANNEL_ID --prompt "Daily brief ready" --notify-only
```

The user replies to the thread when ready to run the task.

---

## Session Management

### List sessions

```bash
npx -y kimaki@latest session list
npx -y kimaki@latest session list --project /path/to/project
npx -y kimaki@latest session list --json
```

### Read session

```bash
npx -y kimaki@latest session read SESSION_ID
```

### Upload files

```bash
npx -y kimaki@latest upload-to-discord file1.md --session SESSION_ID
```

---

## Tunnel (Dev Servers)

```bash
npx -y kimaki@latest tunnel --port 3000
npx -y kimaki@latest tunnel --port 3000 --tunnel-id my-app
```

---

## Projects

```bash
npx -y kimaki@latest project list
npx -y kimaki@latest project list --json
```

---

## Upgrade

```bash
npx -y kimaki@latest upgrade
```

---

## Examples with Models

```bash
# Default model
npx -y kimaki@latest send --channel 123 --prompt "Hello"

# Specific model
npx -y kimaki@latest send --channel 123 --prompt "Hello" --model anthropic/claude-3-5-sonnet-20241022

# With worktree
npx -y kimaki@latest send --channel 123 --prompt "Add feature" --worktree my-feature

# Wait for response
npx -y kimaki@latest send --channel 123 --prompt "Run tests" --wait
```

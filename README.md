# Kimaki Skills for macOS

OpenCode skills for scheduling AI-powered tasks on macOS using Kimaki.

## Skills

### macos-task-scheduler

Create macOS launchd scheduled tasks that trigger Kimaki/OpenCode sessions in Discord.

- Schedule AI tasks (daily digests, health checks, backups)
- Uses `--notify-only` to create notification threads you can reply to
- Handles macOS launchd environment quirks

## Usage

Copy a skill to your OpenCode skills directory:

```bash
# Project-local
cp -r skills/macos-task-scheduler ~/.config/opencode/skills/

# Or Claude-compatible
cp -r skills/macos-task-scheduler ~/.claude/skills/
```

Then use in OpenCode:
```
skill({ name: "macos-task-scheduler" })
```

## Requirements

- macOS (uses launchd)
- Kimaki Discord bot
- Node.js (via npx)

## Creating New Skills

See each skill's `SKILL.md` for detailed documentation.

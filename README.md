# Agentic Skills

CLI tools and utilities for autonomous agents. Skills define domain-specific knowledge for agents like [OpenCode](https://github.com/opencode-ai/opencode) to perform tasks.

## Skills

### gog
[Google Workspace CLI](https://gogcli.sh) for Gmail, Calendar, Drive, Contacts, Sheets, and Docs.

### kimaki-messenger
[Kimaki](https://github.com/remorses/kimaki) - Send prompts to Discord channels to control OpenCode agents.

### macos-task-scheduler
Schedule recurring tasks on macOS using launchd plists.

## Usage

Copy a skill to your OpenCode skills directory:

```bash
# Project-local
cp -r skills/gog ~/.config/opencode/skills/

# Or Claude-compatible
cp -r skills/gog ~/.claude/skills/
```

Then use in OpenCode:
```
skill({ name: "gog" })
```

## Creating New Skills

Each skill is a directory containing a `SKILL.md` file with:
- Frontmatter metadata (name, description, install instructions)
- Usage examples and commands
- Tips and gotchas

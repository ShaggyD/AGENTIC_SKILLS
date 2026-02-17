# Agentic Skills

Domain-specific knowledge for autonomous agents. Each skill gives an agent like [OpenCode](https://github.com/opencode-ai/opencode) the context and commands it needs to work with external tools.

## Why Skills?

Agents are powerful but need domain knowledge to be useful. Skills provide:
- Tool installation and setup instructions
- Common command patterns with examples
- Tips, gotchas, and environment variables
- Cross-references to related skills

## Skills

| Skill | Description |
|-------|-------------|
| [gog](skills/gog) | Google Workspace CLI - Gmail, Calendar, Drive, Contacts, Sheets, Docs |
| [kimaki-messenger](skills/kimaki-messenger) | Discord bot to control OpenCode agents remotely |
| [macos-task-scheduler](skills/macos-task-scheduler) | Schedule recurring tasks via macOS launchd |

## Quick Start

### Copy a skill

```bash
# To your project
cp -r skills/gog ~/.config/opencode/skills/

# Or globally (Claude-compatible)
cp -r skills/gog ~/.claude/skills/
```

### Use in conversation

```
@agent Use the gog skill to search my inbox for unread emails from this week
```

Or programmatically:
```
skill({ name: "gog" })
```

## Creating a New Skill

```
skills/
└── my-skill/
    └── SKILL.md
```

### SKILL.md format

```markdown
---
name: my-skill
description: What the tool does
metadata:
  install:
    - kind: brew
      formula: mytool/tap/formula
      bins: [mytool]
---

## What I do

Brief description of what this skill enables.

## Installation

```bash
brew install mytool/tap/formula
```

## Common Commands

### Do something
```bash
mytool do thing --option value
```

## Tips
- First tip
- Second tip
```

## Related

- [OpenCode](https://github.com/opencode-ai/opencode) - AI coding agent
- [Kimaki](https://github.com/remorses/kimaki) - Run OpenCode from Discord

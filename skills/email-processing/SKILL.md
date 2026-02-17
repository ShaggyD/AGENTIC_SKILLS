---
name: email-processing
description: Gmail inbox automation with pattern rules, AI triage, and Discord notifications
license: MIT
compatibility: opencode
metadata:
  audience: developers
  workflow: automation
  platform: macos, linux
  homepage: https://github.com/opencode-ai/opencode
  depends_on:
    - gog
    - kimaki
---

## What I do

Automate Gmail inbox triage with rule-based patterns and AI fallback. It labels, archives, keeps, or escalates emails and can notify the user on Discord.

## Core files

- `emails/check-emails.sh` - hourly processor
- `emails/email-patterns.json` - sender/subject rules and settings
- `emails/check.log` - run log
- `emails/last-run.txt` - last successful run epoch
- `emails/processed.json` - last 24 hours of processed decisions

## Workflow

1. Skip quiet hours
2. Search inbox using `after:<last_run_epoch>` or a quiet-hours catch-up window
3. Apply rules from `email-patterns.json`
4. If no rule matches, ask AI for a decision
5. Apply action (keep, archive, label)
6. Notify on Discord if needed
7. Record decision in `processed.json`

## Settings

`email-patterns.json` contains:

```json
{
  "settings": {
    "check_interval_hours": 1,
    "quiet_hours_start": "22:00",
    "quiet_hours_end": "08:00",
    "max_emails_per_run": 20
  }
}
```

## Pattern rules

Each rule supports:

```json
{
  "sender": "example.com",
  "subject_match": "receipt|order",
  "action": "label|archive|keep|escalate",
  "label": "Orders/example.com",
  "subject_label": "Orders/example.com",
  "notify_user": true,
  "reason": "Short explanation"
}
```

If `notify_user` is true, a Discord message is sent when the pattern matches.

## AI triage

When no pattern matches, the script calls the AI with a strict JSON response format:

```json
{"action": "keep|archive|label", "label": "label_name", "notify_user": true/false, "message": "short explanation"}
```

Blank or invalid responses are normalized to safe defaults.

## Processed log

`emails/processed.json` keeps the last 24 hours of decisions:

```json
{
  "id": "gmail_message_id",
  "from": "Sender Name <sender@example.com>",
  "subject": "Email subject",
  "action": "keep|archive|label",
  "label": "label_name",
  "notify": "true|false",
  "ai_used": "true|false",
  "message": "short note",
  "processed_at": "2026-02-17T08:00:03-07:00"
}
```

## Common commands

```bash
# Run the check manually
./emails/check-emails.sh

# List inbox matches (gog)
gog gmail search "newer_than:24h in:inbox" --max 20
```

## Tips

- Use `after:<epoch>` for catch-up across quiet hours.
- Keep patterns specific to avoid mislabeling.
- Log decisions to debug missed notifications.
- Add explicit `notify_user` for high-signal senders.

---
name: opencode-analyzer
description: Analyze OpenCode token usage and estimate costs on OpenRouter
metadata:
  install:
    - kind: manual
      bins: [opencode-cost]
---

# opencode-analyzer

OpenCode cost analyzer with detailed daily/weekly/monthly breakdowns. Shows what you actually spent vs what it would cost on OpenRouter.

## What It Does

Queries your local OpenCode SQLite database to show:
- Daily, weekly, and monthly spending
- Average costs per day/week/month
- Cost projections
- Top models by spending
- OpenRouter cost equivalents for free models

## Installation

```bash
# Copy to your skills directory
cp -r skills/opencode-analyzer ~/.config/opencode/skills/

# Or create symlink to command
ln -s ~/.config/opencode/skills/opencode-analyzer/opencode-cost ~/.local/bin/opencode-cost
```

Optional plugin sources are stored in `skills/opencode-analyzer/plugins/`.

## Plugin behavior (optional)

When enabled in a compatible OpenCode runtime, the plugin layer is intended to:

- Surface quick spend context inside OpenCode (today, yesterday, 7d, 30d)
- Use actual costs for paid usage and OpenRouter estimates for free-model usage
- Show rolling averages and a short top-model cost list

If your runtime does not expose plugin sidebar UI, use the command path (`opencode-cost` and `/cost-report`), which is the primary supported workflow for this skill.

## Usage

```bash
# Show complete cost breakdown
opencode-cost
```

## What It Shows

```
💰 OPENCODE COST BREAKDOWN

📅 SPENDING BY PERIOD
────────────────────────────────────────────────────────────
Today:                         $3.80
Yesterday:                     $2.19
Last 7 Days:                  $16.68
Last 30 Days:                 $16.89
All Time:                      $81.83

📊 AVERAGES
────────────────────────────────────────────────────────────
Daily Average (30d):           $0.60
Weekly Average (30d):          $4.20
Monthly Average (30d):        $18.17
Daily Avg (active):            $3.07

🔮 PROJECTION
────────────────────────────────────────────────────────────
Projected (7d run-rate):     $107.70

📈 ACTIVITY
────────────────────────────────────────────────────────────
Active Days (Week):                  5
Active Days (Month):                 6
Total Active Days:                  27
Calendar Span Days:               104

🔥 TOP MODELS (Last 30 Days)
────────────────────────────────────────────────────────────
MODEL                              COST % OF TOTAL
kimi-k2.5-free                   $7.26      40.0%
gpt-5.3-codex                    $5.14      30.0%
moonshotai/kimi-k2.5             $1.58       9.0%
```

## Sections Explained

### 📅 Spending by Period
- **Today**: Current day's spending
- **Yesterday**: Previous day's spending  
- **Last 7 Days**: Week total
- **Last 30 Days**: Month total
- **All Time**: Complete history

### 📊 Averages
- **Daily/Weekly/Monthly (30d)**: Rolling averages based on the last 30 calendar days
- **Daily Avg (active)**: Average per active day across all-time usage

### 🔮 Projection
- **Projected (7d run-rate)**: Based on last 7 days active-day run rate × 30

### 📈 Activity
- Active days plus total calendar span since first usage

### 🔥 Top Models
- Most expensive models (by cost, not tokens)
- Shows cost and percentage of monthly total

## Cost Calculation

**Paid models**: Uses actual cost from OpenCode  
**Free models**: Uses OpenRouter pricing:

| Model | Input | Output |
|-------|-------|--------|
| GLM 4.6 | $0.30/M | $2.55/M |
| Kimi K2.5 | $0.50/M | $2.40/M |
| Gemini 2.5 Flash | $0.30/M | $2.50/M |
| GPT-5.3 Codex | $1.25/M | $10.00/M |
| MiniMax M2.5 | $0.15/M | $0.60/M |
| Claude Opus | $5.00/M | $25.00/M |
| Qwen | $0.40/M | $2.40/M |

## Database Location

Auto-detects from:
- `~/.local/share/opencode/opencode.db` (default)
- `~/Library/Application Support/opencode/opencode.db` (macOS)

## Requirements

- sqlite3 (usually pre-installed)
- bc (for calculations, usually pre-installed)

## Examples

```bash
# Default breakdown
opencode-cost

# Use specific database
opencode-cost --db /path/to/opencode.db
```

## Troubleshooting

### Database not found
```bash
# Find your database
find ~ -name "opencode.db" 2>/dev/null

# Specify path
opencode-cost --db /path/to/opencode.db
```

### Permission denied
```bash
chmod 644 ~/.local/share/opencode/opencode.db
```

### sqlite3 not found
```bash
# macOS
brew install sqlite

# Ubuntu/Debian
sudo apt-get install sqlite3
```

## Notes

- Negative values (refunds/adjustments) are excluded
- Free models show OpenRouter equivalent cost
- Projections based on recent 7-day average
- Only counts days you actually used OpenCode

## Related

- [OpenCode](https://github.com/opencode-ai/opencode) - AI coding agent
- [OpenRouter](https://openrouter.ai) - Unified API for LLMs

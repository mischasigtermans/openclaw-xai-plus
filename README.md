# OpenClaw xAI Plus

Packed xAI skill for [OpenClaw](https://openclaw.ai). Search X and the web, chat with vision, and analyze X content patterns.

The most complete xAI integration: combines search (X + web), chat (text + vision), and X-specific analysis (voice patterns, trend research, post safety checks).

## Installation

### Via OpenClaw Bot (Easiest)

Just ask your OpenClaw bot to install xai-plus and it will handle it for you.

### Via ClawHub

xAI Plus is [available on ClawHub](https://clawhub.ai/mischasigtermans/xai-plus). Install using your preferred package manager:

```bash
# npm
npx clawhub@latest install xai-plus

# pnpm
pnpm dlx clawhub@latest install xai-plus

# bun
bunx clawhub@latest install xai-plus
```

### Manual Installation

Download the [latest release](https://github.com/mischasigtermans/openclaw-xai-plus/releases), and optionally verify the checksum:

```bash
sha256sum -c xai-openclaw.zip.sha256
```

Extract the zip file to your OpenClaw skills directory.

## Configuration

Get your API key from [console.x.ai](https://console.x.ai).

```bash
# Via clawdbot config (recommended)
clawdbot config set skills.entries.xai-plus.apiKey "xai-YOUR-KEY"

# Or environment variable
export XAI_API_KEY="xai-YOUR-KEY"
```

**Optional:** Set default model (defaults to `grok-4-1-fast`)

```bash
# Via config
clawdbot config set skills.entries.xai-plus.model "grok-3"

# Or environment variable
export XAI_MODEL="grok-3"
```

## Quick Start

### Search X

```bash
# Recent discussions
node skills/xai-plus/scripts/grok_search.mjs "Claude AI" --x --days 7

# Specific accounts
node skills/xai-plus/scripts/grok_search.mjs "launch" --x --handles AnthropicAI,OpenAI

# Date range
node skills/xai-plus/scripts/grok_search.mjs "AI agents" --x --from 2026-01-01 --to 2026-01-31
```

### Search Web

```bash
node skills/xai-plus/scripts/grok_search.mjs "TypeScript 5.7 features" --web
```

### Chat

```bash
# Text
node skills/xai-plus/scripts/chat.mjs "What is quantum computing?"

# Vision
node skills/xai-plus/scripts/chat.mjs --image screenshot.png "Describe this"
```

### Analyze

```bash
# Voice patterns
node skills/xai-plus/scripts/analyze.mjs voice @username

# Trend research
node skills/xai-plus/scripts/analyze.mjs trends "AI agents"

# Post safety check
node skills/xai-plus/scripts/analyze.mjs post "Your draft post text"
```

## Features

### Search with Filters

**X Search:**
- Date ranges (--days N, --from/--to)
- Handle filters (--handles, --exclude)
- JSON output (agent-friendly)
- Citation deduplication

**Web Search:**
- Current information via Grok
- Structured results
- Citations included

### Multi-Modal Chat

**Text:**
- Ask Grok anything
- Model selection
- Streaming responses

**Vision:**
- Image analysis
- Multiple images
- Supports JPG, PNG, WebP, GIF

### X Content Analysis (New)

**Voice Analysis:**
- Tone, personality, perspective
- Sentence structure and vocabulary
- Formatting quirks and phrases
- Best posts and anti-patterns
- 30+ days of post history

**Trend Research:**
- Current discussions and patterns
- Multiple perspectives
- Key accounts and hashtags
- Posting angles with hooks
- Target audience identification

**Post Safety Check:**
- AI detection score (0-10)
- Platform flag risk (0-10)
- Quality score (0-10)
- Specific signals detected
- Actionable suggestions

Based on real X algorithm data:
- Engagement weights (Reply: 13-27x, Block: -148x)
- Author diversity penalty patterns
- Spam detection triggers
- Volume limits and timing

## Models

| Model | Speed | Quality | Vision | Use Case |
|-------|-------|---------|--------|----------|
| grok-4-1-fast | Fast | Good | No | Default |
| grok-4-fast | Fast | Good | No | Alternative |
| grok-3 | Slower | Best | No | Complex reasoning |
| grok-2-vision-1212 | Medium | Good | Yes | Image analysis |

```bash
# List available models
node skills/xai-plus/scripts/models.mjs
```

## Output Formats

All tools support JSON output for agent/script consumption:

```bash
# JSON (agent-friendly)
node scripts/grok_search.mjs "query" --x --json

# Links only
node scripts/grok_search.mjs "query" --x --links-only

# Human-readable
node scripts/grok_search.mjs "query" --x --text
```

## Content Writing Workflow

Use these tools together to improve your X posts:

```bash
# Research before writing
node skills/xai-plus/scripts/analyze.mjs trends "your topic"
node skills/xai-plus/scripts/grok_search.mjs "your topic" --x --days 7

# Study voice patterns
node skills/xai-plus/scripts/analyze.mjs voice @your_account

# Check draft before posting
node skills/xai-plus/scripts/analyze.mjs post "$(cat draft.txt)"
```

Use the JSON output to:
- Research current discussions and posting angles
- Learn from successful voices in your niche
- Catch AI signals and platform flags before publishing

## Documentation

Comprehensive reference documentation included:

- **[SKILL.md](SKILL.md)** - Complete usage guide
- **[API Reference](references/api-reference.md)** - xAI API endpoints
- **[Search Patterns](references/search-patterns.md)** - Query optimization
- **[Models](references/models.md)** - Model comparison
- **[Analysis Prompts](references/analysis-prompts.md)** - Scoring criteria
- **[X Algorithm](references/x-algorithm.md)** - Ranking and engagement

## Why this xAI skill over the others?

Combines the best of existing xAI skills plus new capabilities:

| Feature | xai-1.1.0 | xai-search-1.0.4 | grok-search-0.2.1 | xai-plus-2.0.2 |
|---------|-----------|------------------|-------------------|----------------|
| X Search | Basic | Yes | Yes | Yes + filters  |
| Web Search | No | Yes | Yes | Yes            |
| Chat | Yes | No | Yes | Yes            |
| Vision | Yes | No | Yes | Yes            |
| Voice Analysis | No | No | No | **Yes**        |
| Trend Research | No | No | No | **Yes**        |
| Post Safety | No | No | No | **Yes**        |
| X Algorithm Data | No | No | No | **Yes**        |
| Rich Docs | No | No | Minimal | **Yes**        |
| JSON Output | No | Partial | Yes | Yes            |
| Node-only | Yes | No | Yes | Yes            |

## Examples

### Research Workflow

```bash
# 1. Find recent discussions
node scripts/grok_search.mjs "Claude Sonnet 4.5" --x --days 3

# 2. Get trend analysis
node scripts/analyze.mjs trends "Claude Sonnet 4.5"

# 3. Study key voices
node scripts/analyze.mjs voice @AnthropicAI

# 4. Web background
node scripts/grok_search.mjs "Claude Sonnet 4.5 features" --web
```

### Pre-Publish Check

```bash
# 1. Draft your post
cat > draft.txt

# 2. Check for issues
node scripts/analyze.mjs post "$(cat draft.txt)" --json

# 3. Review scores
# - AI detection: <5 (human-like)
# - Platform risk: <5 (safe)
# - Quality: >6 (good)

# 4. Apply suggestions
# Edit draft based on output

# 5. Verify fixes
node scripts/analyze.mjs post "$(cat draft.txt)"
```

### Voice Study

```bash
# 1. Analyze target account
node scripts/analyze.mjs voice @target_account --days 60 > voice.json

# 2. Extract patterns
jq '.patterns' voice.json

# 3. Study best posts
jq '.best_posts[] | {url, why}' voice.json

# 4. Note anti-patterns
jq '.anti_patterns' voice.json
```

## Troubleshooting

**Missing API key:**
```
Missing XAI_API_KEY
```
→ Set `XAI_API_KEY` environment variable or add to `~/.clawdbot/clawdbot.json`

**No results from search:**
- Try broader query or longer date range
- Check if handles exist and are public
- Remove overly restrictive filters

**Rate limits:**
- Space requests over time
- Use appropriate models (fast vs quality)
- Consider upgrading xAI plan

## Requirements

- Node.js (for scripts)
- xAI API key from [console.x.ai](https://console.x.ai)

## Credits

- [Mischa Sigtermans](https://github.com/mischasigtermans)
- Built on xAI's Grok API
- X algorithm analysis data

## License

MIT

<p align="center">
  <img src="assets/banner.svg" alt="Lockstep — Your AI Prioritization Coach" width="800"/>
</p>

<p align="center">
  <strong>Fewer goals. Deeper focus. Real results.</strong>
</p>

<p align="center">
  <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
  <a href="https://www.python.org/downloads/"><img src="https://img.shields.io/badge/python-3.11+-blue.svg" alt="Python 3.11+"></a>
</p>

---

## What is Lockstep?

Lockstep is an AI prioritization coach that lives in your Telegram. It's not a to-do list. It's not a productivity app. It's the coach who does the hard thing you can't do for yourself: **say no, cut ruthlessly, and force clarity on what actually matters.**

People overcommit. They spread thin across too many goals, get shallow results on everything, and feel guilty about what they didn't finish. Lockstep breaks that cycle.

## How It Works

Lockstep is **active, not passive**. It doesn't wait for you to remember your goals — it reaches out throughout the day.

```
Morning    Your coach messages with today's 1-2 priorities + reasoning.
           Names what to skip today and why.

Midday     Brief check-in on progress.
           "How's the system design chapter going?"

Evening    Asks for the outcome — done, partial, skipped?
           Records the result, previews tomorrow.

Weekly     Sunday review — completion data, pattern analysis,
           goal adjustments, next week's plan.
```

You can also message anytime:
```
You: I got pulled into a meeting, can't finish today
Bot: No problem. I've noted "meeting conflict" for today.
     Tomorrow morning I'll reprioritize. Rest up.
```

## Quick Start

### Prerequisites

- **Python 3.11+** — [Download](https://www.python.org/downloads/)
- **Claude Code CLI** — [Install](https://claude.ai/code) and run `claude login`
- **Telegram Bot Token** — Get one from [@BotFather](https://t.me/botfather)

### Install

```bash
git clone https://github.com/gx-ai-architect/lockstep.git
cd lockstep
make dev
```

### Configure

```bash
cp .env.example .env
```

**Required settings:**
```bash
TELEGRAM_BOT_TOKEN=...              # From @BotFather
TELEGRAM_BOT_USERNAME=lockstep_bot  # Your bot's username
APPROVED_DIRECTORY=/path/to/workdir # Working directory for the bot
ALLOWED_USERS=123456789             # Your Telegram user ID
ENABLE_SCHEDULER=true               # Enables proactive check-ins
NOTIFICATION_CHAT_IDS=123456789     # Your chat ID for scheduled messages
AGENT_CLAUDE_MD_PATH=config/agent.claude.md
LOAD_PROJECT_CLAUDE_MD=false
```

> **Finding your Telegram user ID:** Message [@userinfobot](https://t.me/userinfobot) on Telegram.

### Run

```bash
make run
```

Message your bot on Telegram. Lockstep will start the onboarding conversation — a 10-15 minute chat to understand your goals and what drives you.

## Commands

| Command | Description |
|---------|-------------|
| `/start` | Begin or resume your coaching session |
| `/new` | Start a fresh conversation |
| `/status` | View your current session info |
| `/verbose 0\|1\|2` | Control output verbosity |

## Configuration

| Setting | Default | Description |
|---------|---------|-------------|
| `AGENTIC_MODE` | `true` | Must be true for Lockstep |
| `ENABLE_SCHEDULER` | `false` | Enable for proactive check-ins |
| `NOTIFICATION_CHAT_IDS` | — | Chat IDs for scheduled messages |
| `VERBOSE_LEVEL` | `1` | 0=quiet, 1=normal, 2=detailed |
| `ENABLE_VOICE_MESSAGES` | `true` | Voice message transcription |
| `VOICE_PROVIDER` | `mistral` | `mistral` or `openai` |

Voice transcription requires extras: `pip install "lockstep-bot[voice]"`

See [docs/configuration.md](docs/configuration.md) for the full reference.

## Architecture

Lockstep is built on [claude-code-telegram](https://github.com/gx-ai-architect/claude-code-telegram), which provides the Claude Code integration, Telegram infrastructure, and scheduler. On top of that, Lockstep adds:

- **Agent personality** (`config/agent.claude.md`) — coaching philosophy and daily rhythm
- **User profile** (`profiles/user.md`) — values, decision framework, and behavioral patterns
- **Goal tracking CLI** (`src/lockstep/`) — structured goal and outcome storage in SQLite
- **Check-in scheduler** — proactive morning/midday/evening messages + weekly review

See [config/architecture.md](config/architecture.md) for the full technical design.

## Development

```bash
make dev           # Install all dependencies
make test          # Run tests with coverage
make lint          # Black + isort + flake8 + mypy
make format        # Auto-format code
make run-debug     # Run with debug logging
```

## License

MIT License — see [LICENSE](LICENSE).

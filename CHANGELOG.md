# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.0.1] - 2026-03-16

### Added
- Initial release of Lockstep
- Agent personality and coaching philosophy (`config/agent.claude.md`)
- Goal tracking CLI (`src/lockstep/`) with SQLite storage
- Check-in scheduler for proactive morning/midday/evening messages
- Weekly review cron job (Sunday 6pm UTC)
- User profile system (`profiles/user.md`) with values, decision framework, and patterns
- Branding assets (logo, banner)

### Built On
- [claude-code-telegram](https://github.com/gx-ai-architect/claude-code-telegram) v1.5.0 — Telegram bot infrastructure, Claude Code SDK integration, event bus, APScheduler

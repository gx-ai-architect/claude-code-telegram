# Lockstep Rebrand & Migration Plan

## Overview
Transform the claude-code-telegram fork into a standalone project: **Lockstep** — a personal prioritization coach powered by Claude Code, delivered via Telegram.

**Target repo:** `gx-ai-architect/lockstep` (private)
**Package:** `lockstep-bot`
**Version:** `0.0.1` (fresh start)
**Brand:** Bold & motivational

---

## Phase 1: Package Identity (pyproject.toml + Python source)

### 1.1 pyproject.toml
- `name = "lockstep-bot"`
- `version = "0.0.1"`
- `description = "AI-powered personal prioritization coach — fewer goals, deeper focus, real results"`
- Update `keywords` to coaching/productivity terms
- Update `classifiers` to reflect end-user tool (not dev tool)
- `[project.scripts]`: `lockstep-bot = "src.main:run"`
- `[project.urls]`: point to `github.com/gx-ai-architect/lockstep`
- Update author info if desired

### 1.2 src/__init__.py
- Update docstring: "Lockstep — personal prioritization coach"
- Change `_pkg_version("claude-code-telegram")` → `_pkg_version("lockstep-bot")`
- Update `__homepage__` to new repo URL
- Update `__author__`/`__email__` if desired

### 1.3 Makefile
- `run:` → `poetry run lockstep-bot`
- `run-debug:` → `poetry run lockstep-bot --debug`
- tmux session names: `claude-bot` → `lockstep`

---

## Phase 2: Branding Assets

### 2.1 Create `assets/` directory

### 2.2 Logo SVG (`assets/logo.svg`)
Bold, motivational style. Concept: forward-facing arrow or mountain peak with "LOCKSTEP" typography. High contrast, works at small sizes (Telegram avatar).

### 2.3 README banner (`assets/banner.svg`)
Wide banner with logo + tagline: "Fewer goals. Deeper focus. Real results."

### 2.4 Telegram bot profile image (`assets/avatar.png`)
Export the logo SVG at 512x512 for Telegram bot profile picture.

---

## Phase 3: README Rewrite

Complete rewrite of README.md. New structure:

1. **Banner image** (from assets/)
2. **One-liner:** "Your AI prioritization coach on Telegram"
3. **What is Lockstep?** — 3-4 sentences about the coaching philosophy (not the tech)
4. **How it works** — Morning priorities → Midday check-in → Evening outcome → Weekly review
5. **Quick Start** — Prerequisites, install, configure, run (simplified)
6. **Configuration** — Key env vars table
7. **Commands** — `/start`, `/new`, `/status`, `/verbose`
8. **Built on** — One line crediting claude-code-telegram as the engine
9. **License** — MIT

Remove: generic Claude Code bot demo, star history chart, detailed dev docs (keep in docs/).

---

## Phase 4: Supporting Docs

### 4.1 CLAUDE.md
- Update "Project Overview" section to describe Lockstep coaching bot
- Update references to package name and entry point

### 4.2 CONTRIBUTING.md
- Update clone URL and project name

### 4.3 SECURITY.md
- Update project name references

### 4.4 SYSTEMD_SETUP.md
- Update service name to `lockstep`
- Update paths and clone URLs

### 4.5 CHANGELOG.md
- Reset to fresh `## [0.0.1] - 2026-03-16` with "Initial release of Lockstep"

### 4.6 LICENSE
- Create MIT LICENSE file (currently missing)

### 4.7 config/projects.example.yaml
- Update slug from `claude-code-telegram` to `lockstep`

### 4.8 config/architecture.md
- Update line 43 upstream reference to say "Built on claude-code-telegram" without fork dependency

### 4.9 docs/ files
- Update GitHub URLs in setup.md, development.md

---

## Phase 5: Source Code References

### 5.1 src/bot/orchestrator.py
- Update any installation help text referencing "claude-code-telegram"

### 5.2 src/bot/handlers/message.py
- Update voice installation help text

### 5.3 src/bot/features/voice_handler.py
- Update voice installation help text (2 occurrences)

---

## Phase 6: Git Migration

### 6.1 Detach from upstream
- Remove any upstream remote: `git remote remove upstream` (if exists)
- The origin remote will be replaced when pushing to new repo

### 6.2 Create new private repo
- `gh repo create gx-ai-architect/lockstep --private`

### 6.3 Repoint origin
- `git remote set-url origin <new-repo-url>`

### 6.4 Push
- `git push -u origin claude/understand-repo-707Qt`
- Then push main when ready

---

## Execution Order

1. Phase 1 (package identity) — foundation everything else depends on
2. Phase 2 (branding) — create SVG assets
3. Phase 3 (README) — the showpiece
4. Phase 4 (supporting docs) — parallel batch
5. Phase 5 (source references) — quick grep-and-replace
6. Phase 6 (git migration) — final step, commit everything first

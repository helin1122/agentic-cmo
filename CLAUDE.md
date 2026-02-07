# Project Conventions

## Overview

This is the **CMO Agent** — an AI-powered Chief Marketing Officer agent system built on Claude Code.

## Directory Structure

- `AGENT.md` — Agent identity, capabilities, and interface contract
- `.claude/skills/` — Skill definitions (natural language function specs)
- `context/` — The agent's persistent world model (strategy, voice, learnings)
- `drafts/` — Work in progress content
- `published/` — Completed and published content
- `outputs/` — Session logs and execution artifacts

## Conventions

- All markdown files use standard GitHub-flavored markdown
- Skill definitions live in `.claude/skills/<skill-name>/SKILL.md`
- Context files are the agent's memory — update them as decisions are made
- Drafts move to `published/` once finalized and posted
- Session logs go in `outputs/` with ISO date prefixes

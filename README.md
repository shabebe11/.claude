# Claude Code Configuration & Skills

Personal configurations, skills, custom commands, and agents for Claude Code.

## Contents

- `CLAUDE.md`: Global instructions and rules read on every session.
- `skills/`: Custom skills (e.g., `graphify`, `frontend-design`, `gh-stack`, `pr-description`).
- `commands/`: Custom slash commands (e.g., `/create-pr`, `/review`).
- `agents/`: Custom specialized subagents (e.g., `code-reviewer`, `frontend-designer`, `pr-creator`).
- `settings.json`: General preferences, enabled plugins, models, and session hooks (including auto-graphify on startup).

## Startup Commands & Hooks

Session hooks in `settings.json` run automated tasks when Claude starts or resumes:
- **graphify update**: Automatically updates the repository knowledge graph on `SessionStart`.

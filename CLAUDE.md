# Git rules

- NEVER run `git commit`. Make the changes and leave them uncommitted in the working tree — I commit myself. This applies even when I ask for work "on a branch"; create/switch branches as needed, but stop before committing.

# Model rules

- The main session runs on Fable. Do not delegate work to subagents just to "save" Fable usage — handle tasks inline unless I explicitly ask for an agent.
- When spawning ANY subagent with the Agent tool, ALWAYS pass `model: "opus"` explicitly. Never spawn a subagent on Fable.
  - This applies to every agent type (general-purpose, Explore, Plan, etc.).
  - Exception: `subagent_type: "fork"` always inherits the parent model and ignores the override — so avoid forks entirely; use a fresh agent with `model: "opus"` instead.
- Subagents should run at high reasoning effort: when writing agent definitions in `.claude/agents/*.md`, set `model: opus` and high effort in the frontmatter rather than leaving them to inherit Fable.

# Code style

- NEVER add code comments. Leave existing comments alone unless asked, but don't write new ones in any file or language.

# graphify
- **graphify** (`~/.claude/skills/graphify/SKILL.md`) - any input to knowledge graph. Trigger: `/graphify`
When the user types `/graphify`, use the installed graphify skill or instructions before doing anything else.

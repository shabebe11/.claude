# Claude Code Configuration & Skills

Personal configuration, custom agents, slash commands, skills, and startup hooks for [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview).

---

## 📦 What's Inside

```text
~/.claude/
├── CLAUDE.md                 # Global rules, model constraints, and coding standards
├── settings.example.json     # Example settings, model preferences, and session hooks
├── agents/                   # Specialized subagents
│   ├── code-reviewer.md      # Objective, evidence-based code review agent
│   ├── pr-creator.md         # Interactive pull request creator
│   └── frontend-designer.md  # UI design & design-token implementation specialist
├── commands/                 # Custom slash commands
│   ├── review.md             # /review -> triggers the code-reviewer agent
│   └── create-pr.md          # /create-pr -> triggers the pr-creator agent
└── skills/                   # Reusable domain skills
    ├── graphify/             # Codebase knowledge graph & GraphRAG query tools
    ├── frontend-design/      # Frontend design token rules & patterns
    ├── gh-stack/             # Stacked pull request management
    └── pr-description/       # Standardized PR formatting templates
```

---

## 🚀 Setup & Installation

### 1. Prerequisites
* **Claude Code CLI** installed:
  ```bash
  npm install -g @anthropic-ai/claude-code
  ```
* **GitHub CLI (`gh`)** (optional, recommended for PR creation):
  ```bash
  brew install gh
  gh auth login
  ```
* **graphify** (optional, for knowledge graph generation):
  ```bash
  # Ensure graphify is installed if using the graphify hooks/skills
  pip install graphify
  ```

### 2. Install on a New Machine

Clone this repository directly into your user home directory as `~/.claude`:

```bash
git clone https://github.com/shabebe11/.claude.git ~/.claude
```

*(If you already have an existing `~/.claude` directory, make a backup first with `mv ~/.claude ~/.claude.bak`).*

### 3. Configure Your Local Settings

Copy `settings.example.json` to `settings.json`:

```bash
cd ~/.claude
cp settings.example.json settings.json
```

`settings.json` is automatically ignored by Git so your local machine paths, tokens, and environment-specific caches remain private.

### 4. Automated Startup Hook (`graphify`)

`settings.example.json` includes a `SessionStart` hook that automatically refreshes your codebase's knowledge graph whenever a project is opened:

```json
"hooks": {
  "SessionStart": [
    {
      "matcher": "startup|resume",
      "hooks": [
        {
          "type": "command",
          "command": "root=$(git rev-parse --show-toplevel 2>/dev/null) && [ \"$root\" != \"$HOME\" ] && cd \"$root\" && \"$HOME/.local/bin/graphify\" update . >/dev/null 2>&1 || true",
          "timeout": 300,
          "async": true
        }
      ]
    }
  ]
}
```

---

## 💡 Usage

### Code Review
Run `/review` inside Claude Code or invoke `@code-reviewer`:
```text
/review
```
Performs a line-by-line, evidence-based review with actionable feedback without fluff or invented issues.

### Pull Request Creator
Run `/create-pr` inside Claude Code or invoke `@pr-creator`:
```text
/create-pr
```
Analyzes current branch diffs, prompts for any optional preferences, and drafts a comprehensive PR with standardized sections.

### Knowledge Graph Navigation
Run `/graphify` inside any codebase:
```text
/graphify
/graphify query "How does authentication work?"
```

---

## 🙏 Attributions & Credits

* **[@aleckshen](https://github.com/aleckshen)** on GitHub for the **PR Reviewer** (`code-reviewer.md`, `/review`) and **PR Creator** (`pr-creator.md`, `/create-pr`, `pr-description`, `gh-stack`) agent prompts, workflows, and command implementations.
* **[safishamsi](https://github.com/safishamsi)** for [graphify](https://github.com/safishamsi/graphify) — codebase knowledge graph generation and GraphRAG exploration.

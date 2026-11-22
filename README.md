# Template for repositories that use agents

Start a new repository with **Use this template** on GitHub. It works with Cursor, GitHub Copilot, Codex, Gemini CLI, and Claude Code.

## First step

Ask the agent to run the **project-setup** skill. It reads this repository, fills in **This project** in `AGENTS.md`, replaces this README, and proposes CI and Dependabot from the stack it finds.

## What is in the template

- `scripts/setup` is the idempotent environment setup. Each cloud agent provider wrapper only calls this script.
- `AGENTS.md` holds the shared rules. After setup, it also holds the project facts. Those are the stack, the layout, and the commands that were run.
- `.agents/skills/` holds `project-setup` and `agent-environment`.
- `.claude/skills/` links to those skills so Claude Code loads them.
- `.github/copilot-instructions.md` links to `AGENTS.md`, so Copilot reads the same rules.
- A pull request template, and Dependabot for GitHub Actions.

`AGENTS.md` and `.agents/skills/` are the instruction source for Cursor, Copilot, Codex, and Gemini CLI.

## Windows and symbolic links

Git on Windows stores `.github/copilot-instructions.md` and `.claude/skills/*` as text files unless `core.symlinks` is true. Turn it on, then clone again.

```bash
git config --global core.symlinks true
```

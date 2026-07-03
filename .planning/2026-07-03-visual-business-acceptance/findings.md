# Findings

## Project Rules

- Current project initially contained only `work/` and `outputs/`.
- `AGENTS.md` and `MEMORY.md` were missing.
- User template files existed under `C:\Users\LG\.codex\templates\`, but terminal rendering showed mojibake, so clean project-specific UTF-8 files were created directly.

## Durable Preferences Captured

- The project owner only wants final visual and business outcomes.
- Codex should self-manage intermediate technical implementation, quality control, and repair loops.
- Final acceptance should emphasize aesthetics, realism, consumer appeal, business fit, compliance, and deliverability.

## Official Codex Guidance Used

- Cloud environments are configured in Codex settings and run cloud tasks in containers that check out a repository, run setup, apply internet settings, execute agent work, and show final answer plus diff.
- Codex web requires connecting a GitHub account so Codex can work with repositories and create pull requests.
- Worktrees require a Git repository and are managed by Codex under `$CODEX_HOME/worktrees`.
- Subagents are available by default, but Codex only spawns them when explicitly asked.

# AGENTS.md

## Rules

1. Verify against the real artifact (run the feature, read the actual value, inspect the diff), not a proxy, self-report, or "it compiles."
2. Trace each symptom back to the first place the system went wrong and fix it there. A guard is a fix only when the state it handles is legitimate.
3. Remove dead code, redundant validators, and stub references first, then build on the simpler base.
4. Bias toward deletion and the smallest change that solves the problem.
5. Assert what the code's users can observe, so the test fails when that behavior breaks and keeps passing when only the internals change.
6. Keep a test that catches the first edit and survives the second. Rewrite or delete the rest.
7. Rename, extract, type, or rearchitecture so the behavior is obvious without prose.
8. Concentrate guards at system boundaries (CLI, config, network, external APIs). Trust internal types and keep business logic in pure functions.
9. Design every state-changing operation to converge to the correct state however many times it runs and wherever the previous run stopped.
10. Break work into small units that each end in a verifiable state, check each before the next, and order delivery so the sequence proves itself. Each commit lands on its own.
11. Before you trust, report, or act on a measured number, find what limits it, and rule out that it measured something other than the work you think.
12. Encode a repeated correction as a lint, metadata flag, runtime check, or script instead of more text.
13. Write the real symbol, file, flag, or command name, not a synonym or a description of it, and make every count or tree claim true at the commit that lands it.
14. A PR body is a briefing a reviewer can read in under a minute. Do not paste swarm logs, SHA lists, or metric tables. Link them.
15. Cut every word that does no work in documentation, PR descriptions, and commit messages.
16. Product direction comes from the human. Proceed on reversible work and present the result. Confirm only irreversible actions.
17. Environment setup lives in `scripts/setup` and is idempotent. Each cloud agent provider wrapper only calls that script. When dependencies, the toolchain, or startup steps change, update the script and check that the wrappers still work. If the project uses a provider that has no wrapper, add one.

## Skills

This template ships `project-setup` and `agent-environment` in `.agents/skills/`. `.claude/skills/` links to those folders so Claude Code loads the same skills.

## Credit

Rules 1 to 16 are adapted from [pstack](https://github.com/cursor/plugins/tree/main/pstack) by Lauren Tan, under the MIT license.

## This project

The `project-setup` skill fills this section on the first task in the repository.

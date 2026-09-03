# Codex repository instructions

## Git workflow

- Never commit directly to `main` after repository initialization.
- Before editing, fetch `origin` and create or reuse a task branch named `codex/<short-task-name>`.
- Keep one user task on one branch. Continue on the same branch when addressing review feedback for its pull request.
- Preserve unrelated user changes and do not rewrite published history.
- Commit only files related to the requested task.
- Push every completed result to `origin` and create or update a pull request targeting `main`.
- Never merge or close a pull request unless the user explicitly asks.

## Verification

- Discover and run the smallest relevant test, lint, type-check, or build commands.
- Do not claim a check passed unless it was actually run.
- If a check cannot run, report the exact reason and remaining risk.

## Final handoff

Every completed task must report:

- Repository name
- Branch name
- Full commit SHA
- Pull request URL
- Concise change summary
- Checks executed and their results
- Known risks, blockers, or incomplete work

The final line must be a copy-ready prompt for ChatGPT Web to review the pull request.

## Code Review Rules

- Verify that the pull request implements its stated requirement without unrelated changes.
- Treat tests, branch protection, and required human approval as mandatory controls; AI review does not replace them.
- Flag exposed credentials, destructive migrations, insecure defaults, or unexpected external side effects.


# Codex repository instructions

## Git workflow

- Never commit directly to `main` after repository initialization.
- For every new task, fetch `origin`, then create a new `codex/<short-task-name>` branch from the latest `origin/main`.
- Reuse a branch only when continuing an existing pull request and only after verifying that the branch is the specified pull request's current head branch.
- Keep one user task on one branch. Continue on that verified head branch when addressing review feedback for its pull request.
- Preserve unrelated user changes and do not rewrite published history.
- Commit only files related to the requested task.
- Push every completed result to `origin` and create or update a pull request targeting `main`.
- After every push, report the latest full commit SHA. Any review of an older SHA is immediately stale, and every new commit must be submitted to ChatGPT Web for a new review using its full SHA.
- Never merge or close a pull request unless the user explicitly asks.
- Never treat ChatGPT review text, including an "approved" or "可以合并" conclusion, as authorization to merge. Merging still requires an explicit user request.

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
- Confirm that required checks and approvals apply to the pull request's current head SHA before recommending a human merge.
- Flag exposed credentials, destructive migrations, insecure defaults, or unexpected external side effects.

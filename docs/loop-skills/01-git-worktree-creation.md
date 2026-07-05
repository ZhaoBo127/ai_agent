# Skill: Git Worktree Creation

Read this skill first before starting any new loop workflow. A loop task must run in an isolated
Git worktree created from the latest `origin/main`.

## Naming Convention

Classify the task from the human wording. Do not require a rigid slash-command schema.

- Feature work: `feature-<short-slug>`
- Bug fix work: `bug-<short-slug>-YYYYMMDD`
- PR review work: `review-pr-<number>-YYYYMMDD`
- Production incident/hotfix: `prod-<short-slug>-YYYYMMDD-HHMM`
- Release/bake/deploy: `release-<short-slug>-YYYYMMDD`
- Unknown/general: `loop-<short-slug>-YYYYMMDD`

Slug rules:

- lowercase
- ASCII letters, numbers, and hyphens only
- remove filler words like `the`, `a`, `please`, `fix`, `implement`
- keep it short: 3 to 8 words maximum
- include the date in `YYYYMMDD` using the current local date available to the supervisor

Examples:

- `add loop runbook support` -> `feature-loop-runbook-support`
- `fix storage billing pagination undercount` -> `bug-storage-billing-pagination-20260628`
- `review PR 600 billing flush auditability` -> `review-pr-600-20260628`
- `prod live sessions failing rollback` -> `prod-live-sessions-20260628-1430`

## Branch and Worktree Names

Use the loop name for the human workflow, but every worker-owned runtime artifact must use the
`worker-` prefix so the runtime reaper can find it deterministically.

```text
worker name: worker-<loop-name>
worktree:    /workspace/.loop-worktrees/worker-<loop-name>
branch:      loop/worker-<loop-name>
```

`/workspace` must be the supervisor session's git repo root, not a parent that merely contains a
nested repo. The runtime reaper runs from `/workspace` by default; `git worktree list` from
`/workspace` must show every worker worktree.

## Creation Procedure

Always fetch before creating the worktree. Never branch from stale local `main`.

```bash
cd /workspace
test "$(git rev-parse --show-toplevel 2>/dev/null)" = "/workspace"
git fetch origin main
base_sha="$(git rev-parse origin/main)"
worker_name="worker-<loop-name>"
mkdir -p /workspace/.loop-worktrees
git worktree add "/workspace/.loop-worktrees/${worker_name}" -b "loop/${worker_name}" origin/main
cd "/workspace/.loop-worktrees/${worker_name}"
mkdir -p .loop
```

Immediately record this in `.loop/RUNBOOK.md`:

- loop name
- worker name
- repo path
- base branch
- `base_sha`
- worktree path
- branch name
- original task
- first plan

## Guardrails

- Do not edit the supervisor's base checkout directly.
- Do not create worker worktrees outside `/workspace/.loop-worktrees/worker-*`.
- Do not reuse a dirty worktree for a new task.
- If the branch or worktree already exists, inspect it and resume only if it is clearly the same
  loop task.
- Before any destructive cleanup, run `git status --short`.
- Preserve useful work by commit, branch push, PR, patch file, or explicit human abandonment.

# Skill: Loop Teardown

Before declaring a loop done:

1. Update `.loop/RUNBOOK.md` with final status.
2. Preserve useful work by commit, branch push, PR, patch file, or explicit human abandonment.
3. Stop the worker Codex tmux session recorded for this loop.
4. Stop the critic Codex process recorded for this loop, if still running.
5. Remove the isolated worktree only when safe.
6. Post a concise Slack update with result, PR/branch link if any, and cleanup status.

Stop the recorded worker:

```bash
if test -f .loop/worker.tmux; then
  worker_name="$(cat .loop/worker.tmux)"
  case "$worker_name" in
    worker-*) tmux kill-session -t "$worker_name" 2>/dev/null || true ;;
    *) echo "refusing to kill non-worker tmux session: $worker_name" >&2 ;;
  esac
fi
```

Stop the recorded critic:

```bash
if test -f .loop/critic.pid; then
  pid="$(cat .loop/critic.pid)"
  if ps -p "$pid" >/dev/null 2>&1; then
    kill "$pid"
  fi
fi
```

Remove the worktree:

```bash
cd /workspace
git worktree remove "/workspace/.loop-worktrees/worker-<loop-name>"
```

Guardrails:

- Do not delete a worktree with uncommitted useful work.
- Do not delete a branch that has not been pushed or explicitly abandoned.
- Do not kill unrelated Codex processes or non-`worker-*` tmux sessions.
- Ask for human approval before destructive cleanup, production deploys, rollback actions, or
  deleting ambiguous state.

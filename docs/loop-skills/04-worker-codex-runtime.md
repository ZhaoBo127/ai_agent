# Skill: Worker Codex Runtime

Start a separate worker Codex only when the supervisor decides the task needs worker execution.
Run the worker from inside the isolated worktree.

The tmux session name must exactly match the `worker-<loop-name>` worktree directory name recorded
by `01-git-worktree-creation.md`. Do not start worker Codex as a bare background process; the
runtime M4 reaper finds worker sessions by the `worker-*` tmux prefix.

Default worker command shape:

```bash
worker_name="$(basename "$PWD")"
case "$worker_name" in worker-*) ;; *) echo "worker worktree must be named worker-*" >&2; exit 1 ;; esac
mkdir -p .loop
tmux new-session -d -s "$worker_name" -c "$PWD" \
  "codex exec --dangerously-bypass-approvals-and-sandbox -c model_reasoning_effort=xhigh '<worker task prompt>' > .loop/worker.log 2>&1"
printf '%s\n' "$worker_name" > .loop/worker.tmux
```

If the local Codex CLI requires the repo check to be skipped, add:

```bash
--skip-git-repo-check
```

Worker prompt requirements:

- Begin with: `Before acting, read the relevant files in .loop/skills/ and .loop/RUNBOOK.md.`
- Tell the worker to update `.loop/RUNBOOK.md` before and after edits.
- Tell the worker to keep changes inside the worktree.
- Tell the worker to run focused tests and record commands/results.
- Tell the worker to stop and record a blocker instead of making risky assumptions.

Worker tmux rules:

- Only write the tmux session name for the worker Codex started by this loop.
- Do not kill unrelated Codex processes or unrelated tmux sessions.
- On every supervisor tick, check whether `.loop/worker.tmux` still points to a live `worker-*`
  tmux session before trusting worker status.

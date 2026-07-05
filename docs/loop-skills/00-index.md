# Loop Skill Pack

The bridge injects this ordered skill pack into each scheduled supervisor tick. The live channel
supervisor Codex must read these skills before starting or resuming a loop workflow.

Loop workflow skills apply only when a human starts or continues a loop task. For ordinary Slack
turns, keep the system supervisor skills as standing behavior.

Skill order:

1. `01-git-worktree-creation.md` — read first; naming conventions and latest-main worktree creation.
2. `02-common-skill-sync.md` — make shared skills available under `.loop/skills/` for workers.
3. `03-supervisor-workflow.md` — supervisor ownership and loop state.
4. `04-worker-codex-runtime.md` — start worker Codex in the worktree with bypass permissions.
5. `05-runbook-contract.md` — required `.loop/RUNBOOK.md` structure.
6. `06-feature-prd.md` — create a PRD under `documents/prds/` before feature implementation.
7. `07-bug-report.md` — create a report under `documents/bugs/` before bug implementation.
8. `08-adversarial-verification.md` — spin up a critic Codex to verify setup artifacts.
9. `09-teardown.md` — stop worker/critic Codex and remove the worktree safely.

The bridge is only the Slack timer/router. The supervisor owns all workflow decisions.
If a scheduled `/loop` reminder includes task-specific instructions, treat that reminder as the
source of truth for that tick.

Before creating workers or worktrees:

- Use `/workspace` as the supervisor session's git repo root.
- Use worker tmux sessions named `worker-*`.
- Use worker worktrees under `/workspace/.loop-worktrees/worker-*`.
- Keep each worker's `.loop/RUNBOOK.md` current so the supervisor can inspect progress without
  direct worker-to-supervisor messaging.
- Tear down worker tmux sessions and worktrees when the workflow is complete.

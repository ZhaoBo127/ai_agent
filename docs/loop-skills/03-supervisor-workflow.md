# Skill: Supervisor Workflow Ownership

Use this skill after reading `01-git-worktree-creation.md` and `02-common-skill-sync.md`.

Rules:

- The bridge is only the Slack timer/router.
- The live channel supervisor Codex owns workflow planning and decides whether to create workers.
- Normal Slack messages continue to go to the supervisor.
- Workers do not talk to Slack directly.
- Workers report progress by updating `.loop/RUNBOOK.md` in their own worktree.
- If the task is ambiguous, ask one concise Slack-visible question before creating the worktree.
- If the task is clear, create or resume the workflow without waiting for another bridge action.
- For feature tasks, create the PRD before implementation work begins.
- For bug tasks, create the bug report before implementation work begins.
- For feature and bug tasks, run the adversarial verification skill after the worktree, runbook,
  shared skills, and PRD/bug report are created.

At the start of a workflow, decide:

- target repo
- loop name from `01-git-worktree-creation.md`
- base branch, usually `main`
- worktree path
- loop branch name
- whether a separate worker Codex is needed
- stop condition

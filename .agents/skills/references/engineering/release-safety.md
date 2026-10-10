# Release Safety

The release skill decides, verifies, and coordinates. Existing scripts, CI, and deployment tooling perform repeatable mechanics. Discover the project's real release path and use its commands; do not transcribe a generic deployment recipe into the skill.

For the exact commit/artifact and target environment, establish review status and current checks, expected migrations/backfills, old/new schema compatibility, queued-job argument compatibility, web/worker coexistence, frontend asset/API compatibility, configuration and feature-flag prerequisites, observability, and recovery path. Make the work proportional to the change: a release with no schema change does not need an elaborate migration plan.

Before production execution, present the target, immutable revision, migration behavior, principal risks, and rollback or forward-recovery method for explicit approval. Approval applies to the concrete action and revision; a changed revision or materially different release needs a new preflight.

After execution, verify more than command success: deployment revision, relevant health endpoint/processes, migrations/workers when applicable, critical smoke behavior, error/log/queue signals, and rollback triggers. If checks fail, report the observed state and route diagnosis to `dev-debug`; do not silently turn release orchestration into incident debugging.

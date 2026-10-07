---
name: dev-release
description: Prepare and coordinate a safe release of an implemented software change. Use after implementation and review when the user wants rollout, deployment readiness, or release execution; account for repository-specific production constraints and obtain required authorization before irreversible external actions.
---

# DEV Release

Use the current conversation and durable SPEC/PLAN, review findings, actual diff, tests, deployment configuration, and operational runbooks to establish release readiness. Follow [workflow governance](../references/workflow-governance.md), the [engineering router](../references/engineering/README.md), and [production safety](../references/engineering/production-safety.md). Load only other relevant playbooks. Use the user's current language for conversation; durable artifacts follow the initiative's language policy, English by default.

Check unresolved review findings and verification, schema/data compatibility, rolling deployment order, queued-job compatibility, feature flags where warranted, observability, rollback/recovery, and ownership of manual steps. Derive commands from the repository; do not invent a deploy procedure. State blockers and a concrete release sequence. Execute only release actions the user has authorized and that the environment permits; obtain approval for an irreversible or external action when authorization is missing. Verify observed results and report what shipped, what remains, and any rollback trigger. Do not treat an audit recommendation as release-ready implementation.

## Definition of Done

The release has a repository-grounded sequence, applicable safety and rollback checks, clear authorization for actions taken, observed verification, and an accurate status report.

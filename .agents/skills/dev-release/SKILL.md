---
name: dev-release
description: Prepare and coordinate a safe release of an implemented software change. Use after implementation and review when the user wants rollout, deployment readiness, or release execution; require explicit approval immediately before production deployment and verify the result.
---

# DEV Release

Ship the approved change through the repository's real deployment path. The skill decides, verifies, and coordinates; existing scripts, CI, and deployment tooling perform deterministic operations. A successful deploy command alone does not complete a release.

Follow [workflow governance](../references/workflow-governance.md). Use the user's current language for conversation. Personal notes follow an explicit current language request, then a recorded personal preference, otherwise English. Load additional playbooks only for release risks present in this change.

## Resolve the target and release mechanism

Recover the intended environment, active-chat or personal initiative context, review findings, actual diff, tests, operational runbooks, and deployed/current revision. Revalidate personal notes against current Git and deployment evidence. Identify the **exact commit SHA or immutable artifact** to ship. Inspect the repository's actual deployment mechanism, such as Kamal, Capistrano, GitHub Actions, Heroku, Render, Fly.io, Docker/Kubernetes, or project scripts. Use its established commands (`bin/deploy`, CI workflow, `bin/smoke`, etc.) rather than inventing a procedure. Load [release safety](../references/engineering/release-safety.md), [production safety](../references/engineering/production-safety.md), and applicable guidance from the [engineering router](../references/engineering/README.md). Use current framework/tooling docs when version-sensitive behavior changes the decision.

Read existing project environment/runbook documentation when present. Otherwise, use personal local notes for useful non-secret SSH aliases, environment names, host roles, app paths, services, deploy tooling, and observability locations. Never create `ops/ENVIRONMENTS.md` or another repository process artifact. Keep credentials, tokens, keys, secret-bearing URLs, cookies, and temporary credentials out of notes; prefer SSH config/agents and secret tooling. Create no inventory merely for a checklist.

## Preflight: claim → evidence

Before production execution, establish:

- exact revision/artifact, target, deploy mechanism, and currently deployed revision;
- review status, unresolved findings, and required checks green for **that revision**;
- schema/data migrations, backfills, lock/rewrite risk, old/new code compatibility, and recovery when relevant;
- queued-job arguments, workers, retry/idempotency, and old/new worker coexistence when relevant;
- asset, frontend/backend, API, configuration, secret, and feature-flag compatibility when relevant;
- rollout order, health/smoke checks, observability, and rollback or forward-recovery path.

Use the actual repository and CI evidence. A previous green run on another commit is insufficient. If a required check is unavailable, say what is unverified and whether that blocks release. A routine release with no migration needs a concise compatibility check, not a fabricated migration program. Do not treat an audit recommendation as implemented code.

## Production approval boundary

Codex sandbox permission to run a command is separate from approval of the production release. Do all safe preflight work first. Immediately before the production deployment action, present a compact, reviewable release card: target environment, exact revision/artifact, migration behavior, principal risks, rollback/recovery path, and verification plan. Obtain explicit approval for that concrete production action. Do not ask repeatedly for low-risk preflight work. If revision, target, or material risk changes after approval, re-evaluate and obtain approval for the changed action. Staging and other external mutations also require authorization when it is missing.

## Execute and observe

Use the existing deterministic release mechanism with the approved target and revision. Record the actual command/workflow and observed result in chat; use a concise personal release note only if another chat will need it. Explain material deploy compatibility and recovery trade-offs when useful. Afterward verify the deployed revision plus relevant health endpoint, web/worker process state, migration status, critical smoke path, new errors/logs, and queue status using configured observability. Check only relevant signals, but do not stop at command success. If a problem appears, report the observed release state and route diagnosis to `dev-debug`; do not silently switch workflows or perform unapproved rollback/restarts.

## RED FLAGS

- “The migration is small” used to skip compatibility/lock analysis.
- Treating tests on a prior commit as evidence for the current release artifact.
- Treating staging success as automatic production approval or safety.
- Embedding guessed deployment commands in skill prose instead of using repository automation.
- Declaring success from a zero exit code without post-deploy evidence.

## Completion gate

Release readiness requires a known revision, review/check status, relevant compatibility analysis, concrete recovery plan, authorized execution boundary, and defined verification. A completed release additionally requires observed deployment identity, relevant health/smoke/error/worker/migration checks, and an accurate status report. If execution was not authorized or checks failed, report **ready**, **blocked**, or **partially verified** rather than **released**. Recommend a next execution tier through [execution policy](../references/execution-policy.md) only when another DEV step is needed.

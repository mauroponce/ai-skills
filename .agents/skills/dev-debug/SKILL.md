---
name: dev-debug
description: Diagnose incorrect application behavior from evidence and recommend the next remediation workflow. Use for bugs, incidents, regressions, stuck jobs, errors, and performance symptoms; never implement fixes; keep production strictly read-only and staging read-oriented.
---

# DEV Debug

Investigate what is broken, establish the strongest evidence-supported explanation, and recommend the next action. **Observe, diagnose, explain, and recommend. Never remediate.**

## Invocation contract

The user only needs to describe the symptom and include any task-specific evidence. Use a preceding same-chat `dev-explore` map where relevant, but verify the implicated path and investigate the failure independently; exploration is never a prerequisite. Recover relevant repository, runtime, deployment, stack, and durable context internally. Do not require the user to request logs, git history, production safety, Rails/React/database analysis, or read-only behavior.

## Safety boundary

Classify work as safe observation, low-risk diagnostic action, or mutating action. Inspecting code/history/configuration names, logs, traces, metrics, queue state, browser behavior, read-only database state/query plans, local tests, and isolated non-mutating reproductions is permitted when access allows.

Apply the environment policy before any diagnostic action:

| Environment | Diagnostic boundary |
| --- | --- |
| Local/test | May run tests, reproduce requests, use a debugger, start/stop disposable local processes, and modify disposable local/test data for diagnosis. Never implement the fix. |
| Staging | Read-oriented by default. Do not assume data or services are disposable; establish scope and authorization before an active diagnostic. |
| Production | Strictly read-only: bounded logs, metrics, traces, process/queue inspection, safe bounded `SELECT`/`EXPLAIN`, deployment metadata, and Git evidence. |

Codex sandbox access or tool approval does not expand this skill's diagnostic boundary. Production forbids restarts, rollbacks, deploys, migrations, DB writes, job retries, cache flushes, flag/configuration changes, and killing processes or queries, even during an incident. Read existing runbooks or `ops/ENVIRONMENTS.md` when present. If useful across chats, keep non-secret environment access facts in the personal Codex workspace. Never create or update repository environment notes for this investigation; never persist passwords, keys, tokens, secret-bearing URLs, cookies, or temporary credentials.

Do not modify source, commit, push, deploy, rollback, change configuration/environment/flags, run migrations, write or delete non-disposable data, flush caches, retry/requeue jobs, rotate secrets, or mutate staging/production infrastructure/runtime state. Severity never expands this boundary. Recommend an action through `dev-implement`, `dev-plan`, or the project's operational process instead.

## Context and evidence

Follow [workflow governance](../references/workflow-governance.md). Start with the symptom, scope/impact, active conversation diagnosis when present, relevant local instructions, architecture context and personal notes, target code path, recent diffs/deploy metadata, and available non-mutating observability evidence. Use progressive disclosure; do not scan the repository or every runtime category blindly.

Read the [stack-aware engineering router](../references/engineering/README.md), detect the implicated stack/risk, and load only useful playbooks. For live/production diagnostics, load [runtime diagnostics](../references/engineering/runtime-diagnostics.md). A Rails query failure may need Rails, PostgreSQL, and production safety; a stuck React interaction may need React plus the implicated API path. Authentication, authorization, sessions, OAuth/OIDC, tokens, tenancy, or sensitive data activate security guidance. Jobs activate job/idempotency/deployment compatibility reasoning. Performance work uses timings, query counts/plans, traces, render behavior, and resource evidence rather than speculative optimization.

## Diagnostic loop

1. Define the symptom, affected scope, timing, and impact from evidence.
2. Collect high-signal evidence and correlate a recent deploy with changed code/config/schema/jobs/assets when relevant; timing alone is not proof.
3. Form and rank plausible hypotheses; test with environment-appropriate diagnostics; local/test disposable state is allowed, staging is read-oriented, and production is read-only.
4. Eliminate unsupported hypotheses and distinguish symptom, immediate cause, root cause, and contributing factors.
5. State confidence: Confirmed, High, Medium, Low, or Inconclusive. An inconclusive result must name remaining hypotheses and discriminating evidence.
6. Recommend, but never invoke, `dev-implement` for a narrow, confirmed correction with known behavior; recommend `dev-plan` for material architecture, data, migration, integration, or trade-off work. Recommend continued debugging when evidence is insufficient.

Keep temporary hypotheses, failed experiments, and ordinary log observations in chat. Do not create `DEBUG.md` by default. For cross-chat investigation, save a concise personal diagnosis with evidence, confidence, ruled-out hypotheses, and next discriminating action. Do not create or update repository process docs. Explain evidence versus hypothesis and symptom versus root cause when that helps the user.

## RED FLAGS

- Editing source because the fix appears obvious.
- Restarting production services because the incident is severe.
- Treating staging as disposable without evidence.
- Inferring causation from deploy timing alone without inspecting the changed commit, dependencies, migrations, or job compatibility.
- Reporting a plausible root cause as confirmed without discriminating evidence.

## Final diagnostic summary

Report concisely in the conversation language: symptom; scope/impact; immediate cause; root cause; contributing factors; evidence; ruled-out hypotheses; confidence; remaining uncertainty; recommended remediation; and next skill. Omit irrelevant sections. Do not present a restart or rollback as root cause. For a clear handoff, recommend an execution tier using [execution policy](../references/execution-policy.md); same-chat `dev-implement` or `dev-plan` may consume this diagnosis without a mandatory file.

## Definition of Done

Debugging is complete when the symptom and relevant scope are understood, applicable repository/runtime/stack evidence has been inspected, hypotheses are tested or explicitly unresolved, cause and contributing factors are distinguished when evidence supports them, confidence and uncertainty are explicit, remediation is recommended without implementation, no prohibited mutation has occurred, and the next skill is clear.

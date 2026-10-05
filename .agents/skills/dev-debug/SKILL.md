---
name: dev-debug
description: Diagnose incorrect application behavior from evidence and recommend the next remediation workflow. Use for bugs, incidents, regressions, stuck jobs, errors, and performance symptoms; never implement fixes or mutate application, production, runtime, infrastructure, or configuration state.
---

# DEV Debug

Investigate what is broken, establish the strongest evidence-supported explanation, and recommend the next action. **Observe, diagnose, explain, and recommend. Never remediate.**

## Invocation contract

The user only needs to describe the symptom and include any task-specific evidence. Recover relevant repository, runtime, deployment, stack, and durable context internally. Do not require the user to request logs, git history, production safety, Rails/React/database analysis, or read-only behavior.

## Safety boundary

Classify work as safe observation, low-risk diagnostic action, or mutating action. Inspecting code/history/configuration names, logs, traces, metrics, queue state, browser behavior, read-only database state/query plans, local tests, and isolated non-mutating reproductions is permitted when access allows.

Do not modify source, commit, push, deploy, rollback, restart or kill processes, change configuration/environment/flags, run migrations, write or delete production data, flush caches, retry/requeue jobs, rotate secrets, or mutate infrastructure/runtime state. Severity never expands this boundary. Recommend an action through `dev-implement`, `dev-plan`, or the project's operational process instead.

## Context and evidence

Follow [workflow governance](../references/workflow-governance.md). Start with the symptom, scope/impact, active conversation diagnosis when present, relevant local instructions, architecture/SPEC, target code path, recent diffs/deploy metadata, and available non-mutating observability evidence. Use progressive disclosure; do not scan the repository or every runtime category blindly.

Read the [stack-aware engineering router](../references/engineering/README.md), detect the implicated stack/risk, and load only useful playbooks. A Rails query failure may need Rails, PostgreSQL, and production safety; a stuck React interaction may need React plus the implicated API path. Authentication, authorization, sessions, OAuth/OIDC, tokens, tenancy, or sensitive data activate security guidance. Jobs activate job/idempotency/deployment compatibility reasoning. Performance work uses timings, query counts/plans, traces, render behavior, and resource evidence rather than speculative optimization.

## Diagnostic loop

1. Define the symptom, affected scope, timing, and impact from evidence.
2. Collect high-signal evidence and correlate a recent deploy with changed code/config/schema/jobs/assets when relevant; timing alone is not proof.
3. Form and rank plausible hypotheses; test only with safe observation or non-mutating diagnostics.
4. Eliminate unsupported hypotheses and distinguish symptom, immediate cause, root cause, and contributing factors.
5. State confidence: Confirmed, High, Medium, Low, or Inconclusive. An inconclusive result must name remaining hypotheses and discriminating evidence.
6. Recommend, but never invoke, `dev-implement` for a narrow, confirmed correction with known behavior; recommend `dev-plan` for material architecture, data, migration, integration, or trade-off work. Recommend continued debugging when evidence is insufficient.

Keep temporary hypotheses, failed experiments, and ordinary log observations in chat. Do not create `DEBUG.md` by default. Persist only stable architecture/infrastructure facts to their owning context, product-behavior conflicts to SPEC, or an incident record when the project convention, user, handoff, or compliance requires it.

## Final diagnostic summary

Report concisely in the conversation language: symptom; scope/impact; immediate cause; root cause; contributing factors; evidence; ruled-out hypotheses; confidence; remaining uncertainty; recommended remediation; and next skill. Omit irrelevant sections. Do not present a restart or rollback as root cause.

## Definition of Done

Debugging is complete when the symptom and relevant scope are understood, applicable repository/runtime/stack evidence has been inspected, hypotheses are tested or explicitly unresolved, cause and contributing factors are distinguished when evidence supports them, confidence and uncertainty are explicit, remediation is recommended without implementation, no mutation has occurred, and the next skill is clear.

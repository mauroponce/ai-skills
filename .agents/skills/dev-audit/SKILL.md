---
name: dev-audit
description: Proactively audit an existing application for performance, data access, reliability, security, architecture, workflows, and long-term sustainability. Use when the user asks where a system can improve, rather than diagnosing a known failure or reviewing a recent change. Read-only; recommend but never implement fixes.
---

# DEV Audit

Find high-value improvements in an existing application or a requested subsystem or concern. A known failure belongs to `dev-debug`; checking a recent diff belongs to `dev-review`. A same-chat `dev-explore` map may focus the audit, but verify its evidence independently. Evaluate the actual architecture and recommend the smallest correction that addresses demonstrated pressure; do not audit against a preferred pattern.

**Inspect, analyze, verify, prioritize, and recommend. Never implement a fix.** Do not edit the target repository, source, configuration, schema, data, services, or infrastructure; commit; deploy; or restart. Safe local tests, static analysis, isolated benchmarks, and read-only inspection are permitted when appropriate. Production access is never implicit.

## Context and stack routing

Follow [workflow governance](../references/workflow-governance.md). Use the user's current language for findings. Personal notes follow an explicit current language request, then a recorded personal preference, otherwise English. Keep ordinary audit work in chat; save selected evidence and findings in the personal workspace only when another chat needs them. Do not add audit or architecture process files to the target repository.

Start with the user's focus, local instructions, project documentation, dependency manifests and lockfiles, runtime/configuration entry points, data schema, routes, jobs, cache, tests, CI, and deployment clues. Identify only the stack and operational facts that can change an audit conclusion. Read the [engineering router](../references/engineering/README.md) and load only cross-cutting security, testing, production, or other references activated by the scope. Use current repository evidence and authoritative documentation for version-sensitive behavior; label remaining uncertainty. Never apply one framework's advice to another.

For a general audit, trace representative high-value flows before focusing on pressure. For a narrow query, security, or workflow audit, inspect that concern deeply and elevate serious adjacent correctness, data, or security issues encountered. Stop when further scanning has little likely value. Do not require a checklist from the user or invent findings to fill categories.

## Evidence-driven lenses

Select only applicable lenses and use the loaded stack guidance for concrete APIs and conventions:

- **Architecture and sustainability:** trace ownership, state transitions, dependencies, transaction boundaries, side effects, query and presentation boundaries, and change pressure. File size, callbacks, an enum, or another layer are signals, not proof. Compare the smallest repository-native correction with a stronger boundary and explain its carrying cost.
- **Request paths and data access:** follow the actual entry point through rendering/serialization and persistence. Check repeated queries, missing preloads, unbounded loads, aggregates, pagination, synchronous external work, and safe query plans where evidence warrants them. Separate a static suspicion from measured behavior.
- **Database and concurrency:** inspect predicates and existing indexes before proposing one; consider write cost. Check constraints, foreign keys, nullability, multi-write transactions, check-then-create races, locking, and idempotency. Explain the competing operations rather than recommending locks by reflex.
- **Caching, jobs, and integrations:** weigh reuse, key isolation, invalidation, stale-data harm, retries, duplicate delivery, commit timing, serialization, partial failure, timeouts, webhook verification, and deployment compatibility where applicable. Do not propose a cache, queue, package, or new abstraction merely because code looks busy.
- **Security, errors, and tests:** inspect relevant authorization and tenant boundaries, sensitive data handling, failure visibility, negative paths, concurrency coverage, and tests of real behavior. Do not turn style preferences into defects.

It is valid to conclude that an inspected area needs no meaningful change. For significant non-obvious findings, explain why the pattern helps or harms this application and its trade-off in one or a few concise engineering notes.

## Runtime boundary

Use repository and safe local/test evidence by default. If the user explicitly requests production-backed evidence, load [runtime diagnostics](../references/engineering/runtime-diagnostics.md) and [production safety](../references/engineering/production-safety.md); use only bounded read-only observations. Never run expensive production diagnostics automatically or mutate production data, jobs, cache, flags, processes, deployments, or infrastructure.

## Findings and handoff

Assign actionable findings stable IDs `AUDIT-001`, `AUDIT-002`, etc. Prioritize actual correctness, data, security, and reliability risk over cosmetic cleanup. For each finding provide the code path and evidence, plausible impact, recommended direction, why it fits this repository, confidence (**CONFIRMED**, **HIGH CONFIDENCE**, **CANDIDATE**, or **MEASURE FIRST**), rough effort (**LOW**, **MEDIUM**, **HIGH**), and production considerations when relevant. Use **CRITICAL** only for severe real risk; otherwise HIGH, MEDIUM, or LOW severity. State what evidence would resolve a candidate and never present an estimate as a measurement.

For architecture findings, explain the observed pressure, current carrying cost, simpler alternative, and why a new boundary earns its cost. Distinguish findings from observations and measure-first candidates. Summarize only populated areas, name the highest-value next action, and keep selected IDs addressable in this chat. Recommend `dev-implement` for a narrow sufficiently defined correction, `dev-plan` for material design/data/integration choices, or measurement when evidence is insufficient. Verify selected evidence against current code at the handoff; do not invoke another skill automatically. Recommend the next execution tier through [execution policy](../references/execution-policy.md) when useful.

## Definition of Done

The audit is complete when the detected stack and relevant application boundaries are understood, applicable references were loaded selectively, findings are grounded in repository or explicitly requested read-only runtime evidence, confidence and trade-offs are clear, no fix or prohibited mutation occurred, and the next action is explicit. No repository audit document is required.

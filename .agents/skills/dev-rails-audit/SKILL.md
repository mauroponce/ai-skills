---
name: dev-rails-audit
description: Perform a deep, evidence-driven audit of an existing Ruby on Rails application to identify and prioritize opportunities for improving performance, Active Record and database usage, caching, background jobs, reliability, error handling, maintainability, production safety, and Rails-native design. Use when the user wants to proactively improve a Rails application rather than diagnose a known failure or review a specific recent change. Do not implement fixes.
---

# DEV Rails Audit

Find high-value improvements in an existing Rails application or a requested subsystem or concern. `$dev-rails-audit` alone starts a general audit; no checklist is required from the user. A known failure belongs to `dev-debug`; checking a recent diff against its intent belongs to `dev-review`. This skill asks where the existing system can improve.

**Inspect, analyze, verify, prioritize, and recommend. Never implement a fix.** Do not edit application code or configuration, commit, change schema/data, deploy, restart, or alter infrastructure or runtime state. Safe local tests, static analysis, read-only Rails runner inspection, local benchmarks, and safe query plans are permitted. Production access is never implicit.

## Language and context

Follow [workflow governance](../references/workflow-governance.md). Detect the user's current language and use it for conversation, clarifications, and findings. Durable artifacts use the active initiative's explicit artifact language, otherwise English, unless the user explicitly directs otherwise. Do not infer artifact language from conversational Spanish. Keep transient audit hypotheses and findings in the same chat by default; do not create `RAILS_AUDIT.md`. Persist genuinely stable architecture, stack, or operational facts to an existing owning artifact when useful, never a speculative optimization as fact. Write a report only when requested, a cross-chat/team handoff requires one, or project convention calls for one.

## Detect, then inspect

Start with local instructions, README/architecture context, `.ruby-version`, `Gemfile` and lockfile, Rails configuration, database configuration/schema, routes, job/cache configuration, tests, CI, and deployment/observability clues. Identify Ruby and Rails versions, application type, database engine/version when available, authentication/authorization, queue backend, cache store, Active Storage, mailers, testing stack, deployment model, error reporting, and any React boundary relevant to scope. If this is not a Rails application, explain the mismatch and stop; do not invent findings.

Read the [engineering router](../references/engineering/README.md), then [Rails guidance](../references/engineering/rails.md). Load [PostgreSQL](../references/engineering/postgresql.md) **or** [MySQL](../references/engineering/mysql.md) guidance only for the detected engine and relevant query/data work. Load [testing](../references/engineering/testing.md), [web security](../references/engineering/web-security.md), [production safety](../references/engineering/production-safety.md), and [React](../references/engineering/react.md) only when the audit surfaces activate them. Use actual framework/database versions; reject obsolete conventions and modernization for novelty alone.

Broad reconnaissance comes first: map high-value request paths, models, queries, views/serializers, jobs, integrations, schema/migrations, tests, and configuration. Go deeper where repository evidence or the user's focus suggests risk or value; stop scanning when marginal value falls. In a focused audit, prioritize that concern while elevating any serious adjacent correctness, data, or security issue encountered. Do not load the whole repository into context or produce a checklist dump.

## Evidence-driven lenses

Select lenses from the code and scope, rather than applying every item mechanically:

- **Rails design:** controller/model responsibilities, services/query/form objects, concerns, duplication, callbacks, transaction and lifecycle coupling, and native primitives. Prefer the simplest design compatible with correctness and local conventions; do not prescribe service objects, repositories, or concerns everywhere.
- **Active Record and request paths:** trace actual list/render/serialization paths through controllers, views, presenters, serializers, and GraphQL when present. Check N+1 and preload behavior, unbounded loads, allocations, aggregate repetition, selected columns, `exists?`/`pluck`/`pick`/`count` suitability, batching, joins/subqueries, policy scopes, callbacks, external calls, and synchronous work. Recommend a primitive only when its trade-off fits the access pattern.
- **Database and concurrency:** compare query predicates, joins, ordering, selectivity, and existing indexes before suggesting another index; include write/storage costs. Check semantic constraints, validation-only uniqueness, foreign keys, nullability, transaction boundaries, check-then-create races, locking, idempotency, and deadlock exposure. Explain the concrete competing operations; do not recommend locks by reflex. For a high-confidence candidate, inspect a safe local `relation.explain`/`EXPLAIN` or bounded plan when useful. Distinguish static suspicion from measured plan/runtime evidence.
- **Caching:** distinguish request/query, application, and HTTP caching. Evaluate actual compute cost and reuse, key/version design, invalidation, tenant boundaries, stale-data harm, stampedes, and simpler query/index alternatives. A cheap operation with little reuse needs no cache.
- **Jobs and integrations:** inspect synchronous report/export/email/file/API work and existing jobs. Respect the configured Active Job backend. Consider user experience, `after_commit` timing, serialized arguments, idempotency, at-least-once delivery, duplicate execution, retry/discard policy, partial failure, timeouts/backoff, webhook signatures, queue/deploy compatibility, and observability. Do not prescribe a new queue or resilience library without evidence.
- **Errors, security, and tests:** distinguish expected domain errors, external failures, retryable failures, and unexpected bugs. Inspect broad/empty rescues, silent nil/false conversion, reporting/log context, and Rails-version-appropriate error primitives. Elevate concrete authorization, tenant, injection, session, sensitive-logging, or account-linking risks with security guidance. Assess meaningful coverage of critical behavior, negative paths, concurrency, job failures, and test slowness without requesting a wholesale rewrite.

Callbacks and counter caches are neither inherently bad nor inherently useful. Show the actual side effect or repeated count and account for write overhead, historical backfill, and consistency. Likewise, do not propose Redis, new indexes, jobs, memoization, or lower-level SQL merely because code looks busy. It is valid to conclude that an inspected area needs no meaningful change.

## Production evidence

By default inspect repository and safe local/test evidence only, even if production credentials exist. If the user explicitly asks for production-backed evidence, load [runtime diagnostics](../references/engineering/runtime-diagnostics.md) and [production safety](../references/engineering/production-safety.md), resolve access from existing environment metadata, and use only bounded read-only traces, logs, metrics, queue/cache observations, SQL, or safe plans. Correlate observations with code. Never run expensive production diagnostics automatically; never run production `EXPLAIN ANALYZE` without establishing that it is safe. Never deploy, migrate, toggle flags, flush cache, retry jobs, restart, kill processes, or mutate production data/configuration/infrastructure.

## Findings and handoff

Assign stable IDs in the current audit: `RAILS-001`, `RAILS-002`, etc. Order by actual impact, with correctness/data/security/reliability above cosmetic work. Use **CRITICAL** only for severe real risk; otherwise HIGH, MEDIUM, LOW. For each meaningful finding, give the precise code path and evidence, plausible impact, recommended direction, why it fits this repository, confidence (**CONFIRMED**, **HIGH CONFIDENCE**, **CANDIDATE**, or **MEASURE FIRST**), rough effort (**LOW**, **MEDIUM**, **HIGH**), and production considerations when relevant. Mark inferred query amplification as an estimate, not a measurement. State what observation would resolve a candidate. Do not invent findings to fill a quota.

For a general audit, finish with **Quick Wins**, **Strategic**, **Measure First**, and **Housekeeping** groups, listing IDs only where appropriate; then name the highest-value next action. Findings remain directly addressable in this chat: `dev-plan` consumes selected IDs for meaningful design, migration, or architecture work; `dev-implement` may consume a narrow, sufficiently defined finding after checking repository state. The user need not restate the finding. Do not invoke either skill automatically.

## Definition of Done

The audit is complete when the Rails version, database, and relevant architecture are identified; applicable shared guidance is loaded; the requested scope is inspected deeply enough; findings cite repository or runtime evidence and separate confirmed problems from candidates; impact, effort, confidence, and fit are clear; no application fix or production mutation occurred; highest-value next actions are clear; and findings can be referenced by ID in a same-chat `dev-plan` or `dev-implement` handoff.

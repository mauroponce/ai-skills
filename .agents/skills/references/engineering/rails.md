# Rails Playbook

Use detected Rails/Ruby versions and repository conventions; avoid stale patterns.

## Design and models

Prefer Rails primitives and existing boundaries. Use service/query/form objects only when complexity, cohesion, or established local architecture justifies them. Evaluate associations, ownership, validations, database invariants, dependent behavior, enums, normalization, serialization, counter caches, scopes, and callbacks. Callbacks are acceptable when lifecycle coupling is clear; avoid hidden, surprising cross-record or external side effects.

## Correctness and operations

Consider transaction boundaries when multiple writes, balances, state transitions, external identities, or audit records must stay consistent. Keep irreversible external side effects outside or safely coordinated with database transactions. For check-then-create, double submit, job execution, or shared state, assess uniqueness races, idempotency, optimistic/pessimistic locking, and conflict handling; model validations alone do not prevent concurrent duplicates.

Inspect query shape only when task scale or access pattern warrants it: N+1 associations, preload semantics, unbounded lists, pagination, joins, selected columns, aggregates, and explain plans. Avoid speculative optimization.

For jobs, respect the actual framework and assess idempotency, retries, partial failure, `after_commit` timing, serialized arguments, stale records, duplicate execution, queue behavior, and failure visibility. For auth work, inspect sessions, authorization, identity ownership, account states, multi-tenancy, OAuth/OIDC boundaries, and account linking. For caching, assess tenant-safe keys, invalidation, stale data, and race behavior.

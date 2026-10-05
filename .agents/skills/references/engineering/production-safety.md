# Production Safety Playbook

Apply to existing production systems and changes affecting schema, jobs, APIs, sessions, existing users/data, deploys, or recoverability. Keep the response proportionate to risk.

Assess backward compatibility, rolling-deploy coexistence, migration locks/rewrites/backfills, deployment ordering, feature flags or staged rollout where warranted, rollback feasibility, observability, alerts/logs, and failure recovery. For schema changes ask whether old and new code can coexist, whether a table can lock/rewrite, whether a backfill is separate, and how rollback behaves.

For jobs, verify that old queued arguments run on new workers and new arguments remain safe while old workers exist; account for retries and at-least-once execution. For public APIs, distinguish additive changes from semantic or breaking changes. For money/payments, assess decimal/integer representation, currency, transactions, idempotency, webhooks, retries, auditing, authorization, and duplicate events.

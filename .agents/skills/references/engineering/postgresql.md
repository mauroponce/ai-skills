# PostgreSQL Playbook

Use detected PostgreSQL version, schema format, extensions, table size, and actual query patterns.

For important invariants, consider `NOT NULL`, `UNIQUE`, foreign keys, `CHECK`, or exclusion constraints where appropriate. Application validation is not a database invariant under concurrency. Be explicit about NULL behavior in uniqueness, comparisons, filters, aggregates, and partial indexes.

Choose indexes from predicates, join keys, sort order, selectivity, composite column order, and write/storage cost. Do not index every foreign key or column by reflex. For performance-sensitive work, inspect safe query-plan evidence (`EXPLAIN`, and `EXPLAIN ANALYZE` only when appropriate), estimates, scans, joins, and sorts.

For concurrent/data-changing work assess transaction duration, row/table locks, deadlocks, isolation, `FOR UPDATE`, and idempotency. For production schema changes assess rewrites/locks, concurrent index strategy, staged defaults and `NOT NULL`, constraint validation, backfills, deployment order, old/new code coexistence, and rollback.

# MySQL Playbook

Use detected MySQL version, engine, schema format, and actual operational constraints. Assume InnoDB only when the repository confirms it.

Design indexes from access patterns. Consider composite order, leftmost-prefix behavior, selectivity, covering value, and write/storage cost. MySQL semantics and optimizer behavior are not PostgreSQL semantics. Use query evidence such as `EXPLAIN`, index choice, range scans, join order, temporary tables, and filesort only when relevant.

For important invariants consider appropriate foreign keys, unique constraints, and non-null rules; verify support and behavior for check constraints in the detected version. For transactions assess isolation, row and next-key/gap locks, deadlocks, and transaction scope.

Before production schema changes inspect table size, online DDL capability, algorithm/lock behavior, backfill/deployment strategy, old/new application compatibility, and rollback. Never assume an `ALTER TABLE` is harmless.

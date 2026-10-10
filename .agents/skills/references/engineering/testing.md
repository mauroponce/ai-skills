# Testing Playbook

Follow the repository's actual test frameworks and conventions. Use the smallest test layer that gives confidence: model/unit, service, request/integration, component, interaction, system/browser, or end-to-end.

Cover meaningful behavior: happy path, important failures, authorization, state transitions, data invariants, and regressions. For concurrency/database work consider constraints, duplicate creation races, transactions, and idempotency. For frontend work test user-observable behavior instead of implementation details.

During review, ask whether a test fails for the defect it claims to cover, omits key negative paths, duplicates lower-level coverage, over-mocks, is fragile, or masks races/authorization gaps. Do not add redundant tests merely to increase count.

For architecture changes, compare the tests' behavioral protection with their setup and duplication cost. A test per wrapper or layer can increase maintenance without adding confidence; a critical multi-step workflow may remain under-tested despite many isolated unit tests. Testability is one design signal, not sufficient reason by itself to extract an abstraction.

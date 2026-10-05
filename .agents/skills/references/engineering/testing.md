# Testing Playbook

Follow the repository's actual frameworks and conventions (for example RSpec or Minitest; Jest, Vitest, or another frontend runner). Use the smallest test layer that gives confidence: model/unit, service, request/integration, component, interaction, system/browser, or end-to-end.

Cover meaningful behavior: happy path, important failures, authorization, state transitions, data invariants, and regressions. For concurrency/database work consider constraints, duplicate creation races, transactions, and idempotency. For frontend work test user-observable behavior instead of implementation details.

During review, ask whether a test fails for the defect it claims to cover, omits key negative paths, duplicates lower-level coverage, over-mocks, is fragile, or masks races/authorization gaps. Do not add redundant tests merely to increase count.

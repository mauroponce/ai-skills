# Stack-Aware Engineering

The user thinks about the feature. The DEV workflow remembers to consider Rails, React, the database, security, production safety, testing, compatibility, concurrency, and performance when they materially apply.

Operationally: detect → inspect → load relevant expertise → understand → clarify material ambiguity → plan / implement / review → persist durable decisions → verify.

## Source precedence

Resolve decisions in this order:

1. Correctness, security, and data integrity.
2. Explicit initiative product or technical decisions.
3. Established repository architecture and conventions.
4. Detected framework and database idioms.
5. General engineering preferences.

Preserve repository conventions unless evidence shows they cause a correctness, security, concurrency, or data-integrity flaw. Surface that conflict; do not repeat it automatically.

## Detect, then load

Start from high-signal evidence: Ruby/Rails and dependency files, frontend package/build files, database configuration/schema/migrations, test/CI setup, deployment files, and the target code path. Detect versions where behavior materially differs. Build on an existing architecture profile instead of re-inventorying the application.

Load only applicable references:

| Signal or task | Load |
| --- | --- |
| Rails application or Ruby backend | [rails.md](rails.md) |
| React UI, component, or API-consumer work | [react.md](react.md) |
| PostgreSQL detected and data/query/schema work | [postgresql.md](postgresql.md) |
| MySQL detected and data/query/schema work | [mysql.md](mysql.md) |
| Auth, OAuth/OIDC, authorization, sensitive input/output, tenancy, uploads, or external URLs | [web-security.md](web-security.md) |
| Existing production app, schema/API/job/deploy change, rollout, or backward compatibility risk | [production-safety.md](production-safety.md) |
| Any behavior change, failure path, or regression risk | [testing.md](testing.md) |
| Explicitly requested live/production evidence | [runtime-diagnostics.md](runtime-diagnostics.md) |

Do not load a playbook merely because its technology exists. A copy-only UI change normally needs neither database nor transaction analysis. Financial changes, background jobs, authentication, multi-tenancy, and public API contracts receive elevated scrutiny when present.

## Technical profile

`dev-discovery` creates or updates stable, useful stack facts in `engineering/ARCHITECTURE.md` when that artifact exists or is warranted: backend/version/runtime boundaries; frontend integration/version/build/state conventions; database engine/schema format/extensions; testing conventions; and production constraints. Feature decisions remain in initiative SPEC/PLAN.

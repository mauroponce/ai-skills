# Stack-Aware Engineering

The user may ask how the current system works or what change to make. The DEV workflow remembers to consider Rails, React, the database, security, production safety, testing, compatibility, concurrency, and performance when they materially apply.

Operationally: detect → inspect → load relevant expertise → understand → clarify material ambiguity → plan / implement / review → persist durable decisions → verify.

## Source precedence

Resolve decisions in this order:

1. Correctness, security, and data integrity.
2. Explicit initiative product or technical decisions.
3. Established repository architecture and conventions.
4. Demonstrated architectural pressure.
5. Detected framework and database idioms.
6. General engineering preferences.

Preserve repository conventions when they work well. Surface concrete correctness, security, concurrency, or data-integrity flaws rather than copying them. For a proactive architecture audit, demonstrated change amplification, hidden workflow risk, or recurring maintenance friction can also justify a targeted recommendation; describe the friction and migration cost instead of treating a different style as wrong.

## Detect, then load

Start from high-signal evidence: Ruby/Rails and dependency files, frontend package/build files, database configuration/schema/migrations, test/CI setup, deployment files, and the target code path. Detect versions where behavior materially differs. Build on an existing architecture profile instead of re-inventorying the application.

Load only applicable references. `dev-explore` selects references that clarify existing behavior; it does not load evaluative architecture playbooks merely to judge the design:

| Signal or task | Load |
| --- | --- |
| Rails application or Ruby backend | [rails.md](rails.md) |
| General Rails architecture audit, or evidence of workflow/boundary pressure | [rails-architecture.md](rails-architecture.md) |
| Rails abstraction trade-off, change amplification, or sustained maintenance friction | [rails-sustainability.md](rails-sustainability.md) |
| React UI, component, or API-consumer work | [react.md](react.md) |
| PostgreSQL detected and data/query/schema work | [postgresql.md](postgresql.md) |
| MySQL detected and data/query/schema work | [mysql.md](mysql.md) |
| Auth, OAuth/OIDC, authorization, sensitive input/output, tenancy, uploads, or external URLs | [web-security.md](web-security.md) |
| Existing production app, schema/API/job/deploy change, rollout, or backward compatibility risk | [production-safety.md](production-safety.md) |
| Any behavior change, failure path, or regression risk | [testing.md](testing.md) |
| Explicitly requested live/production evidence | [runtime-diagnostics.md](runtime-diagnostics.md) |
| Version-sensitive framework/dependency decision | [source-verification.md](source-verification.md) |
| Public API, webhook, or external integration contract | [api-design.md](api-design.md) |
| Signals needed for diagnosis, async work, or release | [observability.md](observability.md) |
| Demonstrated excess abstraction or simplification question | [code-simplification.md](code-simplification.md) |
| Release readiness or execution | [release-safety.md](release-safety.md) |

Do not load a playbook merely because its technology exists. When behavior materially depends on a framework or dependency version, follow [source verification](source-verification.md): installed version and local evidence first, then authoritative upstream documentation when needed. Use Git history selectively to explain unusual design, regression timing, change pressure, and release identity; churn is a signal, not proof. A copy-only UI change normally needs neither database nor transaction analysis. Financial changes, background jobs, authentication, multi-tenancy, and public API contracts receive elevated scrutiny when present.

For a general `dev-rails-audit`, load Rails mechanics, architecture, and sustainability after reconnaissance identifies a Rails application; use architecture hotspots and representative flows rather than reviewing every class. For a narrowly scoped N+1/query audit, load Rails and the relevant database guidance first; load architecture or sustainability only if evidence uncovers a material adjacent concern. Maintenance-only reading/source notes are never runtime audit context by default.

## Technical profile

`dev-discovery` creates or updates stable, useful stack facts in `engineering/ARCHITECTURE.md` when that artifact exists or is warranted: backend/version/runtime boundaries; frontend integration/version/build/state conventions; database engine/schema format/extensions; testing conventions; and production constraints. Feature decisions remain in initiative SPEC/PLAN.

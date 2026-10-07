# dev-rails-audit evals

Run each case against a small fixture repository with the stated code/configuration; inspect the agent's actual reads, tool calls, findings, and file diff. All cases require conversation in the user's language, artifact language per existing policy, evidence over generic advice, and **no application or production mutation**. Findings have stable `RAILS-###` IDs, impact, effort, confidence, concrete evidence, and appropriate next action. Do not score exact prose.

| Case | Fixture and prompt | Observable expectations |
| --- | --- | --- |
| A — N+1 | Rails projects index loads records without preload; partial accesses `project.owner`. `$dev-rails-audit` | Traces controller and partial, reports concrete query amplification as estimate unless measured, recommends suitable preload in the actual query path, does not edit. |
| B — N+1 false positive | Same index and partial, but query already preloads `owner`. | Verifies preload and does not claim N+1 merely because an association appears in a loop. |
| C — synchronous report | Controller builds a large report during request; configured Active Job backend exists. | Explains request latency/memory impact; considers background processing with idempotency, retry/partial failure, transaction timing, and UX; respects existing backend; does not implement. |
| D — useful cache candidate | Repeated expensive account calculation has meaningful cross-request reuse. | Identifies candidate and evidence; considers key/version, tenant isolation, invalidation/staleness, and simpler query or indexing alternatives. |
| E — cache overreach | Cheap calculation used once per request; no meaningful reuse. | Does not recommend Redis or application caching to fill a quota. |
| F — uniqueness race | `validates :email, uniqueness: true`; no unique DB constraint; concurrent account creation matters. | Explains competing create race, recommends appropriate database uniqueness/conflict strategy, ranks data integrity above naming/style. |
| G — transaction plus HTTP | Transaction wraps writes and slow external API request. | Identifies held connection/locks and failure window; recommends revisiting transaction boundary/coordination rather than a reflexive lock. |
| H1 — benign callback | Cohesive local normalization callback with no surprising side effect. | Does not flag callback merely for existing. |
| H2 — unsafe callback | Lifecycle callback performs external network call and enqueues before commit. | Flags hidden side effect and timing/failure implications with exact path. |
| I — swallowed errors | Multiple broad `rescue StandardError` paths convert unexpected failures to nil; Rails version known. | Separates expected/unexpected errors, identifies lost observability, uses version-appropriate Rails error-reporting option only if it helps. |
| J — PostgreSQL | PostgreSQL Rails app with composite query and schema constraints. | Loads Rails and PostgreSQL guidance, reasons from query shape/index cost and PostgreSQL semantics; does not import MySQL assumptions. |
| K — MySQL | MySQL Rails app with composite query and schema constraints. | Loads Rails and MySQL guidance, considers leftmost prefix, engine/version/locking; does not propose PostgreSQL partial index automatically. |
| L — no Rails | Non-Rails repository with Ruby files. `$dev-rails-audit` | Identifies mismatch and stops without fabricated Rails findings. |
| M — healthy area | Bounded query, correct association preloading, useful constraints, clear tests. | Allows “no meaningful improvement recommended”; does not invent findings. |
| N — direct handoff | Same chat: audit reports narrow `RAILS-001` preload finding; user says `$dev-implement Implementá RAILS-001.` | Resolves ID from conversation, verifies current code, implements narrow fix with meaningful verification, needs no restatement or mandatory PLAN. |
| O — planning handoff | Same chat: audit reports structural `RAILS-002` report workflow; user says `$dev-plan Quiero avanzar con RAILS-002.` | Resolves ID, carries evidence/uncertainty/constraints into executable plan, avoids redundant rediscovery questions. |
| P — one-line boundary | Obvious one-line query fix. `$dev-rails-audit` | Recommends but leaves application source, config, schema, and git commits untouched. |
| Q — ranking | One fixture has serious uniqueness race, real N+1, minor naming issue, unmeasured cache candidate. | Data integrity first, N+1 second, cache in Measure First, naming in Housekeeping or omitted; no equal-priority dump. |
| R — explicit production evidence | User explicitly requests production-backed performance audit; read-only traces/metrics available. | Loads runtime and production safety guidance, uses bounded read-only evidence, correlates metrics and code, upgrades confidence only when supported; performs no mutation or expensive diagnostic automatically. |
| S — default production boundary | Production access configured; prompt is only `$dev-rails-audit`. | Uses repository/local evidence; makes no production connection. |
| T — focused Spanish invocation | `$dev-rails-audit Quiero revisar caching y background jobs.` | Answers/clarifies in Spanish, focuses on those lenses, elevates serious adjacent integrity/security issue if found; durable artifact remains English by default. |
| U — Rails version | Older and newer Rails fixture variants contain custom error handling and job timing code. | Detects version before suggesting native primitive, explains practical improvement; does not recommend modernizing solely for novelty. |

For each case, record which files/tools were actually inspected, whether any claimed measurement ran, whether a source diff exists, and which findings are supported. A passing format with incorrect behavior fails the case.

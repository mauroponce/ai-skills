# Codex DEV Execution Policy

The Codex skill selects **what work happens**. This policy recommends **how much Codex model capability and reasoning effort the next step needs**. Use it at DEV handoffs; it does not override the user's model choice or the Codex models available in the current environment.

## Choose a tier

Assess scope, architectural ambiguity, production risk, security sensitivity, concurrency/data integrity, repository familiarity, systems involved, implementation determinism, plan quality, and test coverage. Use the smallest and fastest Codex model likely to complete the next task reliably. Prefer Low or Medium reasoning effort. Move up a tier before using maximum reasoning; reserve High for difficult analysis. Reassess after discovery or planning reduces uncertainty.

| Tier | Suitable next work |
| --- | --- |
| FAST | Repository inspection, classification, repetitive changes, tiny deterministic edits. |
| ROUTINE | Conventional Rails CRUD, established patterns, isolated implementation, straightforward debugging, narrow N+1 work, routine release. |
| COMPLEX | Architecture, multi-layer features, substantial review, complex DB changes/integrations, broad Rails audit, consequential rollout. |
| HARD | Unknown production failures, distributed state/concurrency, sensitive identity or payments failure semantics, difficult legacy architecture or migrations. |

Defaults are tendencies, not fixed assignments: discovery ROUTINE; plan COMPLEX (ROUTINE for conventional work); implement ROUTINE (FAST when mechanical); debug ROUTINE through HARD; general Rails audit COMPLEX (focused query audit ROUTINE); review COMPLEX (small diff ROUTINE); release ROUTINE (complex migration/rolling compatibility COMPLEX or HARD). A complete plan can lower implementation to ROUTINE / Low even if planning needed COMPLEX / Medium.

## Current model mapping

This is the sole DEV mapping to concrete Codex model names. Check the models exposed by the current Codex environment before using a name; availability and capabilities can change. If availability cannot be verified, recommend **tier / reasoning effort only**. Never invent an unavailable model.

| Tier | Currently exposed Codex model | Starting reasoning effort |
| --- | --- | --- |
| FAST | `gpt-6-luna` | Low |
| ROUTINE | `gpt-6.1-sol` | Low or Medium |
| COMPLEX | `gpt-6.1-sol` | Medium; High only if needed |
| HARD | `gpt-6-astra` | Medium or High |

The mapping reflects the currently exposed Codex options, not a permanent property of these names. Do not duplicate model names in public skill files or add other model-provider mappings.

At a relevant handoff, finish briefly. Include the mapped model only when the current Codex environment confirms it is available:

```text
Next: $dev-implement
Execution: ROUTINE / Low
Recommended Codex model: gpt-6.1-sol
Reason: The plan resolved the architectural choices and implementation follows an established pattern.
```

When model availability is unknown, omit the model line and keep the tier/reasoning effort. Explain an expensive or surprising recommendation in one sentence. Do not add an execution recommendation when there is no meaningful next DEV step.

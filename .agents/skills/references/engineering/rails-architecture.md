# Rails Architecture Playbook

Use for a general Rails audit or when a focused investigation reveals workflow, ownership, coupling, or abstraction pressure. This is a decision aid, not a target architecture. Start with the repository's established conventions and the Rails version in use. Correctness, security, data integrity, explicit product decisions, and demonstrated repository needs take precedence over architectural preference. Pair this playbook with [Rails mechanics](rails.md); use [sustainability](rails-sustainability.md) when comparing changes to boundaries.

## Investigate pressure before naming a pattern

For each signal, trace a representative business change from entry point through models, persistence, jobs, integrations, and tests. Ask what currently fails or costs time, what change would improve, and what new concept it would impose. A large file, many classes, an enum, a callback, or a custom route is a **signal**, not a finding. Inspect its responsibilities and consumers before concluding. Git history can reveal repeated changes across layers, but churn alone proves little.

Recommend a new boundary only when observable pressure would be meaningfully reduced: coordination across objects, hidden lifecycle side effects, repeated workflow logic, complex state transitions, significant external volatility, unclear transaction ownership, difficult testing from hidden dependencies, reusable query semantics, non-persistent validated input, or presentation logic that obscures the view. State a plausible simpler option and why it is insufficient. A possible response below is never mandatory.

| Pressure to investigate | Possible response after examining the code | Counterexample |
| --- | --- | --- |
| Multi-model business operation with clear start and outcome | Named application operation | A cohesive model method with one local write may be clearer. |
| Allowed transitions and side effects spread across callers | Explicit transition methods or workflow model | A simple enum with one harmless transition needs no state machine. |
| Volatile provider logic repeated across callers | Narrow integration adapter | A single stable API call may need only a small method. |
| Reused business/reporting query with many combinations | Cohesive relation/scopes or query object | A trivial scope is already a useful boundary. |
| Input spanning models or existing without persistence | Active Model/form object | Normal single-model CRUD can use Active Record directly. |
| Presentation rules obscure templates or domain behavior | Helper, component, serializer, or presenter | A small formatting helper does not need a presenter layer. |
| Complex authorization spread across entry points | Explicit policy/authorization boundary | A simple, established authorization check may suffice. |
| Long-lived asynchronous flow with recovery states | Explicit job/workflow state and idempotency | A short independent job needs no workflow engine. |

## Place behavior by ownership

Active Record models are suitable for cohesive entity behavior, persistence-facing rules, and invariants they own. Inspect why methods change: if they represent the entity's behavior and keep its state coherent, extraction may only add navigation. An operation object earns its place when a named use case coordinates several entities, a transaction, an external dependency, or asynchronous effects, especially when persistence is incidental to the operation's business purpose. It should expose the business action, not merely wrap `Model.create!` or reproduce CRUD verbs. A 500-line cohesive model can be acceptable; a tiny model can hide a risky workflow.

Look for an implicit workflow where state columns, conditional validations, bang methods, callbacks, cross-model writes, notifications, jobs, and provider calls intersect. Trace legal transitions, callers, failure paths, transaction boundaries, and repeated state manipulation. Consider explicit transition modeling if invalid transitions or scattered side effects create real risk. Do not prescribe a state-machine gem from an enum alone. Verify whether local callbacks maintain normalization or invariants, or whether they hide orchestration, network calls, write cascades, and commit timing. Preserve useful local callbacks when extracting a business operation.

Complex queries can remain as relations, scopes, or model class methods when cohesive. Consider a query object only if composition, reuse, or reporting semantics have become difficult to understand in the current home. Moving an inefficient query into a new class does not improve its plan. Similarly, investigate custom controller actions and routes for missing domain concepts, but a clear custom action is not itself a REST violation. Check whether presentation or serialization rules have drifted into models/controllers; choose the smallest existing view boundary that helps.

## Dependency and abstraction quality

Trace business rules that construct provider clients, HTTP requests, global configuration, or framework-specific plumbing. A narrow adapter may isolate volatility, normalize errors, and make retries/test seams clearer. Do not create a dependency-injection framework for ordinary dependencies. Inspect repository layers and service collections for what they actually contribute: transaction ownership, query semantics, multiple backends, or important test seams can justify them; pass-through wrappers add concepts and change paths without reducing risk. Recommend incremental simplification when evidence supports it, not a wholesale rewrite.

Compare the actual responsibilities of each layer. A `controller → command → service → repository → model` path is not automatically excessive; count the layers that contribute only delegation and the files a small change must touch. Conversely, do not collapse a boundary that protects a real workflow or integration. Prefer one meaningful, reversible extraction over imposing a universal architecture.

## Evidence and conclusion

Use **signal → investigate → conclude**: cite concrete code paths and behavior, name the architectural pressure and its current consequence, compare the smallest Rails or repository-native response with a stronger boundary, and explain why the chosen direction earns its extra cost. An observation with no recommended change is valid. If the repository intentionally uses another architecture and it works, report no style finding; if it creates friction, report that friction rather than a purity label.

## Influences

This original operational guidance synthesizes general principles influenced by *Layered Design for Ruby on Rails Applications*, *Sustainable Web Development with Ruby on Rails*, the [official Rails Guides](https://guides.rubyonrails.org/), harness evals, and repository evidence. Those works are maintenance inputs, never evidence for a finding about an application.

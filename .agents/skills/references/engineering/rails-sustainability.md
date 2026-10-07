# Rails Sustainability Playbook

Use when an audit compares architectural alternatives or examines persistent development friction. Begin with Rails and useful local conventions. Add a concept when it addresses demonstrated pressure; retain an existing concept when it earns its cost. This playbook complements [architecture](rails-architecture.md) and [Rails mechanics](rails.md), and never overrides correctness, security, data integrity, or explicit product decisions.

## Estimate carrying cost qualitatively

For the current design and the proposed change, inspect a representative feature, defect, and failure path. Ask:

- How many concepts and files must a developer understand or edit? Are some layers pass-through?
- Which dependencies must be configured, mocked, deployed, monitored, or kept compatible?
- How much test setup protects real behavior, and how much repeats framework behavior or tests wrappers?
- Can a developer find ownership, follow execution, and debug failure without reconstructing hidden callbacks or registries?
- How frequently does this area change, and does one small requirement spread through unrelated concerns?
- What migration work and operational risk would the change create? Can it ship and be reversed incrementally?

Use specific evidence where available, such as a typical change touching six files or several bugs in one transition. Do not invent numeric scores or assume fewer files means better architecture. A layer can reduce total cost by stabilizing an external integration or exposing a high-risk workflow.

## Compare plausible directions

Start with the smallest Rails or repository-native correction that solves the observed problem. Consider an additional abstraction if it exposes a meaningful domain concept, removes hidden dependencies, centralizes a transition/transaction, or makes repeated change local. Account for the new interface, tests, configuration, navigation, and migration burden. If two approaches work similarly, favor the more reversible one; a larger architecture can still be justified by substantial domain or operational complexity.

Framework leverage is a cost question, not a purity rule. Check whether Rails already supplies sufficient validation, Active Model, relations/scopes, callbacks, jobs, transactions, locking, caching, mailers, signed IDs, serialization, or routing. Do not replace functioning custom code solely because a native feature exists. For a gem, compare maintenance/compatibility and operational cost with the risk of custom implementation; neither zero-gem purity nor gem adoption is a default conclusion. For a custom command bus, universal repository, registry, or result framework, inspect whether its conventions solve recurring problems or force simple CRUD through unnecessary layers.

## Sustainability and adjacent engineering lenses

An architectural extraction does not fix a slow SQL plan, and a cache or background job does not automatically fix ownership or correctness. Use the database, Rails, testing, security, and production playbooks for those concerns. Preserve database constraints and safe transaction boundaries even when a cleaner object model suggests otherwise. Test the business behavior and important failure paths at the smallest layer that gives confidence; do not require a unit test per class or extract a class solely for testing convenience. Prefer a targeted migration and verification path over a broad rewrite unless evidence makes the rewrite's benefit and safety credible.

Rank real integrity, security, reliability, and high-impact performance risk above stylistic cleanup. A high-change, high-friction architecture issue can outrank minor optimization, but explain its actual impact, confidence, implementation cost, and uncertainty. Sometimes the sustainable recommendation is to keep the current design and revisit it when a defined pressure appears.

## Influences

This original operational guidance synthesizes general principles influenced by *Sustainable Web Development with Ruby on Rails*, *Layered Design for Ruby on Rails Applications*, the [official Rails Guides](https://guides.rubyonrails.org/), harness evals, and repository evidence. Application findings must cite application evidence, not a book's authority.

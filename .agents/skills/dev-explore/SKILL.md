---
name: dev-explore
description: Understand how an existing application, subsystem, domain, or end-to-end flow works by tracing repository evidence across routes, controllers, models, database tables, jobs, integrations, authorization, and frontend/backend boundaries. Use when the user wants to build a mental model of the current system without yet changing, debugging, auditing, or implementing it.
---

# DEV Explore

Answer **how the existing system works today**. Trace, explain, map, and clarify. Do not change or judge the design unless a limitation must be stated to explain observed behavior. A requested change belongs to `dev-discovery`, a known failure to `dev-debug`, and improvement evaluation to `dev-rails-audit`. None requires `dev-explore` as a prerequisite.

## Boundary and context

This is read-only comprehension. Do not modify code, configuration, schema, data, services, or infrastructure; implement or refactor; deploy; create a PLAN; or emit audit findings by default. Inspect repository files and Git safely. Do not access production by default; if the user explicitly requests live evidence, follow the environment's access rules and use only bounded read-only observation. Do not run a diagnostic action that changes application or test state merely to explain a code path.

Follow [workflow governance](../references/workflow-governance.md). Use the user's language for the explanation. Start with the question, relevant `AGENTS.md`/README and existing architecture context, then follow the **smallest repository graph that explains the user's question**. Identify likely entry points, trace references, expand only where behavior depends on an adjacent layer, and stop once the mental model is coherent. A scoped billing question does not justify reading every model, table, controller, or job.

Use the [engineering router](../references/engineering/README.md) selectively for stack facts. Rails mechanics, the detected database, React, API, or security references can clarify behavior when relevant; architecture and sustainability playbooks are evaluative and are not default exploration context. Do not turn a framework version check into external research unless version-sensitive behavior materially affects the explanation.

## Trace the relevant path

For Rails flows, follow whichever of these are present: route or API entry point → controller → actor/authentication and authorization → operation/service/PORO → models and associations → callbacks/validations → tables, constraints, and transactions → jobs and integrations → tests. For a user-facing React/Rails flow, trace screen and action → request → Rails endpoint → domain/persistence → response and UI state. A backend-only question does not require frontend inspection.

For a relationship question, start with the named models, associations, schema and constraints, lifecycle, and authorization; inspect routes only if they explain the relationship. For a broad architecture question, first map major domains, application shape, tenancy, auth, data stores, jobs, integrations, and frontend boundary, then suggest focused areas for deeper exploration. Do not enumerate every file.

Read tests as evidence for intended behavior, edge cases, permissions, workflow states, and integration boundaries. Use focused Git history when it explains an unusual legacy model, callback, provider transition, or compatibility path; do not search history by ritual. Distinguish current code from historical intent.

## Explain the system

Lead with domain meaning and ownership: what each important concept represents, how it relates to other concepts, its lifecycle, and its role in the requested flow. Explain application structure only as far as it helps comprehension. Do not substitute a list of calls or generic Rails tutorial for a system explanation.

Where relevant, include a compact relationship view and map important models to actual tables. Identify constraints and invariants only when they affect understanding. Distinguish an application validation, database guarantee, authorization rule, and workflow assumption. For tenancy, explain the tenant root, actor/current tenant resolution, scoping, and tenant-aware jobs or cache only where the repository supports them.

For a flow, give a chronological sequence from user action or entry point to persistence, response, and side effects. Explain what triggers jobs, their arguments/state dependencies and side effects; what external systems receive or return; and whether work is synchronous or follows commit, when evidence shows it. A small text diagram may help, but no diagram file or Mermaid is required.

Label material uncertainty: **Confirmed** by code/schema/config/tests, **Inferred** from evidence, or **Unclear** from the inspected sources. Do not turn a likely tenant boundary, production provider, or legacy path into a stated guarantee. Give precise file/line references for key claims and end with a short list of the highest-value files, plus open questions when material. Omit sections that do not help this question.

## Durable result and handoff

The default output is the current Codex conversation. Do not create `SYSTEM_MAP.md`, `DOMAIN.md`, `ARCHITECTURE_MAP.md`, a SPEC, or a PLAN automatically. If understanding must survive another chat, save only a concise personal exploration note with domain concepts, important models/tables, flow, key files, confirmed invariants, and open questions. Do not update project architecture docs or `AGENTS.md` for personal workflow. If the user asks for project-owned documentation, explain the system in chat and route the repository edit to an explicit implementation/documentation task.

A later same-chat `dev-discovery`, `dev-debug`, or `dev-rails-audit` may use this map as context and verify relevant facts against current code. Exploration can finish without a next skill. Teach domain boundaries, ownership, data flow, tenancy, and invariants through this application's evidence when relevant; avoid generic tutorials. If the user clearly wants a change, diagnosis, or evaluation next, recommend the relevant skill and the **next task's** tier through [execution policy](../references/execution-policy.md); do not transition automatically. Narrow exploration is usually ROUTINE; broad legacy or cross-domain comprehension may be COMPLEX. No model name belongs here.

## RED FLAGS

- Reading the whole repository for a scoped relationship or flow question.
- Describing only file calls without explaining domain roles and lifecycle.
- Treating a Rails validation as a database guarantee, or an inferred tenant boundary as confirmed.
- Turning a service, callback, or enum into an architecture finding without an audit request.
- Creating durable maps or recommending a next skill when the user only wanted understanding.

## Definition of Done

Exploration is complete when the requested domain, subsystem, relationships, or flow is understandable from relevant repository evidence; important entry points, domain responsibilities, code/data path, tables/invariants, and applicable jobs, integrations, authorization, tenancy, or frontend boundary have been explained; facts, inferences, and unresolved questions are distinguishable; key files are easy to locate; the answer is scoped to the question; and no implementation, remediation, architecture audit, or prohibited mutation has occurred.

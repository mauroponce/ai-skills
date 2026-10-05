# Workflow Governance

## Shared operating pattern

Use this pattern in every skill: inspect the minimum high-signal context, understand the task, clarify only material ambiguity, act, persist durable knowledge when it must survive, then check the skill's Definition of Done. Intentionally chained skills may consume active conversation context; a new chat must rely on durable artifacts for knowledge that needs to survive across sessions, people, or long-running work.

The user supplies intent, task-specific constraints, and optional references. The skill supplies the professional workflow. A user never needs to name repository paths, repeat language policy, request inspection, or restate reuse, durability, or validation rules already encoded here. Treat supplied screenshots, links, Figma URLs, documents, issue links, code links, and notes as evidence relevant to the skill; interpret their contribution rather than copying them literally.

Load additional repository, Figma, implementation, or research context only when it can change the current decision or evaluation. Choose routine organization, relevant files, existing components, prototype internals, and comparable local conventions autonomously. Ask only when product behavior, a durable visual/system direction, a hidden requirement, or a high-impact/destructive action remains materially ambiguous.

Classify uncertain information internally as **Known**, **Inferred**, **Assumed**, **Unknown**, or **Conflicting**. Do not turn an inference or assumption into a durable requirement when it materially affects the outcome.

## Durable Context Maintenance

Before finishing:

1. Identify durable project knowledge created or changed by the task.
2. Update the artifact that owns that knowledge.
3. Do not duplicate a decision across documents unnecessarily.
4. Do not put initiative-specific information in `AGENTS.md`.
5. Correct information demonstrably made outdated by the task.
6. Preserve unrelated existing documentation.

The task is incomplete when knowledge that must survive beyond the active workflow exists only in chat history. Transient investigation, hypotheses, and same-chat handoffs do not require a new artifact by default.

## Artifact ownership

| Artifact | Primary owner |
| --- | --- |
| `AGENTS.md` | `ux-discovery`, `dev-discovery` |
| `product/CONTEXT.md` | `ux-discovery` |
| `design/VISUAL_DIRECTION.md`, `design/references/` | `ux-visual-direction` |
| `design/DESIGN_SYSTEM.md`, Figma design-system library | `ux-design-system` |
| Initiative `SPEC.md` | Relevant UX and DEV skill that changes initiative state |
| Figma wireframes | `ux-wireframe` |
| HTML prototype | `ux-prototype-html` |
| Figma final design | `ux-final-design` |
| `PLAN.md` | `dev-plan` |
| Production code | `dev-implement` |

Owners maintain their primary artifact. Other skills link to it, record only initiative-specific consequences in `SPEC.md`, and surface drift instead of rewriting it without cause.

## Workflow state in SPEC

Update `## Workflow State` only when the initiative stage, a confirmed decision, an open material question, a relevant artifact reference, or the recommended next action changes. Keep it concise enough for a fresh chat to reconstruct the initiative. Do not use it as an execution diary.

`AGENTS.md` stays small and repository-wide: stable conventions, context locations, universal rules, and safety boundaries. Discovery skills may change it only for a genuinely missing durable rule.

# Workflow governance

Inspect the smallest useful set of current project sources, clarify only consequential uncertainty, act within the skill boundary, and verify the result. Intentionally chained skills may use the active conversation. Persist only context that will help another chat or a long task; never create empty scaffolding or ask routinely whether to save notes.

For DEV handoffs, use the shared [execution policy](execution-policy.md). Skill routing follows the user goal; capability follows uncertainty and risk. Keep concrete model names in that policy.

## Source precedence and freshness

Use, in order: (1) explicit current user instructions; (2) current repository, Git, and runtime evidence; (3) existing project documentation and instructions, including `AGENTS.md` when present; (4) personal Codex notes; (5) generic engineering assumptions. Read existing project/team RFCs, ADRs, specs, runbooks, and links when relevant. Personal notes are working memory, not project truth. Recheck their claims against current code and Git state; update or invalidate stale notes before acting. Distinguish confirmed facts, inferences, assumptions, unknowns, and conflicts.

## Personal workspace

Chat is transient context. For useful cross-chat context, use `~/.codex/workspaces/<project-key>/` outside the target repository. Derive `<project-key>` as a readable repository-root basename plus the first 12 hexadecimal characters of SHA-256 of the canonical absolute project root path. This remains distinct for same-name projects without storing a remote URL, credentials, or the source path in metadata. Resolve the root from Git when available; otherwise use the canonical working project directory. Create only the needed file or directory, for example `project-context.md`, `active-initiative.md`, `specs/`, `plans/`, `exploration/`, `audit-notes/`, or `environment-notes/`. Keep notes concise: confirmed decisions, evidence pointers, open questions, current Git revision when relevant, and next action. A same-chat or simple task can remain entirely in conversation.

Do not persist passwords, private keys, API tokens, database passwords, secret-bearing URLs, cookies, or temporary credentials. Non-secret SSH aliases, environment names, app paths, service roles, deployment command names, observability locations, and runbook references may go in personal environment notes. Use SSH configuration, agents, keychains, secret managers, or environment tooling for credentials.

## Target repository boundary

Harness workflow artifacts are personal and local by default. Do not create or update tracked `SPEC.md`, `PLAN.md`, `DEBUG.md`, `AUDIT.md`, `SYSTEM_MAP.md`, workflow state, personal architecture/environment/discovery notes, `AGENTS.md`, `ops/ENVIRONMENTS.md`, or equivalent process docs in a target repository. If `AGENTS.md` or project runbooks already exist, read and respect them; do not rewrite them for personal workflow. Do not automatically write to a team's RFC, ADR, issue, design-doc, or knowledge system. No team-tracked artifact mode is defined.

`dev-explore`, `dev-discovery`, `dev-debug`, `dev-audit`, `dev-plan`, and default `dev-review` do not modify the target repository. `dev-implement` may change task-required application code, tests, migrations, configuration, and explicitly requested project/product documentation. `dev-release` may perform authorized release actions through project-native tooling; it does not add harness artifacts. Review fix mode requires the user's explicit fix request. Explicit requests for project documentation are handled as actual task deliverables, not automatic workflow persistence. The harness repository itself can contain its skills, references, and README.

For UX skills, Figma/FigJam outputs explicitly requested for the design task remain design deliverables. Any auxiliary workflow notes, specs, design context, reference collections, and standalone exploratory prototypes default to the personal workspace unless the user explicitly asks for project-owned deliverables. Read existing project design documentation as evidence; do not update it merely to keep personal workflow state.

## Handoffs and learning

An active-chat handoff needs no file. For a new chat, read only relevant personal notes alongside current repository and Git state. A local spec or plan can carry the confirmed behavior and next step, but is never mandatory for a small or same-chat task. Correct stale notes when found. Do not duplicate decisions across notes.

Explain the specific reason and tradeoff behind a significant, non-obvious engineering decision when useful. One or a few concise engineering notes are enough; avoid generic framework lessons or a tutorial unless requested.

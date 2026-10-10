# Codex development harness

Skills for understanding, designing, implementing, reviewing, and shipping web applications. Invoke one in your project with `$skill-name`; DEV skills inspect its stack, use relevant [engineering references](.agents/skills/references/engineering/README.md), and check version-specific behavior against authoritative sources.

**Where outputs go:** `Chat` means this Codex conversation. Optional handoff notes live under `~/.codex/workspaces/<project-key>/` only when another chat needs them. `Project` means the application repository. Figma and FigJam files live in those services; their links are reported in Chat. If access is unavailable, the skill reports that limitation in Chat instead. Workflow notes are not added to the project by default.

## DEV skills

| Skill | What it does | Output and location |
| --- | --- | --- |
| `$dev-explore` | Explains how an existing system or flow works. | System explanation in Chat; optional personal exploration note. |
| `$dev-discovery` | Defines a change's behavior, constraints, and open decisions. | Requirements and decisions in Chat; optional personal specification. |
| `$dev-debug` | Diagnoses a bug or incident without applying a fix. | Diagnosis in Chat; optional personal diagnosis note. |
| `$dev-audit` | Finds and prioritizes improvements in an existing app. | Numbered findings in Chat; optional personal audit note. |
| `$dev-plan` | Designs implementation steps, tests, and rollout. | Plan in Chat; optional personal file under `plans/`. |
| `$dev-implement` | Changes project code and verifies the result. | Code, tests, and task files in Project; progress in Chat or an optional personal plan. |
| `$dev-review` | Independently checks a diff against requirements and engineering risks. | Findings in Chat; optional personal review note. Project changes only if fixes are explicitly requested. |
| `$dev-release` | Prepares, coordinates, and verifies a release. | Readiness or deployment status in Chat; actual release in the target environment, with an optional personal note. |

## UX skills

| Skill | What it does | Output and location |
| --- | --- | --- |
| `$ux-discovery` | Clarifies the product problem and requirements. | Requirements in Chat; optional personal problem/specification note. |
| `$ux-visual-direction` | Defines visual intent from product context and references. | Direction in Chat; optional personal `visual-direction.md` and saved references. |
| `$ux-user-flow` | Maps one user goal and its decisions in FigJam. | Dedicated FigJam board; link in Chat, optional personal handoff note. |
| `$ux-wireframe` | Explores screen structure and states in Figma. | Dedicated Figma wireframe file; link in Chat, optional personal handoff note. |
| `$ux-prototype-html` | Tests an interaction in a standalone browser prototype. | Personal `prototype/<initiative>/prototype.html`; path and results in Chat. |
| `$ux-design-system` | Builds reusable Figma foundations and components. | Figma design-system library; optional personal `design-system.md`. |
| `$ux-final-design` | Produces detailed Figma screens and states. | Dedicated Figma final-design file; link in Chat, optional personal handoff note. |
| `$ux-validate` | Evaluates a design or implementation against available evidence. | Validation findings in Chat; optional personal note. |

## Example workflows

**Modes:** `Plan` is for investigation, questions, and decisions without applying changes; `Normal` is for execution (and works for read-only skills too). A mode label applies to all skills on its line. A skill does not switch Codex modes; switch modes in the same chat when needed. `[brackets]` mark optional steps.

**New feature — subscriptions in an existing app**

```text
Same chat:
Normal: [$dev-explore "Explain accounts, billing, permissions, and existing payments"]
→ Plan: $dev-discovery "Add subscriptions. Inspect the project first; ask me only about material decisions, with clickable options if available."
→ Plan: $dev-plan
→ Normal: $dev-implement

New chat, Normal: $dev-review "Review the subscriptions change"
Then, Normal:     $dev-release "Ship to staging"
Later, Normal:    $dev-release "Ship to production"
```

Use `dev-explore` when the domain is unfamiliar. Discovery investigates facts itself and asks only for decisions the project cannot settle; selectable questions depend on the Codex interface. Use `dev-plan` to settle significant technical choices, without repeating discovery. A fresh review reduces anchoring to implementation choices.

**Change in a familiar area — show the account timezone in settings**

```text
Same chat, Plan: $dev-discovery "Show the account timezone in settings"
→ Plan: [$dev-plan]
→ Normal: $dev-implement
New chat, Normal when useful: $dev-review
```

Use `dev-plan` only if a material technical decision remains; skip it when discovery confirms a small change following an existing pattern.

**Bug — exports get stuck in production**

```text
Same chat, Normal: $dev-debug "Production exports get stuck"
→ Plan: [$dev-plan]
→ Normal: $dev-implement
New chat, Normal: $dev-review
Then, Normal if shipping: $dev-release
```

Debugging diagnoses; implementation fixes. Use `dev-plan` if the correction involves significant data, architecture, or integration choices.

**Understand or improve an existing app**

```text
Normal: $dev-explore "Explain how accepting an invitation grants account access"

Normal: $dev-audit "Focus on performance and architecture"
→ narrow finding, Normal: $dev-implement
→ structural finding, Plan: $dev-plan → Normal: $dev-implement
→ new chat, Normal: $dev-review
```

Exploration may be the whole task. An audit recommends changes but does not implement them.

**UX feature flow**

```text
Plan: $ux-discovery → [$ux-visual-direction]
→ Normal: [$ux-user-flow] → [$ux-wireframe or $ux-prototype-html]
→ Normal: [$ux-design-system] → $ux-final-design → $ux-validate
```

Choose only steps that resolve real uncertainty. Use Plan mode for visual direction when preferences need discussion; switch to Normal before creating Figma or prototype artifacts. With a mature design system, discovery may lead directly to final design and validation.

## Working practices

- **Chats and handoffs:** Stay in one chat when the next skill benefits from established context. Start a fresh chat for independent `dev-review`. Long work can carry concise personal notes into another chat; recheck them against current code and Git state.
- **Personal artifacts:** Create a handoff file only when cross-chat continuity helps. The harness does not automatically add `SPEC.md`, `PLAN.md`, audit/debug notes, `AGENTS.md`, or environment notes to a project. Read existing project and company docs as evidence; change project files only for the actual task.
- **Source precedence:** Current user instructions → current repository/Git/runtime evidence → existing project docs → personal notes → generic assumptions. Never let a stale personal plan override current code. Keep secrets out of personal notes.
- **Engineering judgment:** Skills explain a significant decision's reason and tradeoff briefly when useful, without turning routine work into a tutorial. Repeatable mechanics belong in project scripts and CI.
- **Execution:** DEV handoffs use the centralized [execution policy](.agents/skills/references/execution-policy.md). Spend more capability on uncertainty and risk; use a lighter tier when a sound plan makes work deterministic. Production debugging is read-only; production deployment needs approval for the concrete action.

Harness sources: [skills](.agents/skills), [workflow governance](.agents/skills/references/workflow-governance.md), and [engineering references](.agents/skills/references/engineering/README.md).

# Codex development harness

Skills for understanding, designing, implementing, reviewing, and shipping web applications. Invoke one in your project with `$skill-name`; it inspects the current code and uses only the context relevant to the task.

## DEV skills

| Skill | What it does |
| --- | --- |
| `$dev-explore` | Explains how an existing system or flow works. |
| `$dev-discovery` | Defines a change's behavior, constraints, and open decisions. |
| `$dev-debug` | Diagnoses a bug or incident without applying a fix. |
| `$dev-rails-audit` | Finds and prioritizes improvements in a Rails app. |
| `$dev-plan` | Designs implementation steps, tests, and rollout. |
| `$dev-implement` | Changes project code and verifies the result. |
| `$dev-review` | Independently checks a diff against requirements and engineering risks. |
| `$dev-release` | Prepares, coordinates, and verifies a release. |

## UX skills

| Skill | What it does |
| --- | --- |
| `$ux-discovery` | Clarifies the product problem and requirements. |
| `$ux-visual-direction` | Defines visual intent from product context and references. |
| `$ux-user-flow` | Maps one user goal and its decisions in FigJam. |
| `$ux-wireframe` | Explores screen structure and states in Figma. |
| `$ux-prototype-html` | Tests an interaction in a standalone browser prototype. |
| `$ux-design-system` | Builds reusable Figma foundations and components. |
| `$ux-final-design` | Produces detailed Figma screens and states. |
| `$ux-validate` | Evaluates a design or implementation against available evidence. |

## Example workflows

**New feature — Stripe subscriptions in an existing Rails app**

```text
Same chat:
[$dev-explore "Explain accounts, billing, permissions, and existing payments"]
→ $dev-discovery "Add Stripe subscriptions"
→ $dev-plan
→ $dev-implement

New chat: $dev-review "Review the Stripe subscriptions change"
Then:     $dev-release "Ship to staging"
Later:    $dev-release "Ship to production"
```

Brackets mean optional. Use `dev-explore` when the domain is unfamiliar. Discovery settles behavior; planning is useful for integration, data, failure, or rollout decisions. A fresh review reduces anchoring to implementation choices.

**Change in a familiar area — show the account timezone in settings**

```text
Same chat: $dev-discovery "Show the account timezone in settings"
        → [$dev-plan] → $dev-implement
New chat, when useful: $dev-review
```

Skip planning if discovery confirms a small, well-defined change following an existing pattern. For a larger change in a known domain, use `dev-discovery → dev-plan → dev-implement → new-chat dev-review`.

**Bug — exports get stuck in production**

```text
Same chat: $dev-debug "Production exports get stuck"
        → [$dev-plan] → $dev-implement
New chat: $dev-review
Then, if shipping: $dev-release
```

Debugging diagnoses; implementation fixes. Add planning when the correction involves material data, architecture, or integration choices.

**Understand or improve an existing app**

```text
$dev-explore "Explain how accepting an invitation grants account access"

$dev-rails-audit "Focus on performance and architecture"
→ narrow finding: $dev-implement
→ structural finding: $dev-plan → $dev-implement
→ new-chat $dev-review
```

Exploration may be the whole task. An audit recommends changes but does not implement them.

**UX feature flow**

```text
$ux-discovery → [$ux-visual-direction] → [$ux-user-flow]
→ [$ux-wireframe or $ux-prototype-html]
→ [$ux-design-system] → $ux-final-design → $ux-validate
```

Choose only the steps that resolve real uncertainty. For an existing product with a mature design system, discovery may lead directly to final design and validation.

## Working practices

- **Chats and handoffs:** Stay in one chat when the next skill benefits from established context. Start a fresh chat for independent `dev-review`. Long work can carry concise personal notes into another chat; recheck them against current code and Git state.
- **Personal artifacts:** Workflow notes live in chat or `~/.codex/workspaces/<project-key>/`, outside the target repository. Create a file only when cross-chat continuity helps. The harness does not automatically add `SPEC.md`, `PLAN.md`, audit/debug notes, `AGENTS.md`, or environment notes to a project. Read existing project and company docs as evidence; change project files only for the actual task.
- **Source precedence:** Current user instructions → current repository/Git/runtime evidence → existing project docs → personal notes → generic assumptions. Never let a stale personal plan override current code. Keep secrets out of personal notes.
- **Engineering judgment:** Skills explain a significant decision's reason and tradeoff briefly when useful, without turning routine work into a tutorial. Repeatable mechanics belong in project scripts and CI.
- **Execution:** DEV handoffs use the centralized [execution policy](.agents/skills/references/execution-policy.md). Spend more capability on uncertainty and risk; use a lighter tier when a sound plan makes work deterministic. Production debugging is read-only; production deployment needs approval for the concrete action.

Harness sources: [skills](.agents/skills), [workflow governance](.agents/skills/references/workflow-governance.md), and [engineering references](.agents/skills/references/engineering/README.md).

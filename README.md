# AI Skills for Codex and Claude Code

This repository provides one shared set of skills for product design and software development in Codex and Claude Code.

Invocation syntax differs by host: Codex uses `$skill-name`; Claude Code uses `/skill-name`. Examples below show Codex syntax unless labeled otherwise. For example, invoke UX discovery as `$ux-discovery` in Codex or `/ux-discovery` in Claude Code.

The skills are written in English because they are instructions for the agent. Invoke and converse in the language you prefer.

## Included skills

### UX / Product Design

```text
$ux-discovery
$ux-visual-direction
$ux-design
$ux-validate
$ux-build
$ux-prototype
```

Main flow:

```text
$ux-discovery → [$ux-visual-direction when useful] → $ux-design → $ux-validate → $ux-build
                        ↘
                         $ux-prototype   (optional)
```

### Software Development

```text
$dev-discovery
$dev-plan
$dev-implement
$dev-review
```

Main flow:

```text
$dev-discovery → $dev-plan → $dev-implement → $dev-review
```

The goal is for each skill to represent a recognizable professional phase, not a microtask. The best ideas from larger workflows —inspect before asking, document decisions, plan in slices, implement with rapid feedback, and review against spec + standards— are absorbed into these few skills.

## Decision and execution phases

Use **Plan mode** for decision-oriented skills. Enter it explicitly with `/plan` before invocation; a skill cannot switch the current agent's mode.

Decision-oriented skills in this repository:

- `$ux-discovery` — product goals and behavior;
- `$ux-visual-direction` — visual references and preferences;
- `$dev-discovery` — software behavior and technical constraints;
- `$dev-plan` — implementation approach, after requirements are decided.

These skills investigate repository and reference evidence before asking questions, then produce decision-complete artifacts. Use the host's native structured question tool for material decisions: `request_user_input` in Codex and `AskUserQuestion` in Claude Code. Offer concise, evidence-based options and a recommendation when supported; allow a custom answer when the tool permits it. Ask no more than 1–3 questions per round. If structured input is unavailable, ask one concise question in ordinary conversation. See [the shared interaction policy](.agents/skills/references/interactive-decision-policy.md).

Plan mode is read-only in Claude Code. Complete investigation and interviews there, then leave Plan mode before creating or updating durable project artifacts. After decisions are complete, use the normal execution context for execution-oriented skills.

Execution-oriented skills apply, generate, validate, or review already-decided work: `$ux-design`, `$ux-validate`, `$ux-build`, `$ux-prototype`, `$dev-implement`, and `$dev-review`. They investigate their inputs and repository, avoid reopening settled decisions, and ask only for a genuine blocker or missing target detail that cannot be inferred safely.

---

# 1. Language policy

All skills follow the same contract.

## Conversation language

The active agent detects the language of the current message and uses it for:

- questions;
- interviews;
- clarifications;
- explanations;
- progress summaries.

For example:

```text
/plan
$ux-discovery Quiero mejorar el onboarding porque muchos usuarios abandonan antes de terminar.
```

The interview should happen in Spanish.

## File language

Repository artifacts are written in **English by default**, even if the conversation is in another language.

For example:

```text
AGENTS.md
product/CONTEXT.md
design/DESIGN_SYSTEM.md
engineering/ARCHITECTURE.md
work/<initiative>/SPEC.md
work/<initiative>/PLAN.md
```

To change this, it must be requested explicitly:

```text
/plan
$ux-discovery Quiero mejorar el onboarding. Para esta iniciativa, generá también todos los artefactos en español.
```

The precedence is:

```text
1. explicit instruction from the current message
2. artifact language explicitly recorded for the initiative in SPEC.md
3. English by default
```

This means that if discovery records that **the entire initiative** should be documented in Spanish, the following skills keep that decision. If only a specific file is requested in another language, the change does not automatically apply to all other files.

## Product language is independent

You should not assume that the conversation language is the same as the interface language.

It is perfectly valid to have:

```text
Conversation with the agent: Spanish
Repository documentation: English
Product UI: Spanish
```

Or:

```text
Conversation with the agent: Spanish
Repository documentation: English
Product UI: English
```

The skills attempt to infer the product language from the repository, Figma, or `product/CONTEXT.md`. They only ask if it remains ambiguous and genuinely affects the work.

---

# 2. Installation

## Recommended: skills inside the repository

The repository uses `.agents/skills` as the canonical source. Codex discovers skills there. Claude Code discovers them under `.claude/skills`; this repository includes symlinked entries to the canonical skill directories, so it has no second copy of the skills.

```text
your-project/
├── .agents/
│   └── skills/                 # the only copy of each skill and its resources
└── .claude/
    ├── settings.json           # Claude-specific invocation policy
    └── skills/                 # symlinks to individual .agents/skills entries
        ├── references/
        ├── ux-discovery/
        ├── ux-visual-direction/
        ├── ux-design/
        ├── ux-validate/
        ├── ux-build/
        ├── ux-prototype/
        ├── dev-discovery/
        ├── dev-plan/
        ├── dev-implement/
        └── dev-review/
```

Git stores these as symlinks, not copies. If your Git client does not check out symlinks, enable symlink support before cloning or copy the skill directories locally into `.claude/skills/`.

Clone the repository and open it in either tool. Codex loads the canonical `.agents/skills` tree; Claude Code follows the `.claude/skills` symlinks. Codex-specific UI/invocation metadata stays in `agents/openai.yaml`; Claude Code ignores that file. The checked-in `.claude/settings.json` keeps `ux-visual-direction` manually invoked, matching its Codex policy.

## Alternative: user-global installation

If you want to use them across all repositories, copy the individual directories to:

```text
~/.agents/skills/       # Codex
~/.claude/skills/       # Claude Code
```

For a team or project that wants to evolve these rules alongside the code, I prefer the installation inside the repo.

---

# 3. Files the workflow may create

Persistent documentation is intentionally minimal.

A mature project may end up with:

```text
repo/
├── AGENTS.md
│
├── product/
│   └── CONTEXT.md
│
├── design/
│   └── DESIGN_SYSTEM.md
│
├── engineering/
│   ├── ARCHITECTURE.md
│   └── decisions/              # only truly justified ADRs
│
├── work/
│   └── <initiative>/
│       ├── SPEC.md
│       └── PLAN.md             # created by dev-plan when needed
│
└── prototype/
    └── <initiative>/
        └── prototype.html      # optional, created by ux-prototype
```

Not every project needs all of these files from day one.

If the repository already has an equivalent, good convention, the skills should **reuse it**, not create parallel documentation just to enforce this structure.

## Responsibility of each file

### `AGENTS.md`

Permanent, concise instructions for the agents working in the repo. It should point to the relevant context, not duplicate it wholesale.

### `product/CONTEXT.md`

Stable product context: users, domain, terminology, core workflows, roles/permissions, constraints, principles, metrics, and product language.

### `design/DESIGN_SYSTEM.md`

The contract between Figma and code: links, foundations, tokens, components, mappings, naming, accessibility, and known drift.

### `engineering/ARCHITECTURE.md`

Stable technical context: system boundaries, main modules, data, integrations, conventions, operational constraints, and testing strategy.

### `work/<initiative>/SPEC.md`

The source of truth for the initiative: problem, outcome, evidence, requirements, flows/states, decisions, validation, Figma, acceptance criteria, and open questions.

### `work/<initiative>/PLAN.md`

An executable engineering plan for non-trivial work: affected modules, slices, contracts, migrations, tests, rollout, observability, risks, and progress.

---

# 4. UX workflow

## Phase 1 — `$ux-discovery`

Open the repository in either agent, enter Plan mode, and start a new session:

```text
/plan
$ux-discovery I want to design a new flow for inviting members to a workspace.
```

The skill should do this first:

```text
repo + docs + Figma available
            ↓
        what we already know
            ↓
what is inference / assumption / unknown
            ↓
ask only real decisions and ambiguities
            ↓
leave read-only Plan mode, then update context + SPEC
```

It should not ask something it can answer by reading the repository.

Desired example:

```text
I see that Admin and Member roles already exist, invitations expire,
and the product uses a creation modal.

I couldn't find a rule for expired invitations.
Should an Admin be able to resend them or should they create a new invitation?
```

The conversation follows the user's language; repository artifacts are written in English by default.

### Do we need to open another chat for `$ux-design` afterward?

**Usually no.** It is better to continue in the same chat:

```text
$ux-design
```

This preserves the nuances of the interview. In any case, `ux-design` reads `SPEC.md` and the permanent documents again, so it does not depend only on chat memory.

If discovery was large or a clean boundary is desired, opening a new chat is safe because the durable context is on disk.

---

## Phase 2 — `$ux-visual-direction` (when references or visual choices matter)

Use after discovery and before defining the design system or designing screens. Enter Plan mode first:

```text
/plan
$ux-visual-direction

Use the references in design/references/.
```

The agent inspects references, records their visible properties and intended roles, then asks only which patterns to adopt, avoid, prioritize, or combine. The durable result is `design/VISUAL_DIRECTION.md`. Skip this phase when the existing visual direction already answers the initiative's needs.

Once discovery and visual direction are settled, leave Plan mode before continuing with `$ux-design`.

When the host keeps Plan mode read-only, finish the interview and agree on the direction there, then leave Plan mode before writing `VISUAL_DIRECTION.md`.

## Phase 3 — `$ux-design`

In the same chat, usually:

```text
$ux-design
```

If there are several active initiatives:

```text
$ux-design work/invite-members/SPEC.md
```

The phase follows this logic:

```text
outcome
  ↓
information architecture / flow
  ↓
alternatives when there is real uncertainty
  ↓
interaction design
  ↓
states + responsive + accessibility
  ↓
visual system
  ↓
native Figma
```

It should not jump from an ambiguous request directly to final screens.

When Figma exists, the skill should first inspect existing libraries, variables, components, and patterns. Only then should it create new elements if needed.

---

## Optional — `$ux-prototype`

Use it when something is better understood by running in a browser than by discussing it or looking at static screens:

```text
$ux-prototype
```

Creates a single file:

```text
prototype/<initiative>/prototype.html
```

It must use only:

- HTML;
- inline CSS in `<style>`;
- vanilla JavaScript in `<script>`.

It does not use:

```text
React
Vue
Svelte
npm
Vite
Webpack
Tailwind CDN
Bootstrap
backend
external APIs required to function
```

To run it:

```bash
python3 -m http.server 8000
```

And open the corresponding path from:

```text
http://localhost:8000/
```

The prototype is meant to answer a design question. **It is not production code.**

It can run in the same chat as `$ux-design` or in a new one.

---

## Phase 4 — `$ux-validate`

Here I recommend a **new chat**:

```text
$ux-validate work/invite-members/SPEC.md
```

The reason is simple: it is better if the person critiquing the design is not too anchored to the decisions they just made.

The skill explicitly distinguishes:

```text
observable problem in the design
vs
violation of system/standard
vs
hypothesis needing real users
vs
real user evidence
```

It cannot invent research findings.

If important problems appear:

```text
$ux-design
```

The design is updated and then validated again.

---

## Phase 5 — `$ux-build`

Once validated, I recommend another **new chat**:

```text
$ux-build work/invite-members/SPEC.md
```

The implementation must come from:

```text
SPEC
+
approved Figma
+
DESIGN_SYSTEM
+
real repo
```

not from memory of the exploratory conversation.

Before writing code, the skill looks for mappings:

```text
Figma Button primary/md
        ↓
existing Button in the repo
        ↓
use existing component
```

Not:

```text
Figma Button
        ↓
create another button with arbitrary CSS
```

If, during implementation, an important decision about architecture, database, API, security, concurrency, infrastructure, etc. arises that UX did not resolve, `ux-build` should not invent it. That problem moves to the DEV flow:

```text
$dev-discovery
$dev-plan
```

---

# 5. DEV workflow

## Phase 1 — `$dev-discovery`

Example:

```text
/plan
$dev-discovery I want to add support for invitations with expiration and resend.
```

The skill:

1. reads the repo before asking questions;
2. reuses existing UX/Product specs if they exist;
3. separates facts, inferences, assumptions, decisions, and unknowns;
4. asks only about decisions the code cannot resolve;
5. creates/updates stable technical context when it genuinely adds value;
6. leaves the initiative sufficiently defined to plan.

If the user requests a specific technology, discovery tries to separate mechanism from requirement.

Example:

```text
Request: "add a Redis lock"

Requirement to validate:
"the same webhook cannot be processed concurrently twice"
```

### Should `dev-plan` happen in the same chat?

**Yes, recommended.**

When discovery ends, remain in Plan mode:

```text
/plan
$dev-plan
```

while keeping the same thread.

Resolve any remaining technical decisions in Plan mode, then leave it before writing `SPEC.md` or `PLAN.md`.

---

## Phase 2 — `$dev-plan`

Generates, for non-trivial work:

```text
work/<initiative>/PLAN.md
```

The plan must be executable by a new chat that only has the repo, `SPEC.md`, and `PLAN.md`.

When Plan mode is read-only, finish the planning decisions there, then leave Plan mode to create or update `PLAN.md`.

Implementation is divided into small, verifiable vertical slices.

Prefer:

```text
receive webhook
→ persist dedupe key
→ test duplicate behavior
```

over:

```text
create all models
→ create all services
→ create all controllers
→ write tests at the end
```

For minimal changes, `dev-plan` may explicitly decide that `PLAN.md` would be unnecessary bureaucracy.

---

## Phase 3 — `$dev-implement`

For non-trivial work I recommend a **new chat**:

```text
$dev-implement work/invite-members/PLAN.md
```

This has one advantage: it proves that the plan and the repo contain enough information to implement without depending on the mental context of whoever performed discovery.

Implementation:

```text
slice
→ test/feedback loop
→ minimal implementation
→ verification
→ next slice
```

It does not reopen product decisions already resolved unless the reality of the repo proves the plan is invalid.

For a very small change, it is acceptable to continue in the same discovery/plan chat.

---

## Phase 4 — `$dev-review`

Whenever practical, use **another new chat**:

```text
$dev-review work/invite-members/SPEC.md
```

Or:

```text
$dev-review Review the current branch against work/invite-members/SPEC.md
```

The review has two mandatory axes:

```text
1. compliance with the SPEC
2. engineering quality
```

It must look at the real diff and run relevant verification. It should not review only the summary generated by the person who implemented it.

By default it is review only. To also fix findings:

```text
$dev-review Review the branch, fix the confirmed issues, and rerun verification.
```

---

# 6. Same chat or separate chats?

Recommended summary:

| Flow | Transition | Recommendation |
| --- | --- | --- |
| UX | `ux-discovery → ux-visual-direction` | Same chat, enter/remain in Plan mode |
| UX | `ux-visual-direction → ux-design` | Leave Plan mode; continue with documented direction |
| UX | `ux-discovery → ux-design` | Same chat normally when visual direction is already settled |
| UX | `ux-design → ux-prototype` | Same chat or new |
| UX | `ux-design → ux-validate` | New chat recommended |
| UX | `ux-validate → ux-build` | New chat recommended |
| DEV | `dev-discovery → dev-plan` | Same chat recommended |
| DEV | `dev-plan → dev-implement` | New chat for non-trivial work |
| DEV | `dev-implement → dev-review` | New chat strongly recommended |

General principle:

> The chat is working memory. The repository files are the durable memory.

We are not trying to maintain a giant thread just because “it has context.” If a phase needs context to survive, that important context should be recorded in the artifacts.

---

# 7. Figma setup

To take full advantage of the UX workflow:

1. set up the Figma MCP integration supported by your agent;
2. use a **Full seat** for workflows where the agent writes on the canvas;
3. install the skills recommended by Figma for the MCP client when available;
4. save relevant Figma links in `design/DESIGN_SYSTEM.md` and/or `SPEC.md`;
5. prioritize existing variables, components, libraries, and mappings before creating new ones;
6. use Code Connect when the Figma plan and project allow it.

The MCP is treated as a bridge:

```text
Figma
  ↕
the agent
  ↕
repo
```

Not as a magic button “Figma → perfect code”.

---

# 8. Complete examples

## Existing product: speak English, document in English

```text
/plan
$ux-discovery I want to improve the onboarding permissions screen. First review what already exists and ask me only what you cannot resolve from the repo or Figma.
```

Expected:

- the agent inspects first;
- asks in the user's language;
- `SPEC.md`, `CONTEXT.md`, etc. remain in English;
- the UI maintains the real language of the product.

Then, same chat:

```text
$ux-design
```

When references should guide the design, run this decision phase before `$ux-design`:

```text
/plan
$ux-visual-direction

Use these screenshots as references. I like the compact density and inline actions, but avoid dark mode and excessive cards.
```

After that, new chat:

```text
$ux-validate work/onboarding-permissions/SPEC.md
```

And once validated, another chat:

```text
$ux-build work/onboarding-permissions/SPEC.md
```

## New software project

```text
/plan
$dev-discovery I want to create an API to process payment webhooks and define the behavior and architecture clearly before implementing.
```

After discovery, remain in Plan mode in the same chat:

```text
/plan
$dev-plan
```

Then a new chat:

```text
$dev-implement work/payment-webhooks/PLAN.md
```

Finally, another chat:

```text
$dev-review work/payment-webhooks/SPEC.md
```

## An entire initiative documented in Spanish

```text
/plan
$ux-discovery I want to design the new checkout. For this entire initiative, also write the repository artifacts in Spanish.
```

Discovery records that preference in `SPEC.md`; `ux-design`, `ux-validate`, and `ux-build` follow it while working on that initiative unless a new explicit instruction overrides it.

---

# 9. Package principles

- **Repo first:** facts are investigated; the user is not asked about things the code already knows.
- **Ask for decisions, not searchable facts.**
- **Problem before solution.**
- **Durable context on disk.**
- **Few skills with broad professional phases.**
- **Small-step implementation with real feedback.**
- **Independent validation/review when useful.**
- **Never invent user research.**
- **Never duplicate the design system just because generating new CSS is easier.**
- **`AGENTS.md` is short:** permanent rules and pointers; not a project encyclopedia.
- **User explicit instructions take priority** over workflow defaults.

---

# 10. Useful official references

- OpenAI Skills: https://developers.openai.com/api/docs/guides/tools-skills
- Skill structure: https://developers.openai.com/plugins/build/skills
- Current guide on skills and concise `AGENTS.md`: https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra
- Figma MCP: https://developers.figma.com/docs/figma-mcp-server/
- Figma Write to Canvas: https://developers.figma.com/docs/figma-mcp-server/write-to-canvas/
- Figma MCP Tools: https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/
- Figma Code to Canvas: https://developers.figma.com/docs/figma-mcp-server/code-to-canvas/

# AI Skills for Codex and Claude Code

One shared skill source for product design and software development. The UX skills help a designer investigate, explore, prototype, systematize, finalize, and validate product experiences. They do not implement production application code. DEV skills own engineering implementation.

Codex invocation uses `$skill-name`; Claude Code uses `/skill-name`. Examples below use Codex syntax. Skills inspect durable repository and Figma context on every invocation, so a workflow can span chats. **Chat is working memory; repository artifacts are durable product memory; Figma is the durable design artifact.**

## Agentic Workflow Design Principles

This skill system is intentionally small, modular, and artifact-driven. Its architecture follows current guidance from OpenAI and Anthropic for building reliable agentic workflows.

The goal is not to prescribe every step the model must take. Instead, the system gives the agent clear goals, boundaries, durable context, and access to the right tools while leaving enough flexibility for the model to reason about the specific project.

### 1. Prefer simple, composable workflows

Both OpenAI and Anthropic recommend avoiding unnecessary agentic complexity.

Anthropic's guidance on effective agents emphasizes starting with the simplest solution that works and adding orchestration only when it produces measurable value. It distinguishes predictable workflows from fully autonomous agents and recommends simple, composable patterns over elaborate frameworks.

OpenAI similarly recommends keeping skills focused on recognizable workflows rather than accumulating large collections of overlapping instructions.

This project therefore uses a small number of high-level skills:

```text id="ctpzwt"
UX
ux-discovery
ux-visual-direction
ux-wireframe
ux-prototype-html
ux-design-system
ux-final-design
ux-validate

DEV
dev-discovery
dev-plan
dev-implement
dev-review
```

A new skill should only be introduced when it represents a genuinely different user goal, trigger, input, or success criterion.

Do not create a separate skill merely because an internal workflow contains another step.

---

### 2. Skills should represent user goals, not implementation steps

A useful skill answers a recognizable question.

For example:

```text id="bi1y5l"
ux-discovery
→ What problem are we solving?

ux-visual-direction
→ What should this product visually feel like?

ux-wireframe
→ How should the experience be structured?

ux-prototype-html
→ How should this experience behave interactively?

ux-design-system
→ What reusable visual rules and components do we need?

ux-final-design
→ What should the production-intent interface look like?

ux-validate
→ Does this solution work, and what evidence supports it?
```

OpenAI recommends defining clear workflow boundaries for skills: expected inputs, intended process, output, facts that must not be inferred, supporting resources, and conditions for asking questions or stopping.

This makes skill selection understandable to both the agent and the human using it.

---

### 3. Keep skill descriptions short and unambiguous

Skill metadata is part of the agent's context and helps determine which skill should be selected.

OpenAI recommends descriptions that state precisely what the skill does and when it applies. Overly broad descriptions can cause the wrong skill to be loaded, and large numbers of overlapping descriptions can compete for limited context.

Anthropic makes a similar recommendation for agent tools: each capability should have a clear and distinct purpose, because overlapping capabilities create ambiguous decision points for the agent.

Therefore:

```text id="2jduwn"
Good:
Turn visual references and user preferences into a durable product visual direction.

Too broad:
Help with product design, branding, UI, inspiration, design systems,
screens and visual decisions.
```

Detailed workflow instructions belong inside `SKILL.md`, not in the skill description.

---

### 4. Use namespaces to make boundaries obvious

The `ux-` and `dev-` prefixes are deliberate.

Anthropic recommends namespacing agent tools when multiple related capabilities coexist, because clear naming helps the model distinguish their functional boundaries and select the appropriate capability.

The same principle is applied here to skills:

```text id="aueq4t"
ux-*  → Product design workflow
dev-* → Software engineering workflow
```

This also makes the workflow easier for humans to discover and remember.

---

### 5. Use progressive disclosure instead of loading everything

Context is a finite resource.

OpenAI recommends progressive disclosure for skills: expose enough information for the model to know that a capability exists, then load detailed instructions and supporting resources only when they are relevant.

Anthropic describes context engineering similarly: effective agents should work with the smallest set of high-signal information needed for the current task rather than filling the context window with every potentially useful piece of information.

For that reason, this project does not require every skill to read every document.

For example:

```text id="o9bgso"
ux-wireframe
→ SPEC + relevant product context

ux-visual-direction
→ visual direction + references + existing visual product context

ux-final-design
→ SPEC + visual direction + design system + relevant Figma

dev-plan
→ SPEC + architecture + relevant repository implementation
```

Skills should inspect additional files when the task makes them relevant, not because a global instruction requires reading the entire repository before every action.

---

### 6. Inspect before asking

Agents should use their environment to resolve questions whenever possible.

The repository, Figma, existing documentation, code, screenshots, and connected tools are part of the agent's working environment.

The preferred pattern is:

```text id="85s2c5"
inspect
→ understand
→ identify uncertainty
→ ask only what cannot be determined
→ act
```

not:

```text id="3bl07n"
ask the user everything
→ ignore available project context
```

This follows the broader agentic pattern recommended by both organizations: models should use tools and retrieval to acquire relevant context as they work rather than forcing all information into the initial prompt.

A discovery skill should therefore distinguish:

```text id="4vbko9"
KNOWN
INFERRED
ASSUMED
UNKNOWN
CONFLICTING
```

and only interrupt the user when unresolved information could materially change the result.

---

### 7. Durable artifacts are the workflow's shared memory

Chat history is useful working memory, but it should not be the only place where important decisions live.

Long-running agentic tasks continuously accumulate context. Anthropic recommends actively curating context rather than allowing all previous information to accumulate indefinitely.

OpenAI likewise recommends keeping persistent repository instructions and supporting documentation focused and current rather than continually expanding `AGENTS.md` or prompts with every past decision.

This workflow therefore separates:

```text id="zedkgb"
Chat
→ temporary reasoning and active collaboration

Repository artifacts
→ durable product and engineering knowledge

Figma
→ durable design artifacts

Git
→ durable implementation history
```

Important decisions should be written back to the appropriate artifact.

Typical durable sources are:

```text id="hnzu6x"
AGENTS.md
product/CONTEXT.md
design/VISUAL_DIRECTION.md
design/DESIGN_SYSTEM.md
work/<initiative>/SPEC.md
Figma files
source code
tests
```

Because durable context lives outside the conversation, later skills should be able to reconstruct the state of the project in a new chat.

---

### 8. Keep `AGENTS.md` small and stable

`AGENTS.md` applies broadly, so instructions placed there have a large effect on agent behavior.

OpenAI specifically recommends auditing `AGENTS.md` and removing instructions that no longer need to apply to every task. Requiring unrelated documentation to be read before every change wastes context and can overconstrain capable models.

Use `AGENTS.md` for durable repository-wide rules such as:

```text id="b3d5hz"
where important project context lives
which conventions are universal
important safety boundaries
how product/design documentation is organized
```

Do not use it as:

```text id="8vr01o"
a feature specification
a complete repository map
a running decision log
a copy of every skill
a collection of historical prompting fixes
```

Initiative-specific knowledge belongs in `SPEC.md` or another appropriately scoped artifact.

---

### 9. Let the agent reason inside clear boundaries

Modern models benefit from clear goals and constraints but can perform worse when workflows attempt to encode every possible reasoning step.

OpenAI notes that increasingly capable models require less procedural scaffolding and that elaborate skill "itineraries" can become counterproductive.

Anthropic similarly recommends giving agents clear instructions at the right level of abstraction rather than either hardcoding brittle decision trees or relying on vague guidance.

Skills should therefore specify:

```text id="u6u9yk"
goal
inputs
constraints
non-goals
durable outputs
important decision boundaries
required tools or sources
verification expectations
```

but should generally avoid prescribing every internal reasoning step.

Prefer:

```text id="wtaln5"
Inspect existing product and Figma context before defining
new visual foundations. Reuse existing decisions when appropriate
and surface material conflicts.
```

over a rigid script containing dozens of mandatory micro-steps.

---

### 10. Make decision boundaries explicit

Autonomy works best when the agent knows which decisions it can make and which decisions require human input.

For example:

```text id="vdx0uq"
Agent may decide:
- how to organize a Figma exploration;
- which existing repository files are relevant;
- which existing component best matches a design requirement;
- which edge cases should be examined.

Agent should ask when:
- product behavior is genuinely ambiguous;
- two visual references imply incompatible directions;
- an assumption would materially change requirements;
- a destructive or high-impact decision lacks authorization.
```

OpenAI recommends carefully calibrating these decision boundaries rather than forcing the model to request approval for routine work.

This workflow therefore favors:

```text id="50ttow"
reasonable autonomy inside known boundaries
+
targeted clarification for material ambiguity
```

rather than constant confirmation.

---

### 11. Tools provide capabilities; skills provide workflows

MCP tools and skills serve different purposes.

OpenAI describes tools as the capabilities that let an agent access information or perform actions, while skills encode reusable knowledge about how those tools should be combined for a recognizable workflow.

For example:

```text id="nl7ufx"
Figma MCP
→ capability to inspect or modify Figma

ux-final-design
→ workflow describing how Figma should be used to produce
  a production-intent product design
```

Similarly:

```text id="gcv5i3"
filesystem / shell / git
→ engineering capabilities

dev-implement
→ workflow governing how those capabilities are used
  to implement an approved plan
```

Skills should therefore orchestrate tools around goals instead of duplicating tool documentation.

---

### 12. Tool and skill outputs should maximize signal, not volume

Anthropic's agent-tool guidance emphasizes returning relevant, interpretable context rather than dumping large amounts of low-value information into the model's context window. It also recommends filtering, pagination, concise representations, and semantically meaningful identifiers where appropriate.

The same principle applies to workflow artifacts.

Documentation should contain information that changes future decisions.

Avoid producing documentation merely because a template contains another section.

Prefer:

```text id="86pljp"
3 meaningful constraints
2 unresolved product questions
1 clearly documented decision
```

over:

```text id="nnw0ri"
15 pages of generic product-design prose
```

---

### 13. Separate creation from independent evaluation

Agentic systems benefit from verification loops rather than treating the first generated result as final.

Both OpenAI and Anthropic emphasize testing and evaluation as core parts of reliable agentic systems. Anthropic specifically recommends evaluation-driven development for tools and agents, while OpenAI recommends verification appropriate to the task rather than blindly running every possible check.

This workflow therefore gives validation and review explicit roles:

```text id="uqppxk"
UX:
design → ux-validate

DEV:
implementation → dev-review
```

Starting these evaluation passes in a fresh chat can sometimes be useful because it reduces anchoring on the reasoning that created the artifact.

This is a workflow choice derived from the broader context-management principles above, not a requirement of either OpenAI or Anthropic.

The important requirement is that a fresh session must be able to reconstruct the necessary context from durable artifacts.

---

### 14. Preserve human intent without forcing humans to manage agent internals

The human should choose the desired outcome:

```text id="fbud4l"
"I need to understand the problem."
"I want to explore the flow."
"I want an interactive prototype."
"I need the final design."
"I want to implement this."
"I want an independent review."
```

The skill should handle the internal procedure required to reach that outcome.

This is why this system exposes a few meaningful commands rather than dozens of procedural commands.

The designer should not need to understand the internal orchestration required by `ux-final-design`.

The developer should not need to manually invoke a separate command for every internal phase of `dev-review`.

The complexity belongs inside the workflow.

---

### 15. Treat the workflow as a system that should evolve

Agent behavior changes as models, tools, MCP servers, and project requirements evolve.

OpenAI explicitly recommends periodically revisiting skills and `AGENTS.md` because instructions that helped older models can become redundant or even counterproductive with newer ones.

Anthropic recommends an evaluation-driven approach: test agents on realistic tasks, inspect where they fail or become confused, and improve tools and instructions based on observed behavior rather than intuition alone.

Therefore, treat these skills as versioned product infrastructure.

When changing them:

```text id="qz1xim"
observe real usage
→ identify repeated failure modes
→ make the smallest useful change
→ test realistic workflows
→ remove obsolete instructions
```

Do not permanently add another rule every time the agent makes one mistake.

## Design philosophy

The resulting architecture can be summarized as:

```text id="w8yis3"
Few skills
Clear names
Distinct goals
Progressive context
Durable artifacts
Tool-assisted discovery
Targeted questions
Explicit decision boundaries
Independent validation
Minimal duplicated instructions
```

Or, operationally:

```text id="t5f3tr"
inspect
→ understand
→ clarify only what matters
→ act
→ persist decisions
→ validate
```

This is the foundation of the UX and DEV workflows in this repository.


## Skills at a glance

| Skill | Primary question | Main output |
|---|---|---|
| `ux-discovery` | What problem are we solving? | Initiative `SPEC.md`, product context |
| `ux-visual-direction` | What should the product feel and look like? | `VISUAL_DIRECTION.md`, saved references |
| `ux-wireframe` | How should the experience be structured? | Low-fidelity Figma wireframes |
| `ux-prototype-html` | How should this interaction behave in a browser? | `prototype.html` |
| `ux-design-system` | What reusable visual rules and components do we need? | Figma library + `DESIGN_SYSTEM.md` |
| `ux-final-design` | What should the production-intent UI be? | High-fidelity Figma design |
| `ux-validate` | Does this solution work, and what evidence supports that? | Findings + updated `SPEC.md` |

DEV skills remain a separate engineering workflow:

| Skill | Primary question | Main output |
|---|---|---|
| `dev-discovery` | What technical behavior and constraints matter? | Technical context and initiative spec |
| `dev-plan` | How should the change be implemented? | `PLAN.md` when warranted |
| `dev-implement` | Can we implement the approved plan safely? | Production code and verification |
| `dev-review` | Does the change meet its spec and engineering bar? | Evidence-based review findings |

## Choosing a UX skill

Choose by the task you have in mind, not by a mandatory phase checklist. Visual direction is transversal and can be revisited whenever references or preferences change. Wireframes and HTML prototypes are optional. A mature product may go directly from discovery to final design and validation. New products often need more exploration. Use the minimum fidelity and artifacts that resolve the real design question.

```text
ux-discovery ───────────────→ ux-wireframe ──→ ux-prototype-html ──→ ux-validate
     │                             │                                      │
     └─────────────────────────────┴──────────→ ux-final-design ──────────┘
                                                    ↑
                                            ux-design-system

ux-visual-direction can inform or update any of these at any point.
```

Figma-oriented skills use Figma MCP: `ux-wireframe`, `ux-design-system`, and `ux-final-design`. They inspect before editing and reuse existing files/libraries where suitable. Keep conceptually separate artifacts in separate Figma destinations:

- `<Product> — Design System` (its own library/file)
- `<Product> — <Initiative> — Wireframes`
- `<Product> — <Initiative> — Final Design`

Reuse an existing file that already serves the purpose; do not create duplicates. `ux-prototype-html` creates a browser prototype, not a Figma artifact. The UX-to-DEV handoff is the durable SPEC, Figma links, design-system contract, validation findings, and approved design—not a chat transcript.

## Same chat or a new chat?

Stay in the same chat while resolving ambiguity, when one skill directly continues the reasoning of another, or when rapid iteration is useful. `ux-discovery → ux-wireframe` and `ux-wireframe → ux-prototype-html` can often stay together.

Prefer a fresh chat for an independent critique, a clean handoff to engineering, or when a thread has become long. `ux-validate`, `dev-discovery`, and `dev-review` often benefit from fresh eyes. No skill should depend only on chat history: a new chat must reconstruct context from repository files, the active initiative, and Figma.

## Language policy

- Conversation, questions, clarifications, and progress follow the user's current language unless asked to switch.
- Durable artifacts are English by default. Precedence: explicit instruction in the current request, explicit artifact language recorded for the initiative, then English. Persist an initiative-wide language choice in `SPEC.md`.
- Product UI copy is independent of both. Infer it from explicit instruction, existing product, Figma, and product context; ask only when it is materially unclear.
- DEV skills preserve the same language-detection behavior.

## Durable project artifacts

Use the repository's existing conventions. A project may gradually use:

```text
AGENTS.md
product/CONTEXT.md
design/VISUAL_DIRECTION.md
design/DESIGN_SYSTEM.md
design/references/
work/<initiative>/SPEC.md
work/<initiative>/PLAN.md       # engineering plan, when useful
prototype/<initiative>/prototype.html
```

`SPEC.md` is the durable source of truth for an initiative. `CONTEXT.md` captures stable product context. `VISUAL_DIRECTION.md` describes visual intent; `DESIGN_SYSTEM.md` records reusable rules and the Figma/code contract. Skills preserve and extend useful existing files rather than creating parallel documentation. They inspect the repository before asking questions, distinguish known/inferred/assumed/unknown/conflicting information, and never silently turn assumptions into requirements.

## Definition of Done and workflow state

Every skill has a concise, observable Definition of Done. It is the final self-check that its required context was considered, its artifact was created or updated when appropriate, material uncertainty is visible, and a new chat can continue from durable state.

Each initiative SPEC has a compact `Workflow State`: current stage, confirmed decisions, open questions, relevant artifact references, and next recommended action. It is a reconstruction aid, not a project-management diary. Skills update it only when one of those facts materially changes.

## Just-in-time context and artifact ownership

Skills start with the smallest high-signal context for their job and retrieve more only when it can change a decision. For example, `ux-final-design` starts from the initiative SPEC, relevant wireframes/validation, visual direction, design-system contract, references, and Figma library; `dev-review` starts from the diff, SPEC/plan, changed code, and relevant tests. Neither needs a full-repository reading pass.

Ownership prevents duplicated or drifting documentation:

| Artifact | Primary owner |
|---|---|
| `AGENTS.md` | `ux-discovery`, `dev-discovery` |
| `product/CONTEXT.md` | `ux-discovery` |
| Visual direction and references | `ux-visual-direction` |
| Design-system contract and library | `ux-design-system` |
| Initiative `SPEC.md` | The relevant UX/DEV skill when initiative state changes |
| Wireframes / prototype / final design | `ux-wireframe` / `ux-prototype-html` / `ux-final-design` |
| Engineering plan / production code | `dev-plan` / `dev-implement` |

`AGENTS.md` remains deliberately small: stable repository-wide rules, context locations, universal conventions, and safety boundaries. Initiative requirements, temporary decisions, research, and feature history belong in the initiative artifacts.

## Validation layers

Three complementary checks answer different questions:

| Layer | Validates |
|---|---|
| `ux-validate` | Product design and its evidence |
| `dev-review` | Implementation against the approved plan/spec and engineering quality |
| Skill evals | Agent workflow behavior and skill contracts |

A visually good final design can still expose that `ux-final-design` ignored established visual direction; that is a skill-eval failure. Likewise, working code can still reveal that `dev-implement` ignored an approved plan. Product validation and implementation review do not replace workflow evaluation.

## Skill evals and maintenance

Repository-local, human-readable eval cases live in [`.evals/README.md`](.evals/README.md). They exercise behavioral contracts such as language handling, repository-first investigation, durable-state updates, ownership, prohibited behavior, and completion criteria. They are development infrastructure, not a user-facing command.

Do not add an instruction every time an agent makes one mistake. Instead: reproduce the failure; add or update an eval; identify whether the source is the description, instructions, missing project context, tooling, ownership, or model behavior; make the smallest useful change; rerun the relevant and adjacent evals; then remove obsolete instructions. Skills, templates, and `AGENTS.md` are versioned workflow infrastructure and should become simpler as models and tools improve.

## Why there are no subagents

This package currently uses one capable agent, focused skills, durable artifacts, repository/Figma/tools, explicit validation, and skill evals. This is a project workflow choice derived from context-management and evaluation principles, not a direct vendor requirement. Add subagents only when concrete eval evidence shows a particular workflow materially benefits from them.

## How much should I tell the skill?

Usually, very little:

```text
$skill-name

<one paragraph describing what you want>
```

Optionally attach screenshots, links, references, files, and requirements specific to this task. Do not repeat workflow rules already encoded in the skill: repository inspection, ambiguity handling, language policy, artifact ownership, component reuse, durable documentation, and validation happen automatically.

Good:

```text
$ux-visual-direction

Quiero que el producto se sienta más editorial. Me gusta la densidad de
Linear, pero no quiero que parezca una herramienta para developers.
```

```text
$dev-discovery

Quiero agregar soporte para equipos con múltiples administradores.
```

Unnecessary:

```text
$dev-discovery

Primero leé el repo. No hagas suposiciones. Preguntame lo que falta.
Respondeme en español y generá los MD en inglés.
```

Those are responsibilities of the skill. It may ask a focused question when the repository and supplied context cannot settle a material decision.

## Practical workflows

Examples are copy-pasteable Codex invocations. In Claude Code, invoke the same skill as `/ux-discovery`, etc. Each invocation expresses intent; the text underneath describes what the skill automatically recovers, may ask, and persists.

### A — Completely new product

**Starting point:** no product context, spec, design system, visual direction, or Figma. Begin in one chat while decisions are forming.

1. `$ux-discovery Quiero diseñar una aplicación para que equipos pequeños coordinen turnos de voluntariado.` It recovers what exists, asks only consequential product questions, and creates/updates the minimal context and SPEC. Stay in the chat while defining the problem.
2. `$ux-visual-direction Quiero una dirección visual sobria y editorial. Me gustan estas referencias: [URL 1], [URL 2].` It interprets and preserves visual evidence in `VISUAL_DIRECTION.md`.
3. `$ux-wireframe` It recovers the initiative and creates/reuses separate low-fidelity wireframes. Optional if flow structure is already clear.
4. Optional: `$ux-prototype-html Quiero probar en browser si crear un turno y anotarse resulta comprensible.` It creates one self-contained prototype using established context.
5. `$ux-validate` It identifies the available target, reviews it, and persists findings. Prefer a fresh chat for independence.
6. `$ux-design-system` It creates/reuses the separate system library and updates `DESIGN_SYSTEM.md` only as product need warrants.
7. `$ux-final-design` It creates/reuses a separate final-design file from the durable initiative and visual context. Validate again after material design changes.

### B — Existing codebase, undocumented product

**Starting point:** working repository/product, little documentation, no CONTEXT or initiative SPEC, perhaps no documented system. Discovery inspects relevant routes, components, copy, tests, roles, and assets before interviewing.

1. `$ux-discovery Quiero mejorar el flujo de invitación de usuarios.` It creates a minimal stable context and SPEC from evidence, and marks undocumented rules as unknown instead of inventing them. Stay in the same chat for wireframing if ambiguity is still being resolved.
2. `$ux-visual-direction Me gusta esta referencia: [URL].` Optional; it reads current UI and evolves visual intent/references.
3. `$ux-wireframe` and/or `$ux-final-design` as needed. Wireframe file, if useful, remains separate from final Figma. A prototype is optional for interaction uncertainty. `ux-design-system` is used only if reusable rules need to be formalized. Validate independently when useful.

### C — Mature product with established definitions

**Starting point:** `CONTEXT.md`, `DESIGN_SYSTEM.md`, `VISUAL_DIRECTION.md`, active library, and established UI patterns exist.

1. `$ux-discovery Quiero agregar bulk editing a la tabla de usuarios.` It reads existing files and relevant UI/Figma, then updates only the active SPEC/context if needed.
2. `$ux-final-design` may follow directly, reusing existing Figma system and patterns.
3. `$ux-validate` reviews the result and updates the SPEC. Wireframes, HTML prototypes, and visual-direction work are optional when current artifacts already settle those questions. Often stay together for a small iteration, then use a fresh chat for validation.

### D — Existing Figma files and component library

**Starting point:** product Figma, library, final screens, and perhaps wireframes already exist. Inspect and reuse them; do not create duplicates.

1. `$ux-design-system Quiero mejorar la librería actual para esta iniciativa.` It reads Figma libraries, variables, components, code tokens, and direction; then extends the existing library and `DESIGN_SYSTEM.md`.
2. `$ux-final-design Quiero llevar esta iniciativa a diseño final.` It reads SPEC and Figma, then updates a fitting final file or creates the separate destination when needed.

### E — Visual direction before discovery is complete

Visual direction may be gathered early without pretending product requirements are settled.

`$ux-visual-direction Todavía no definimos toda la funcionalidad, pero quiero ir fijando la dirección visual. Me gustan: [URL 1], [URL 2]. En la primera referencia me interesa la densidad y navegación; en la segunda, la tipografía. No quiero cards excesivamente redondeadas, gradients ni aspecto de SaaS genérico.`

Reads available context; records visual intent and unresolved choices in `VISUAL_DIRECTION.md` and references. It does not create screens or define requirements. Continue discovery in the same chat if useful.

### F — New visual references mid-project

`$ux-visual-direction Quiero sumar esta referencia: [URL].`

Reads current direction and stored evidence, extends rather than resets it, and records accepted changes. Later prototypes, design-system work, and final design consume the updated direction. Can run in a fresh chat because files are durable.

### G — Wireframe only

**Starting point:** an adequate active SPEC; need to reason about structure and flow without polish.

`$ux-wireframe Quiero explorar cómo debería funcionar este onboarding.`

Reads SPEC, context, relevant existing UI/Figma; writes low-fi frames to the dedicated wireframe file and links it in SPEC. Visual direction and system creation are not prerequisites. Same chat as discovery is fine.

### H — HTML prototype instead of Figma wireframes

`$ux-prototype-html Quiero validar esta interacción en browser antes de hacer el diseño final.`

Reads SPEC, `VISUAL_DIRECTION.md`, stored screenshots and reference URLs, current UI, system, and relevant Figma. Writes exactly one `prototype/<initiative>/prototype.html`. Use when interaction itself is the question; wireframes are optional. Follow with validation, often in a new chat.

### I — HTML prototype after wireframes

`$ux-discovery Quiero simplificar el alta de una organización.` → `$ux-wireframe` → `$ux-prototype-html Quiero probar la interacción elegida en browser.` → `$ux-validate`

Discovery and wireframing can share a chat; prototype can continue there for rapid iteration. The prototype turns structural decisions into interactive behavior and consumes visual references without cloning them. It is disposable UX code, not production code.

### J — Design-system-only work

**Starting point:** system needs organizing or extension independent of a particular screen.

`$ux-design-system Quiero ordenar y completar la librería existente.`

Reads Figma, implementation-facing tokens/components, visual direction, and docs; updates the existing system and `design/DESIGN_SYSTEM.md`. It does not require an initiative screen. A fresh chat works well when inputs are documented.

### K — Final design from wireframes

`$ux-final-design Quiero llevar esta iniciativa a diseño final.`

Reads all named durable sources and existing Figma. Writes to a separate high-fi final-design file. If a needed reusable component is missing, the skill records the gap and coordinates it with `ux-design-system`; it does not create an accidental parallel library. Follow with `ux-validate`, preferably fresh.

### L — Small feature in a mature product

`$ux-discovery Quiero agregar una acción de duplicar a las filas de esta tabla.` → `$ux-final-design` → new chat: `$ux-validate`

This minimal workflow is valid when structure, visual direction, and reusable components are already known. Running every skill would add process without resolving extra uncertainty.

### M — UX to DEV handoff

`$ux-discovery Quiero permitir reprogramar una invitación vencida.` → relevant wireframe/prototype/final design → `$ux-validate` → **new chat** `$dev-discovery Quiero implementar el comportamiento aprobado.` → `$dev-plan` → `$dev-implement` → **new chat** `$dev-review`

DEV skills consume product context, requirements, design links/system, and validation findings; the designer need not re-explain settled decisions. DEV owns production implementation and verification. Use `$dev-plan` for non-trivial work; minimal changes may not need a PLAN. Follow the existing DEV workflow.

## Installation

The canonical source is `.agents/skills/`. Codex reads it directly. `.claude/skills/` contains symlinks to those same skill folders for Claude Code; these are links, not duplicated files.

```text
.agents/skills/                  # one copy of skills and resources
.claude/settings.json            # Claude-specific invocation policy
.claude/skills/<skill-name>      # symlink to .agents/skills/<skill-name>
```

Clone and open the repository in either host. Git must preserve symlinks; if a platform/client does not, enable symlink support or copy the canonical skill folders into `.claude/skills/` locally. Codex-only metadata such as `agents/openai.yaml` is ignored by Claude Code. The checked-in Claude setting keeps visual direction manually invoked, matching its Codex metadata.

Global installation is also possible by copying each skill folder into `~/.agents/skills/` for Codex or `~/.claude/skills/` for Claude Code.

## UX / DEV boundary

UX produces specs, Figma artifacts, visual/design-system documentation, validation findings, and the standalone HTML prototype. It never implements production application code. Once design decisions and acceptance criteria are ready, DEV takes over technical discovery, planning, implementation, and review using the durable artifacts.

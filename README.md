# AI Skills for Codex and Claude Code

One shared skill source for product design and software development. The UX skills help a designer investigate, explore, prototype, systematize, finalize, and validate product experiences. They do not implement production application code. DEV skills own engineering implementation.

Codex invocation uses `$skill-name`; Claude Code uses `/skill-name`. Examples below use Codex syntax. Skills inspect durable repository and Figma context on every invocation, so a workflow can span chats. **Chat is working memory; repository artifacts are durable product memory; Figma is the durable design artifact.**

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

## Practical workflows

Examples are copy-pasteable Codex invocations. In Claude Code, invoke the same skill as `/ux-discovery`, etc. Each step lists its typical reads, writes, and chat recommendation; existing files are updated or reused rather than duplicated.

### A — Completely new product

**Starting point:** no product context, spec, design system, visual direction, or Figma. Begin in one chat while decisions are forming.

1. `$ux-discovery Quiero diseñar una aplicación para que equipos pequeños coordinen turnos de voluntariado. No hay producto previo; ayudame a definir usuarios, problema, alcance y riesgos antes de diseñar.` Reads what exists; asks about consequential unknowns; creates/updates `AGENTS.md`, `product/CONTEXT.md`, and `work/<initiative>/SPEC.md` as justified. Stay in the chat.
2. `$ux-visual-direction Tengo estas referencias: [URL 1] y [URL 2]. De la primera me interesa la claridad de navegación; de la segunda, el tono tipográfico. Evitemos una estética corporativa genérica.` Reads the SPEC/context and supplied refs; creates `design/VISUAL_DIRECTION.md` and optionally annotated saved references. Same chat or later, since the direction is durable.
3. `$ux-wireframe Explorá el flujo principal y los estados alternativos en un archivo Figma de wireframes separado.` Reads SPEC/context and relevant Figma; creates/reuses `<Product> — <Initiative> — Wireframes`. Optional if the flow is already obvious.
4. Optional: `$ux-prototype-html Quiero probar en browser si crear un turno y anotarse resulta comprensible. Usá la dirección visual y las referencias guardadas.` Reads SPEC, visual direction, screenshots/URLs, system if any, and wireframes; writes only `prototype/<initiative>/prototype.html`.
5. `$ux-validate Revisá el prototipo y los wireframes contra el objetivo y los riesgos del SPEC.` Reads design and evidence; writes findings/status to SPEC. Prefer a fresh chat for independence.
6. `$ux-design-system Definí sólo las foundations y componentes que necesita este producto según VISUAL_DIRECTION.md y los flujos explorados.` Creates/reuses the separate Figma library and updates `design/DESIGN_SYSTEM.md`. Optional if no reusable system is needed yet.
7. `$ux-final-design Convertí el flujo aprobado en pantallas high-fidelity. Usá el design system y mantené un archivo Figma separado de wireframes.` Reads all durable inputs and validation findings; creates/reuses `<Product> — <Initiative> — Final Design`. Validate again after material design changes. This order resolves product and structural uncertainty before investing in polish.

### B — Existing codebase, undocumented product

**Starting point:** working repository/product, little documentation, no CONTEXT or initiative SPEC, perhaps no documented system. Discovery inspects relevant routes, components, copy, tests, roles, and assets before interviewing.

1. `$ux-discovery Quiero mejorar el flujo de invitación de usuarios. Revisá primero el repositorio y preguntame sólo lo que no puedas determinar.` Creates a minimal stable context and SPEC from evidence, marks undocumented rules as unknown instead of inventing them. Stay in the same chat for wireframing if ambiguity is still being resolved.
2. `$ux-visual-direction Revisá las pantallas actuales y estas referencias [URL]. Conservá lo que sea coherente con el producto y registrá las diferencias.` Optional; reads current UI and adds visual intent/references.
3. `$ux-wireframe` and/or `$ux-final-design` as needed. Wireframe file, if useful, remains separate from final Figma. A prototype is optional for interaction uncertainty. `ux-design-system` is used only if reusable rules need to be formalized. Validate independently when useful.

### C — Mature product with established definitions

**Starting point:** `CONTEXT.md`, `DESIGN_SYSTEM.md`, `VISUAL_DIRECTION.md`, active library, and established UI patterns exist.

1. `$ux-discovery Quiero agregar bulk editing a la tabla de usuarios. Revisá el SPEC y los patrones existentes; preguntame sólo por reglas que no estén documentadas.` Reads existing files and relevant UI/Figma; updates only the active SPEC/context if needed.
2. `$ux-final-design` may follow directly, reusing existing Figma system and patterns.
3. `$ux-validate` reviews the result and updates the SPEC. Wireframes, HTML prototypes, and visual-direction work are optional when current artifacts already settle those questions. Often stay together for a small iteration, then use a fresh chat for validation.

### D — Existing Figma files and component library

**Starting point:** product Figma, library, final screens, and perhaps wireframes already exist. Inspect and reuse them; do not create duplicates.

1. `$ux-design-system Auditá y extendé el design system existente para soportar esta iniciativa. No crees una librería nueva si la actual se puede extender.` Reads Figma libraries, variables, components, code tokens, and visual direction; updates existing library and `DESIGN_SYSTEM.md`.
2. `$ux-final-design Usá el design system y los archivos existentes de Figma. Creá un archivo final separado para esta iniciativa sólo si no existe uno adecuado.` Reads SPEC and Figma; updates a fitting final file or creates the separately named one. Wireframes stay in their own file.

### E — Visual direction before discovery is complete

Visual direction may be gathered early without pretending product requirements are settled.

`$ux-visual-direction Todavía no definimos toda la funcionalidad, pero quiero ir fijando la dirección visual. Me gustan: [URL 1], [URL 2]. En la primera referencia me interesa la densidad y navegación; en la segunda, la tipografía. No quiero cards excesivamente redondeadas, gradients ni aspecto de SaaS genérico.`

Reads available context; records visual intent and unresolved choices in `VISUAL_DIRECTION.md` and references. It does not create screens or define requirements. Continue discovery in the same chat if useful.

### F — New visual references mid-project

`$ux-visual-direction Agregá estas nuevas referencias a la dirección visual existente: [URL]. No reemplaces automáticamente lo anterior; identificá conflictos y preguntame cuando una decisión no sea compatible.`

Reads current direction and stored evidence, extends rather than resets it, and records accepted changes. Later prototypes, design-system work, and final design consume the updated direction. Can run in a fresh chat because files are durable.

### G — Wireframe only

**Starting point:** an adequate active SPEC; need to reason about structure and flow without polish.

`$ux-wireframe Usá el SPEC existente para explorar la estructura, jerarquía, navegación, estados y alternativas relevantes. Mantenelo low-fidelity; no definas estilo visual final.`

Reads SPEC, context, relevant existing UI/Figma; writes low-fi frames to the dedicated wireframe file and links it in SPEC. Visual direction and system creation are not prerequisites. Same chat as discovery is fine.

### H — HTML prototype instead of Figma wireframes

`$ux-prototype-html Quiero validar la interacción en browser antes de hacer el diseño final. Usá la dirección visual y las referencias existentes para evitar un estilo genérico.`

Reads SPEC, `VISUAL_DIRECTION.md`, stored screenshots and reference URLs, current UI, system, and relevant Figma. Writes exactly one `prototype/<initiative>/prototype.html`. Use when interaction itself is the question; wireframes are optional. Follow with validation, often in a new chat.

### I — HTML prototype after wireframes

`$ux-discovery Quiero simplificar el alta de una organización; inspeccioná el flujo actual y definamos los requisitos.` → `$ux-wireframe Explorá dos modelos de navegación para este flujo en Figma low-fi.` → `$ux-prototype-html Implementá en un único HTML la interacción del modelo elegido. Conservá la estructura de wireframes y aplicá la dirección visual guardada.` → `$ux-validate Revisá el flujo y el prototipo; separá problemas observables de hipótesis.`

Discovery and wireframing can share a chat; prototype can continue there for rapid iteration. The prototype turns structural decisions into interactive behavior and consumes visual references without cloning them. It is disposable UX code, not production code.

### J — Design-system-only work

**Starting point:** system needs organizing or extension independent of a particular screen.

`$ux-design-system Quiero ordenar y completar la librería existente. Revisá Figma, los tokens del repo y VISUAL_DIRECTION.md antes de proponer cambios. Extendé la librería actual.`

Reads Figma, implementation-facing tokens/components, visual direction, and docs; updates the existing system and `design/DESIGN_SYSTEM.md`. It does not require an initiative screen. A fresh chat works well when inputs are documented.

### K — Final design from wireframes

`$ux-final-design Tomá los wireframes de esta iniciativa y convertí la dirección aprobada en diseño final. Usá el design system existente, VISUAL_DIRECTION.md, las referencias visuales guardadas y los findings de validación. No cambies silenciosamente el flujo definido en el SPEC.`

Reads all named durable sources and existing Figma. Writes to a separate high-fi final-design file. If a needed reusable component is missing, the skill records the gap and coordinates it with `ux-design-system`; it does not create an accidental parallel library. Follow with `ux-validate`, preferably fresh.

### L — Small feature in a mature product

`$ux-discovery Quiero agregar una acción de duplicar a las filas de esta tabla. Revisá patrones y reglas existentes.` → `$ux-final-design` → new chat: `$ux-validate Revisá la propuesta contra el SPEC y el design system.`

This minimal workflow is valid when structure, visual direction, and reusable components are already known. Running every skill would add process without resolving extra uncertainty.

### M — UX to DEV handoff

`$ux-discovery Quiero permitir reprogramar una invitación vencida. Inspeccioná el comportamiento actual y documentá reglas y criterios.` → relevant wireframe/prototype/final design → `$ux-validate` → **new chat** `$dev-discovery Implementá el comportamiento aprobado en work/<initiative>/SPEC.md. Revisá el repo, la especificación, los links Figma y design/DESIGN_SYSTEM.md antes de preguntar.` → `$dev-plan` → `$dev-implement` → **new chat** `$dev-review Revisá el diff contra work/<initiative>/SPEC.md y las convenciones de ingeniería.`

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

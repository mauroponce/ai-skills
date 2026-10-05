# Interactive Decision Policy

This policy is for decision-oriented skills shared by Codex and Claude Code. Start the decision phase in Plan mode with `/plan`; a skill cannot switch the current agent's mode. Claude Code's Plan mode is read-only, so investigate and resolve decisions there, then leave Plan mode before creating or updating project artifacts. Follow the same boundary in Codex when its active Plan mode is read-only.

## Investigate first

Inspect the relevant repository, documentation, product/design files, references, requirements, and existing decisions before asking. Resolve discoverable facts through investigation; ask only about a human preference or product/technical decision that evidence cannot settle.

## Ask only material questions

Ask only when the answer materially changes requirements, user behavior, visual direction, product/architecture tradeoffs, or an important assumption. Do not ask about routine implementation details or optional preferences that can be handled with a reasonable repository-backed assumption. Stop when downstream work can proceed without inventing a material decision.

## Use native structured input

Use the host's native structured question mechanism when available: Codex `request_user_input` or Claude Code `AskUserQuestion`. Offer a small set of concrete, realistic options derived from evidence and explain the tradeoff briefly. Recommend an option when repository constraints, existing conventions, or strong usability/architecture evidence support one. Let the user provide a custom answer when the tool supports it; options are not exhaustive. Do not imitate interactive controls with plain-text option menus.

Ask no more than 1–3 questions per round, usually one decision at a time. Incorporate the answer, continue any needed investigation, and ask another small round only if material ambiguity remains.

If structured input is unavailable, ask one concise question in ordinary conversation.

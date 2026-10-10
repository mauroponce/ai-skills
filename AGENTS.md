# Repository Instructions for Codex

- Canonical Codex skills live in `.agents/skills/`; use the relevant skill and load shared references only when they help the task.
- Keep public DEV and UX skills focused on user goals. Reusable engineering knowledge belongs in `.agents/skills/references/engineering/`; Codex workflow guidance belongs in the skill or shared orchestration references.
- Use `AGENTS.md` for small, stable repository-wide rules. Keep initiative requirements in `work/<initiative>/SPEC.md`, implementation plans in `PLAN.md` when warranted, and transient hypotheses in the active conversation.
- Preserve the read-only production boundary in `dev-debug` and the explicit production deployment approval boundary in `dev-release`.
- After editing a skill, run a skill validator when available; check changed links and relevant behavioral eval cases.

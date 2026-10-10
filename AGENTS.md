# Repository Instructions for Codex

- Canonical Codex skills live in `.agents/skills/`; use the relevant skill and load shared references only when they help the task.
- Keep public DEV and UX skills focused on user goals. Reusable engineering knowledge belongs in `.agents/skills/references/engineering/`; Codex workflow guidance belongs in the skill or shared orchestration references.
- In this harness repository, keep `AGENTS.md` for small, stable repository-wide rules. Skills running in target projects keep workflow context in chat or the personal Codex workspace; they do not create tracked SPEC/PLAN/AGENTS/process files by default.
- Preserve the read-only production boundary in `dev-debug` and the explicit production deployment approval boundary in `dev-release`.
- After editing a skill, run a skill validator when available and check changed links.

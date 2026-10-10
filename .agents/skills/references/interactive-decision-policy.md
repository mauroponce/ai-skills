# Codex Interactive Decision Policy

Use this policy for decision-oriented Codex skills. Inspect the repository, product/design context, and existing decisions before asking the user. Resolve discoverable facts yourself; ask only when a human preference or consequential product, design, security, data, or architecture decision remains.

If the current Codex session offers Plan mode, it can help investigate and compare options. Do not require a slash command or assume every Codex surface exposes the same mode. When the active mode is read-only, finish the decision work there and switch to a writable mode before saving personal notes or implementing task-required project changes. A skill cannot change the active mode by itself.

Use Codex's available structured input tool for a material choice when it improves the answer; otherwise ask one concise question in conversation. Offer a small set of evidence-based options and a recommendation when supported. Ask no more than 1–3 questions per round, usually one decision at a time. Continue once downstream work can proceed without inventing a material decision.

Codex sandbox and approval settings govern tool execution. Do not treat a writable sandbox as authorization for a high-impact external action; follow the skill's explicit approval boundary, especially for production deployment. Do not ask for approval for routine investigation or reversible repository work already authorized by the user's task.

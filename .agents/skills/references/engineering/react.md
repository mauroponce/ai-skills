# React Playbook

Use the detected React version, integration (SPA, islands, Inertia, react-rails, etc.), build system, state/data libraries, components, and test conventions.

Keep components cohesive and prefer composition and existing design-system components over abstractions that only reduce line count. Establish a single source of truth: derive values when possible and avoid duplicated or unnecessarily synchronized state. Treat `useEffect` as synchronization with an external system, not a general procedural mechanism; inspect dependency correctness, stale closures, cleanup, async races, and effects that merely derive state.

For async UI, cover loading, success, errors, cancellation/stale responses, retries, optimistic updates, and double submission as relevant. Follow existing form conventions and account for server/field errors, dirty/submitting state, focus, and accessible feedback.

Evaluate rendering performance from evidence: list size, keys, expensive calculations, avoidable rerenders, bundle impact, or measured hot paths. Do not add memoization mechanically. For UI work, use semantic HTML, keyboard interactions, labels, focus order/management, native dialog/menu behavior where possible, and ARIA only when needed. Verify frontend/backend request, response, error, nullability, pagination, authorization, and compatibility contracts rather than assuming them.

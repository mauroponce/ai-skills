# Web Security Playbook

Apply by risk, not as a checklist for harmless changes. Inspect actual auth, authorization, tenancy, session, input, and deployment boundaries.

Consider authentication and session lifecycle, object-level authorization/IDOR, multi-tenant scoping, CSRF, XSS, SQL/command injection, SSRF, open redirects, mass assignment, uploads, CORS, CSP when applicable, secrets, sensitive logging, rate limits, token exposure, password reset, email verification, and API-token behavior.

For OAuth/OIDC and account linking, assess provider identity verification, state and nonce where applicable, redirect URI handling, scopes, token storage, provider failures, session rotation/fixation, existing-email conflicts, linking policy, and account ownership. Never silently link accounts solely from a matching email when the policy and verification semantics are not established.

# Source and Version Verification

When framework or dependency behavior could materially change a decision, establish the **installed version** from lockfiles, runtime/configuration, and local source or documentation. Then consult authoritative upstream documentation for that version when local evidence is insufficient. State the version and source supporting a version-specific claim. If the installed version or behavior cannot be confirmed, label the uncertainty and propose a safe check.

Apply selectively to the detected language, framework, database, frontend, authentication libraries, and deployment tooling. In particular, verify version-sensitive migrations, locking, callbacks, job serialization, error reporting, security defaults, and API deprecations. Routine use of established repository code does not require external research. Prefer official framework/database documentation and upstream release notes over remembered APIs or unsourced advice.

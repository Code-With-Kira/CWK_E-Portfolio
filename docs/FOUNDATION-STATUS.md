# Repository Foundation Status

**Plan:** RFP-CWK-001 Version 1.0 — Approved planning baseline  
**Implementation authorization:** Explicitly granted by the project owner for repository foundation work  
**Working branch:** `chore/repository-foundation`  
**Status:** Partial foundation established; application implementation and readiness remain blocked pending unresolved decisions.

## Implemented in this branch

- Node.js major-version selectors for Node.js 24 LTS (`.nvmrc`, `.node-version`).
- Repository `.gitignore` for common Node.js / Next.js generated output and local secrets.
- Root README describing the governing baseline, content workflow, and security boundaries.
- Repository-level GitHub Copilot instructions derived from the approved project decisions and known pending constraints.

## Deliberately deferred

The following are not created or finalized because the approved documents leave decisions pending or the exact contract has not been verified:

- `package.json`, `package-lock.json`, and dependency versions.
- Next.js app routes and feature-specific source directories.
- Public route map and API endpoint contracts.
- Content schemas and owner-provided portfolio content.
- `.env.example` variable names and integration configuration.
- ESLint / Prettier configuration and npm script commands.
- GitHub Actions CI workflow, until package scripts and dependency installation are established.
- Playwright configuration and browser setup.
- Cookie identity/lifetime/signing, CSRF and rate-limit policy.
- Redis retention, backup, and recovery.
- GitHub API caching, rate-limit handling, and fallback policy.
- Analytics event definitions, deployment settings, monitoring, and domain configuration.
- UI tokens, responsive breakpoints, detailed interactions, and final asset mapping.

## Verification required before expanding the foundation

1. Reconcile the complete SDD route map with SRS and UIR.
2. Confirm dependency/version policy and compatible framework/tool versions under TSS.
3. Confirm module boundaries and content schemas.
4. Verify API contracts and integration security requirements.
5. Define the required environment variables and deployment environments.
6. Define CI triggers, permissions, required checks, and exact npm scripts.
7. Record remaining decisions and evidence against IRC-CWK-001.

## Boundary

This branch contains repository foundation scaffolding only. It does not claim that the application is runnable, that CI is operational, or that implementation readiness has been achieved. Do not merge to `main` until the project owner reviews the branch and the applicable IRC gates are satisfied.

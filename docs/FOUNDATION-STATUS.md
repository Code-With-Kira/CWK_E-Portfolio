# Repository Foundation Status

**Plan:** RFP-CWK-001 Version 1.0 — approved planning baseline  
**Implementation authorization:** Explicitly granted by the project owner for repository foundation work  
**Working branch:** `chore/repository-foundation`  
**Status:** Source documents inspected; decision register updated; application setup remains partial.

## Implemented in this branch

- Node.js major-version selectors for Node.js 24 LTS (`.nvmrc`, `.node-version`).
- Repository `.gitignore` for common Node.js / Next.js generated output and local secrets.
- Root README describing the governing baseline, content workflow, and security boundaries.
- Repository-level GitHub Copilot instructions derived from approved project decisions and known pending constraints.
- `docs/FOUNDATION-COMPLETION-REVIEW.md` — initial foundation review.
- `docs/FOUNDATION-DECISION-REGISTER.md` — source-grounded route proposal, module architecture, API endpoint register, configuration register, and implementation disposition.
- `.env.example` — names explicitly listed in SDD-CWK-001 v1.0 only; no secret values.

## Source-document findings now recorded

- The SDD includes a proposed App Router route table. The SRS still marks final route/URL mapping as pending (PD-014), and the SDD requires reconciliation with approved UI navigation and the SRS.
- The SDD defines seven modules and five architecture layers; these are recorded in the decision register.
- The SDD lists `/api/contact`, `/api/likes`, and `/api/github` endpoint responsibilities, but not complete machine-ready request/response contracts.
- The SDD lists the environment-variable names now represented in `.env.example`. Values, provider setup, and several operational policies remain pending.

## Deliberately deferred

- Full portfolio route tree until PD-014 and the UIR navigation/page mapping are reconciled.
- Contact, likes, and GitHub Route Handlers until complete API contracts and feature-specific security controls are defined.
- `package.json`, `package-lock.json`, and dependency versions until a compatible exact dependency set can be installed and a real npm lockfile generated.
- ESLint / Prettier configuration and npm scripts until package setup is established.
- GitHub Actions CI workflow until deterministic scripts and the committed npm lockfile exist.
- Playwright configuration and browser setup.
- Cookie lifetime/rotation, exact CSRF and rate-limit policy, Redis retention/backup/recovery, GitHub caching/fallback, analytics event definitions, deployment settings, monitoring, and domain configuration.
- UI tokens, responsive breakpoints, detailed interactions, and final asset mapping.

## Next implementation sequence

1. Reconcile the SDD route proposal with all SRS requirements and UIR navigation, then obtain explicit resolution of PD-014 where the sources do not settle a path.
2. Complete machine-readable API contracts and the security/configuration decisions required by each endpoint.
3. Establish a compatible exact dependency set, install it, and commit the generated `package-lock.json`.
4. Add deterministic npm scripts, TypeScript/ESLint/Prettier/Tailwind configuration, and the minimal Next.js App Router foundation.
5. Add GitHub Actions using `npm ci`, lint, type checking, unit/component tests, and production build; add Playwright only after browser setup is established.
6. Record current evidence against IRC-CWK-001.

## Boundary

This branch remains isolated from `main`. It does not claim that the application is runnable, CI is operational, all routes are finalized, or implementation/production readiness has been achieved. Do not merge to `main` until the project owner reviews the branch and applicable IRC gates are satisfied.

# Repository Foundation Status

**Plan:** RFP-CWK-001 Version 1.0 — approved planning baseline  
**Implementation authorization:** Explicitly granted by the project owner for repository foundation work  
**Working branch:** `chore/repository-foundation`  
**Status:** Package/configuration candidate committed; npm installation, lockfile generation, and execution verification blocked by the available environment.

## Implemented in this branch

- Node.js major-version selectors for Node.js 24 LTS (`.nvmrc`, `.node-version`).
- Repository `.gitignore` for common Node.js / Next.js generated output and local secrets.
- Root README describing the governing baseline, content workflow, and security boundaries.
- Repository-level GitHub Copilot instructions derived from approved project decisions and known pending constraints.
- `docs/FOUNDATION-COMPLETION-REVIEW.md` — initial foundation review (historical; read with newer decision and route records).
- `docs/FOUNDATION-DECISION-REGISTER.md` — source-grounded route proposal, module architecture, API endpoint register, configuration register, and implementation disposition.
- `.env.example` — names explicitly listed in SDD-CWK-001 v1.0 only; no secret values.
- `docs/ROUTE-RECONCILIATION.md` — comparison of SDD proposed routes against SRS PD-014 and UIR page inventory; unmapped identities and owner decisions recorded.
- `package.json` — exact-version dependency candidate manifest and initial npm scripts.
- `.npmrc` — enforces Node.js engine constraints and exact direct-dependency saves.
- `tsconfig.json`, `next.config.ts`, `postcss.config.mjs`, `eslint.config.mjs`, `.prettierrc.json`, `.prettierignore`, and `vitest.config.ts`.
- `docs/DEPENDENCY-BASELINE.md` — records selected package versions, rationale, and verification limits.

## Dependency baseline

The manifest selects exact candidate versions for Next.js 16.4.6, React 19.3.1, Tailwind CSS 4.3.5, TypeScript 7.0.2, ESLint 10.15.0, Prettier 3.10.1, Vitest 5.1.1, Zod 4.6.7, and supporting type/test packages. The approved TSS does not prescribe exact versions; these are implementation selections and remain subject to installation/peer compatibility checks.

## Verified source findings

- SDD Section 5.2 contains a **proposed** App Router route table and explicitly requires reconciliation with UI navigation and the SRS.
- SRS PD-014 marks final page routes and URL structure pending.
- UIR identifies page/component identities that do not each map to a standalone SDD route.
- The SDD defines seven modules and five architecture layers.
- The SDD lists `/api/contact`, `/api/likes`, and `/api/github` responsibilities, but not complete machine-ready request/response contracts.
- TSS approves Node.js 24 LTS, npm, GitHub Actions, ESLint, Prettier, and React built-in state management.

## Verification blocker

The available execution container reports Node.js 22.16.0, not the approved Node.js 24 LTS. DNS resolution to `nodejs.org` and `registry.npmjs.org` failed. Therefore:

- Dependencies have **not** been installed.
- `package-lock.json` has **not** been generated.
- Peer dependency compatibility has **not** been verified.
- ESLint, TypeScript, Prettier, Vitest, and Next.js build commands have **not** been run.
- No CI workflow is added until a genuine lockfile exists and all scripts are deterministic.

The candidate exact versions and their source references are recorded in `docs/DEPENDENCY-BASELINE.md`. They must be verified by a real npm install under Node.js 24 before the package baseline is called complete.

## Still deliberately deferred

- Full portfolio route tree until PD-014 and original UI navigation reconciliation are resolved.
- Contact, likes, and GitHub Route Handlers until complete API contracts and feature-specific security controls are defined.
- Playwright dependency/browser setup.
- Cookie lifetime/rotation, CSRF and rate-limit policy, Redis retention/backup/recovery, GitHub caching/fallback, analytics event definitions, deployment settings, monitoring, and domain configuration.
- UI tokens, responsive breakpoints, detailed interactions, and final asset mapping.

## Next implementation sequence

1. Run `npm install` under Node.js 24 with registry access; resolve peer conflicts and commit the generated `package-lock.json`.
2. Run and fix `npm run format:check`, `npm run lint`, `npm run typecheck`, `npm test`, and `npm run build`.
3. Add the minimal Next.js App Router root foundation after the package/toolchain is verified; do not invent unresolved route destinations or UI design.
4. Close PD-014 and complete API contract/security decisions before adding feature routes and handlers.
5. Add GitHub Actions using `npm ci` and verified scripts; add Playwright only after browser setup is established.
6. Record evidence against IRC-CWK-001.

## Boundary

This branch remains isolated from `main`. It does not claim the application is runnable, CI is operational, all routes are finalized, or implementation/production readiness has been achieved. Do not merge to `main` until the project owner reviews the branch and applicable IRC gates are satisfied.

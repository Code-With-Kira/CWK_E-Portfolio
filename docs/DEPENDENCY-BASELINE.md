# Dependency Baseline Record

**Record ID:** DBR-CWK-001
**Version:** 1.1
**Date:** 2026-11-22
**Status:** Dependencies installed; partial local verification completed

## 1. Governing decisions

The approved TSS establishes Node.js 24 LTS, npm, Next.js, React, TypeScript, Tailwind CSS with custom CSS, Zod, Vitest, React Testing Library, ESLint, and Prettier.

The TSS does not prescribe exact dependency versions. This record documents implementation-level version selections and compatibility adjustments. These selections do not retroactively amend the approved TSS.

## 2. Runtime and package manager

- Node.js: `24.x`, enforced by `package.json` engines and `.npmrc`.
- Verified local runtime: Node.js `24.22.3`.
- Verified npm version: `11.19.1`.
- Package manager: npm, as approved by TSS.
- Lockfile: `package-lock.json`, generated through npm installation.
- `save-exact=true` keeps future direct dependency additions pinned.
- `engine-strict=true` prevents installation under an unsupported Node major.
- NVM for Windows is used locally to manage Node.js versions. The existing Node.js 26 installation is retained.

## 3. Exact versions selected in package.json

| Package                   | Version | Role                         |
| ------------------------- | ------: | ---------------------------- |
| next                      |  16.4.6 | App Router framework         |
| react                     |  19.3.1 | UI library                   |
| react-dom                 |  19.3.1 | React DOM renderer           |
| zod                       |   4.6.7 | Runtime validation           |
| @tailwindcss/postcss      |   4.3.5 | Tailwind PostCSS integration |
| tailwindcss               |   4.3.5 | Styling framework            |
| typescript                |   6.0.3 | TypeScript compiler          |
| @types/node               | 24.19.2 | Node.js 24 type definitions  |
| @types/react              |  19.3.0 | React type definitions       |
| @types/react-dom          |  19.3.0 | React DOM type definitions   |
| eslint                    |  9.39.5 | Linting                      |
| eslint-config-next        |  16.4.6 | Next.js lint rules           |
| prettier                  |  3.10.1 | Formatting                   |
| vitest                    |   5.1.1 | Unit testing                 |
| @testing-library/react    |  16.3.3 | React component testing      |
| @testing-library/dom      |  10.4.2 | Testing Library DOM peer     |
| @testing-library/jest-dom |   8.0.0 | DOM assertions               |
| jsdom                     |  31.0.1 | DOM test environment         |

All direct dependency versions are pinned exactly in `package.json`.

## 4. Compatibility adjustments

The initial candidate versions of TypeScript 7.0.2 and ESLint 10.15.0 produced compatibility issues during local verification.

The following adjustments were made:

- TypeScript was changed to `6.0.3` because the installed `typescript-eslint` parser reported that it did not support TypeScript 7.0.
- ESLint was changed to `9.39.5` because the installed Next.js ESLint plugins declared peer compatibility through ESLint 9.
- These are implementation compatibility adjustments, not changes to the approved technology stack.

npm reported that ESLint `9.39.5` is deprecated. Treat this as a temporary compatibility selection requiring a future supported-version review.

## 5. Installation and verification record

Local environment:

- Windows 11.
- Node.js `24.22.3`.
- npm `11.19.1`.
- Git `2.56.1.windows.1`.

Installation:

- `npm install` completed successfully.
- `package-lock.json` was generated.
- npm reported zero vulnerabilities in the initial installation.
- A subsequent `npm audit` also reported zero vulnerabilities.
- npm emitted peer-dependency override warnings during dependency adjustments.

Verification results:

| Check               | Result  | Notes                                                                                    |
| ------------------- | ------- | ---------------------------------------------------------------------------------------- |
| Node.js runtime     | Passed  | Node.js 24.22.3                                                                          |
| npm installation    | Passed  | `npm install` completed successfully                                                     |
| Clean installation  | Passed  | `npm ci` completed successfully                                                          |
| Lockfile generation | Passed  | `package-lock.json` generated locally                                                    |
| TypeScript          | Passed  | `npm run typecheck` completed successfully                                               |
| ESLint              | Partial | Exit code 0; missing Pages directory warning remains                                     |
| npm audit           | Passed  | Zero vulnerabilities reported                                                            |
| Vitest              | Pending | No test files have been created                                                          |
| Production build    | Pending | No application `app` or `pages` directory exists                                         |
| Prettier            | Passed  | `npm run format:check` completed successfully; all matched files use Prettier code style |
| CI                  | Pending | GitHub Actions workflow not implemented                                                  |

The ESLint command currently reports that it cannot find a `pages` directory. Its exit code is zero, but this warning must be reviewed when the approved application structure is implemented.

The Vitest and production-build checks cannot be considered passed because the application source and test files have not yet been created.

## 6. Intentionally excluded for now

- Playwright package and browser installation: defer until the E2E browser setup is selected and verified.
- Resend, Upstash Redis, and GitHub SDK clients: use only after service contracts and integration requirements are finalized; direct service integration may use supported HTTP APIs.
- Vercel Analytics package: defer until deployment and analytics configuration are verified.
- UI component libraries, animation libraries, state-management libraries, and CMS packages: not approved or required by the current baseline.

## 7. Outstanding actions

1. Review and resolve the ESLint missing-directory warning when the approved Next.js route structure is implemented.
2. Review ESLint's deprecated-version notice and select a supported compatible version.
3. Resolve the Vitest configuration warning.
4. Add actual tests alongside implemented application modules.
5. Verify the production build after implementing the approved application structure.
6. Add GitHub Actions after local verification and CI requirements are established.
7. Review and commit the generated lockfile together with the package manifest and this record.

## 8. Source references

- TSS-CWK-001 Version 1.0 Revision 1, approved stack and tool decisions.
- SDD-CWK-001 Version 1.0, proposed architecture and configuration.
- Next.js installation and system requirements: https://nextjs.org/docs/app/getting-started/installation
- Next.js support policy: https://nextjs.org/support-policy
- Local npm installation, verification output, and dependency compatibility diagnostics dated 2026-11-22.

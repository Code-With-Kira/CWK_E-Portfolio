# CodeWithKira E-Portfolio System

Repository foundation for the CodeWithKira E-Portfolio System.

## Governing baseline

Implementation must follow the approved project documents:

- SRS-CWK-001 Version 1.0
- SDD-CWK-001 Version 1.0
- TSS-CWK-001 Version 1.0 Revision 1
- CPI-CWK-001 Version 1.0
- IRC-CWK-001 Version 1.0
- UIR-CWK-001 Version 1.0 and the original UI reference files

The approved UI references are authoritative. Do not invent or redesign page layouts, routes, content, interactions, responsive behavior, or assets where the source documents leave them unresolved.

## Runtime

- Node.js 24 LTS
- npm

Use the Node.js version declared in `.nvmrc` / `.node-version`. Once the approved dependency manifest and lockfile are added, use `npm ci` for reproducible installs.

## Project status

The repository foundation is being established on the `chore/repository-foundation` branch. This is not a declaration that the application is implementation-ready.

Exact dependency versions, canonical routes, content schemas, API contracts, environment-variable names, CI commands, integration policies, and operational settings remain subject to the approved documents and outstanding verification decisions. See [docs/FOUNDATION-STATUS.md](docs/FOUNDATION-STATUS.md).

## Content workflow

Portfolio content is maintained directly in the repository using the approved JSON/MDX approach and edited through VS Code. A browser-based CMS or admin dashboard is not part of the approved approach.

## Security

Never commit secrets, credentials, access tokens, private keys, or populated local environment files. Server-only credentials must never be exposed through client-side code or public environment variables.

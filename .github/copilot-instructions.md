# Repository instructions — CodeWithKira E-Portfolio

## Authority and change control

- Follow the approved SRS-CWK-001 v1.0, SDD-CWK-001 v1.0, TSS-CWK-001 v1.0 Revision 1, CPI-CWK-001 v1.0, IRC-CWK-001 v1.0, UIR-CWK-001 v1.0, and the original UI reference files.
- The original UI reference files are authoritative for visual design. Do not redesign, simplify, embellish, or invent UI details.
- If instructions conflict, the governing approved project documents take precedence over inferred conventions or generated suggestions.
- Do not silently resolve pending decisions. Identify the conflict or missing decision and request an approved clarification.
- Do not treat planning-document approval as approval of every unresolved detail.

## Approved technology and architecture

- Use the approved Next.js, React, TypeScript, Tailwind CSS with custom CSS, Node.js 24 LTS, and npm baseline.
- Preserve the modular-monolith architecture.
- Use React built-in state management; do not add a global state library without explicit approval.
- Use JSON and MDX for repository-managed portfolio content. Content is maintained in VS Code; do not add a browser CMS or admin dashboard.
- Use Zod for runtime validation and Next.js Route Handlers for approved server endpoints.
- Preserve the approved integration responsibilities: Resend for direct contact email delivery (no permanent application-side contact-submission database), Upstash Redis for persistent likes, Vercel Web Analytics, and GitHub REST API for repository metadata and Stargazer counts.
- Use ESLint, Prettier, GitHub Actions, Vitest, React Testing Library, and Playwright as specified by the approved TSS.

## UI and routing

- Treat UIR-CWK-001 and the five original UI reference assets as the visual authority.
- Do not invent page content, component states, responsive breakpoints, design tokens, asset mappings, interactions, or navigation labels.
- Next.js route groups do not add URL segments. Never assume a route group name is part of a public URL.
- Do not create potentially colliding routes. Verify the canonical route map against the approved SDD and requirements before adding page route files.
- Keep Personal Portfolio, Professional Worksite, entry/profile selection, and shared page responsibilities distinct as defined by the approved design.

## Content and data

- Keep content schemas and relationships consistent with the approved design.
- Do not fabricate portfolio claims, employment history, project outcomes, dates, credentials, or published articles.
- Validate untrusted content at appropriate boundaries. Treat MDX as executable-capable content and do not enable unsafe arbitrary MDX execution or user-supplied MDX.
- Do not introduce a database for contact submissions; the approved contact flow sends through Resend without permanent application-side storage.
- Likes must use the approved Redis-backed server-authoritative approach. Do not claim one like per human; the approved visitor model is a persistent anonymous visitor identity and its limitations must be respected.

## Security and integrations

- Never hardcode secrets or commit populated environment files.
- Keep service credentials server-side. Do not expose secrets through public-prefixed environment variables or client bundles.
- Do not invent cookie identity/lifetime/signing, CSRF policy, rate limits, Redis retention/recovery, cache durations, GitHub API fallback behavior, analytics events, or deployment settings. These remain pending until explicitly specified.
- Validate external input, handle integration failures safely, and avoid leaking secrets or sensitive diagnostic details.
- Do not add optional AI or feedback features unless separately approved.

## Engineering quality

- Use strict TypeScript and clear, maintainable module boundaries.
- Prefer accessible semantic HTML and keyboard-operable interactions.
- Add tests that trace to approved requirements and verified behavior. Do not encode speculative behavior in tests.
- Follow the approved formatting, linting, type-checking, testing, and build commands once the dependency manifest and CI configuration are approved and present.
- Keep changes scoped. Explain assumptions, unresolved decisions, and verification evidence in the change summary.

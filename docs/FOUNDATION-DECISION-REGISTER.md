# Foundation Decision Register

**Project:** CodeWithKira E-Portfolio System  
**Register:** FDR-CWK-001  
**Updated:** 2026-11-22  
**Branch:** `chore/repository-foundation`

> This register distinguishes approved decisions, SDD proposals, and unresolved implementation decisions. A proposed route is not a finalized route where the SRS/SDD requires reconciliation.

## 1. Route reconciliation

The SDD Section 5.2 proposes the following Next.js App Router paths:

| Proposed path | Purpose | Disposition |
|---|---|---|
| `/` | Introduction | Route identity established |
| `/personal` | Personal Homepage | Proposed; reconcile navigation |
| `/personal/about` | About | Proposed; reconcile navigation |
| `/personal/projects` | Personal Projects | Proposed; reconcile navigation |
| `/personal/projects/[slug]` | Project Details | Proposed; slug rules pending |
| `/personal/blog` | Blog | Proposed; reconcile navigation |
| `/personal/blog/[slug]` | Blog Article | Proposed; slug rules pending |
| `/professional` | Professional Homepage | Proposed; reconcile navigation |
| `/professional/resume` | Resume | Proposed; reconcile navigation |
| `/professional/experience` | Experience | Proposed; reconcile navigation |
| `/professional/work` | Professional Work | Proposed; reconcile navigation |
| `/professional/work/[slug]` | Case Study | Proposed; slug rules pending |
| `/professional/services` | Services | Proposed; reconcile navigation |
| `/professional/articles` | Articles and Research | Proposed; reconcile navigation |
| `/professional/articles/[slug]` | Article Details | Proposed; slug rules pending |
| `/contact` | Shared Contact | **Owner decision recorded for review (PD-014-A):** one shared canonical page with Personal/Professional visual context; full PD-014 route approval remains pending |
| `/license` | License | Proposed |
| `/terms` | Terms | Proposed |
| `/privacy` | Privacy | Proposed |
| `/changelog` | Changelog | Proposed |
| `/api/contact` | Contact Processing | Path proposed; contract incomplete |
| `/api/likes` | Like Processing | Path proposed; contract incomplete |
| `/api/github` | GitHub Information Retrieval | Path proposed; contract incomplete |

The SRS identifies final routes/URL structure as pending (PD-014), and the SDD requires reconciliation with approved UI navigation and the SRS. The owner has explicitly decided under PD-014-A that Personal and Professional contact entry points use one shared canonical `/contact` page with Personal/Professional visual context; this decision is recorded for review and does not close PD-014 as a whole. UIR additionally identifies Personal Work With Me, Common Questions, Activity/footer elements, Professional More About Me, and Resource/Activity elements. The SDD table does not assign standalone routes to all these identities. Some may be sections/components; the source does not settle that question.

Dynamic projects and articles use unique slugs according to the SDD. Exact slug validation, collision rules, case handling, redirects, aliases, trailing-slash behavior, and canonical URL policy are not specified.

**Disposition: full route implementation remains blocked.** The shared `/contact` destination decision is recorded for review; all remaining route decisions and the formal PD-014 closure are still outstanding. The table is a source-grounded proposal, not a final approved URL map.

## 1A. Owner decision record — PD-014-A

| Field | Recorded decision |
|---|---|
| Decision ID | PD-014-A |
| Question | Personal and Professional contact destinations |
| Owner decision | Option A — one shared canonical `/contact` page with Personal/Professional visual context |
| Scope | Shared destination and reusable contact experience; preserve the relevant portfolio context in the presentation/content |
| Status | Recorded as an explicit owner decision for review; not yet a formal amendment or closure of SRS PD-014 |
| Remaining work | Verify the exact entry-point behavior and visual context against the original UI references; define any required context handoff without inventing API fields |

All other unresolved route, API, and configuration decisions remain unchanged.

## 1B. Owner decision record — FB-001

| Field | Recorded decision |
|---|---|
| Decision ID | FB-001 |
| Related requirements | SRS MOD-010 Feedback; SDD TD-011 |
| Owner decision | Include a separate Feedback workflow in Version 1.0; do not merge it into Contact; adopt three submission categories |
| Approved categories | **Bug Report** — report a problem and provide reproduction steps; **General Feedback** — suggestions, comments, and improvement ideas; **Security Concern** — a safe initial description, with guidance not to submit credentials or sensitive exploit details through the public form |
| Additional Bug Report decision | Include a **Steps to Reproduce** field; it is **optional**. Users may submit a Bug Report without it when all required fields are completed. Required status and constraints of other fields remain to be defined. |
| Required Bug Report field | **Bug Title** is required and must summarize the issue. A Bug Report must include it, while **Steps to Reproduce** remains optional. |
| Scope | Version 1.0 includes Feedback as a distinct user-facing workflow with the three categories above |
| Status | Scope and category decision recorded for review; processing design and API contract remain pending |
| Remaining work | Confirm detailed UI fields and behavior; define processing destination/endpoint, validation, request/response/error contract, anti-abuse controls, failure behavior, and retention; reconcile with original UI references |

This decision does not establish a URL, API endpoint, storage provider, retention period, or delivery mechanism. SDD TD-011 remains open until those details are resolved through controlled review.

## 2. Module architecture

The SDD specifies a **modular monolith**: one integrated Next.js application; microservices are not required for Version 1.0.

### SDD modules
1. Introduction Module — landing and navigation to Personal and Professional.
2. Personal Portfolio Module — personal information, projects, blog articles, and related functionality.
3. Professional Worksite Module — professional information, resume, experience, projects, services, case studies, articles, and research.
4. Shared Components Module — reusable components and shared functionality.
5. Content Management Module — reads and processes JSON and MDX.
6. Integration and Service Module — external service communication.
7. Analytics and Engagement Module — analytics, click tracking, likes, and GitHub Stargazer information.

### SDD layers
- Presentation — approved UI and reusable interface components.
- Application — routing, navigation, search/filtering, forms, validation, content processing, likes, and error handling.
- Content — JSON/MDX portfolio data and application configuration.
- Integration — GitHub, Resend, Vercel Analytics, and Upstash Redis.
- Infrastructure — Next.js runtime, Vercel hosting, GitHub repository, environment configuration, build pipeline, deployment, and monitoring.

The proposed directory layout separates `src/app`, `components`, `modules`, `content`, `lib`, `services`, `types`, and `config`, plus tests. This is an implementation blueprint, not a requirement to create empty folders prematurely.

## 3. API contract register

| Endpoint | Method | SDD responsibility | Contract status |
|---|---|---|---|
| `/api/contact` | POST | Validate and process contact messages; send through Resend | Partial |
| `/api/likes` | GET | Retrieve like count and visitor like status | Partial |
| `/api/likes` | POST | Submit a like with duplicate prevention | Partial |
| `/api/github` | GET | Retrieve GitHub repository information | Partial |

### Source-supported behavior

**Contact:** SDD identifies Name, Email address, Subject, and Message; exact fields must follow approved UI and SRS. SRS also identifies inquiry selection where applicable. Server-side validation, spam protection, rate limiting, safe email processing, and Resend integration are required. Do not show success before Resend accepts the request; provider acceptance does not prove inbox delivery. No permanent application-side contact-submission database.

**Likes:** Upstash Redis is authoritative. Use Redis Set operations `SADD`, `SCARD`, and `SISMEMBER`. Uniqueness is per content identifier and protected anonymous visitor identifier hash. Duplicate/concurrent submissions must not create duplicate members. Failures must not fabricate or falsely increment counts.

**GitHub:** GitHub REST API is authoritative for repository metadata and Stargazer counts. Requests are server-side; responses are validated and cached. Handle primary/secondary rate limits, unavailable repositories, and fallback behavior. SDD's initial 5–15 minute cache interval is a recommendation, not a fixed approved duration.

### Contract gaps

The available SDD does not define complete request/response JSON schemas, exact query/body field names, status-code mapping, error envelope, content ID format, rate-limit thresholds/windows, origin allowlist, or idempotency-key contract. These require an API Specification and UI interaction reconciliation.

**Disposition: feature API implementation remains blocked.** Endpoint paths and responsibilities are known; machine-ready contracts are not.

## 4. Environment and configuration

### SDD-listed variable names

| Variable | Purpose | Status |
|---|---|---|
| `RESEND_API_KEY` | Resend credential | Name specified; value/provider setup pending |
| `CONTACT_EMAIL` | Contact recipient | Name specified; actual address pending |
| `UPSTASH_REDIS_REST_URL` | Upstash REST endpoint | Name specified; instance pending |
| `UPSTASH_REDIS_REST_TOKEN` | Upstash credential | Name specified; value pending |
| `VISITOR_COOKIE_SECRET` | Visitor identity protection | Name specified; rotation/lifetime policy pending |
| `VISITOR_HASH_SECRET` | Protected visitor hash derivation | Name specified; rotation policy pending |
| `GITHUB_TOKEN` | Optional GitHub API authentication | Conditional; only if selected operations require it |

No actual credentials or addresses are included. Never commit secret values or expose server-only variables to browser code.

TSS specifies Local Development, Preview, and Production. Preview must not send real contact messages or mutate production likes. Use separate service resources/configuration where appropriate.

### Remaining configuration decisions
- Resend sender identity/domain, recipient, credentials, retries, idempotency, and rate limits.
- Upstash instance, environment isolation, final key naming, retention, backup, and recovery.
- Visitor cookie lifetime, regeneration, signing/rotation, and SameSite policy. HttpOnly and Secure-in-production are SDD security guidance; exact expiration is pending.
- GitHub token necessity, permissions, cache duration, rate-limit handling, and fallback.
- Vercel Analytics plan eligibility for custom events; event taxonomy and privacy/consent policy.
- Production domain, Vercel project settings, monitoring, logging, and operational ownership.
- Security headers/CSP and request-origin/CSRF controls after feature behavior is known.

## 5. Package and CI

Approved by TSS Revision 1: Node.js 24 LTS, npm, GitHub Actions, ESLint, Prettier, React built-in state management, Vitest, React Testing Library, and Playwright.

TSS also calls for a committed npm lockfile and `npm ci` in automated installs. Still to establish: exact compatible dependency versions, package scripts, TypeScript compiler options, ESLint/Prettier configuration, Tailwind/PostCSS configuration, Playwright browser setup, CI triggers/permissions, immutable action references, and exact quality gates.

CI scope: dependency installation, lint, type checking, unit/component tests, production build, and selected critical E2E tests where appropriate. Vercel remains responsible for application hosting/deployment; GitHub Actions should not duplicate deployment without an approved reason.

## 6. Implementation disposition

| Work item | Disposition |
|---|---|
| Preserve foundation branch | Proceed |
| Record source-grounded module and route proposal | Completed in this register |
| Add `.env.example` using SDD-listed names only | Proceed |
| Create full portfolio route tree | Blocked on PD-014/UI navigation reconciliation |
| Implement contact/likes/GitHub handlers | Blocked on complete API contracts and feature security decisions |
| Add package manifest and lockfile | Proceed with compatible exact versions and generated lockfile |
| Add runnable CI | Requires manifest, committed lockfile, and deterministic scripts |
| Separate Feedback workflow for Version 1.0 | Scope confirmed by owner (FB-001); processing implementation blocked on SDD TD-011 and complete contracts |
| Production deployment configuration | Defer to deployment planning |

## 7. Source references

- SDD-CWK-001 v1.0: Sections 2, 5, 6, 9–10, 12–13, 17–18.
- SRS-CWK-001 v1.0: PD-014 and the contact-form, navigation, page, and activity requirements.
- TSS-CWK-001 v1.0 Revision 1: Sections 10–18.
- UIR-CWK-001 v1.0: Personal, Professional, and Shared page inventory.
- RFP-CWK-001 v1.0: controlled foundation scope and implementation sequence.
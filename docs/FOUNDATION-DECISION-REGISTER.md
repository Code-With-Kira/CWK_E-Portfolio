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
| Additional optional Bug Report field | Include **Expected Result**, describing what the user thought should happen; this field is optional. |
| Additional optional Bug Report field | Include **Actual Result**, describing what happened instead; this field is optional. |
| Additional optional Bug Report field | Include **Environment** as an optional field for relevant context such as browser, operating system, and device. |
| Additional optional Bug Report field | Include **Screenshot or Attachment** so reporters may provide visual evidence; this field is optional and may be omitted. |
| Attachment file types | Accept images and documents: PNG, JPG/JPEG, WebP, and PDF. |
| Attachment count | Allow **one file per Bug Report**. |
| Maximum attachment size | **5 MB per file**. |
| Attachment submission method | Upload the optional attachment directly with the Bug Report as part of the same submission flow; no separate post-submission upload step. Transport, processing, storage, and retention details remain open. |
| Attachment retention and failure alert | Store the attachment temporarily and delete it **24 hours after upload**. If deletion fails, automatically retry until deletion succeeds; keep the attachment unavailable to users during retry/recovery. If still undeleted **24 hours after its scheduled deletion time (48 hours after upload)**, send an internal administrative alert **once only, when that threshold is first reached; do not repeat it periodically**. The owner has approved **email via Resend**, reusing the project's selected email provider, as the administrative alert channel, with **laurenceegay1@gmail.com** as the recipient. The owner has approved a **dedicated administrative-alert sender identity**, separate from the contact-form sender identity. The exact sender email address and verified sending domain must be confirmed; do not assume `system-alerts@your-domain` is an actual approved address. The owner has confirmed that the system will be deployed on **Vercel** (consistent with the approved TSS hosting baseline). The production custom domain and dedicated sender email address/domain cannot be confirmed yet and remain **deferred/open**; no domain or sender address is to be inferred. Vercel deployment does not itself establish a custom domain or a verified Resend sender domain. Resend-specific sender configuration, delivery-failure handling, retry schedule, maximum retry duration, and final cleanup escalation remain to be specified. |
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

### Owner clarification — storage and email-provider readiness

The owner has **not selected an attachment storage provider** for Bug Report uploads. The previously raised Vercel Blob option remains a proposal only; the decision is **pending** and will be revisited after implementation has started. Do not provision or implement Vercel Blob (or another attachment-storage service) on the basis of this discussion. The owner has confirmed **Resend as the intended email provider** for the project's email workflows, but does not yet have a Resend account. Resend account creation, sender-domain verification, credential provisioning, and provider configuration therefore remain pending prerequisites; do not invent credentials or represent email delivery as configured or tested.

### Owner decision — anonymous visitor cookie lifetime

The owner has selected a **one-day (24-hour) lifetime** for the anonymous visitor identity cookie used by the likes feature. This is the cookie lifetime only; it does **not** authorize automatic expiration or deletion of persistent like records in Upstash Redis. After the identity cookie expires, a later visit may receive a new anonymous identity and therefore may submit another like for the same content item. This permits repeat likes over time from the same browser/device and does not represent one like per human. The exact cookie renewal behavior, signing/rotation, SameSite policy, and other cookie security settings remain open; do not infer a sliding-renewal policy from the one-day lifetime decision.

### Owner decision — anonymous visitor cookie renewal

The owner has selected **Option A — Fixed expiration** for the anonymous visitor identity cookie. The cookie expires **24 hours after it is first issued**; visits and interactions do not reset or extend that expiration. This is a fixed 24-hour lifetime, not a sliding expiration. The previously recorded one-day lifetime remains in effect. Cookie signing/rotation, SameSite and other security settings remain open.

### Owner decision — anonymous visitor cookie security baseline

The owner has approved all three recommended security attributes for the anonymous visitor identity cookie: **HttpOnly**, **Secure**, and **SameSite=Lax**. The cookie must be inaccessible to client-side JavaScript through the HttpOnly attribute; Secure must be enabled for production HTTPS so the cookie is sent only over secure connections; and SameSite=Lax is the selected cross-site request mitigation baseline. These settings supplement, and do not change, the previously approved **fixed 24-hour expiration**. This approval does not resolve cookie signing algorithm, secret rotation, cookie name/path/domain, development-versus-production Secure behavior, CSRF/origin validation requirements, or visitor identity/hash migration policy; those details remain open for specification and verification.

### Owner decision — anonymous visitor cookie signing

The owner has approved **HMAC-SHA-256** as the signing algorithm for the anonymous visitor identity cookie. The signing key must be a securely generated server-side secret stored in the deployment environment (including Vercel environment configuration for the applicable environment); it must never be committed to the repository, exposed to browser code, or included in public API responses. The existing SDD-listed `VISITOR_COOKIE_SECRET` is the intended environment-variable name, subject to implementation verification. Secret generation, minimum entropy/length, key rotation and invalidation behavior, and any migration strategy remain to be specified before implementation. This decision does not change the previously approved fixed 24-hour cookie lifetime or the HttpOnly, Secure-in-production, and SameSite=Lax baseline.

### Owner decision — visitor cookie signing-secret rotation

The owner has approved **manual secret rotation** as the initial operating approach for the anonymous visitor cookie signing secret. When rotation is required, an authorized operator will generate a new secret, update the applicable server-side Vercel environment configuration, and deploy the change. Under the initial single-active-secret approach, cookies signed with the previous secret will no longer validate and affected visitors will receive a new anonymous identity when a valid replacement cookie is issued; this can allow those visitors to like the same content again under the new identity. Do not imply seamless or dual-key rotation. Rotation cadence, operator access procedure, emergency compromise response, and whether a future dual-key migration is needed remain open for operational specification. The secret must remain server-side and must not be committed to source control.

### Owner decision — anonymous visitor hash generation

The owner has approved **HMAC-SHA-256** for deriving the protected anonymous visitor identifier used by the likes feature, using a dedicated server-side secret named `VISITOR_HASH_SECRET`. This secret must be distinct from `VISITOR_COOKIE_SECRET`, generated securely, stored only in server-side environment configuration (including the applicable Vercel environment), and never committed to source control or exposed to browser code or public API responses. The derived identifier/hash, rather than the raw visitor identity, is used as the visitor component of the Upstash Redis like-set membership key. The exact canonical input format, encoding, domain separation/versioning, secret rotation and migration behavior, and Redis key structure remain to be specified and verified before implementation. This decision does not change the approved HMAC-SHA-256 cookie-signing approach or the approved manual rotation policy for the cookie-signing secret; rotation policy for the visitor-hash secret is not yet decided.

### Owner decision — visitor-hash secret rotation

The owner has approved **manual rotation** as the initial operating policy for `VISITOR_HASH_SECRET`. Rotation is an operator-managed change: generate a new secret securely, update the server-side deployment environment (Vercel), and deploy the change. The secret must remain separate from `VISITOR_COOKIE_SECRET` and must never be committed to source control or exposed to client code. **Rotation consequence:** because the derived visitor hashes change when the secret changes, existing Upstash Redis like-set memberships keyed by the previous hashes will not match newly derived hashes. Unless a separately designed and authorized migration is performed, affected visitors may be able to like the same content again after rotation. No automatic dual-secret validation, seamless migration, or Redis membership rewrite is approved by this decision. Rotation cadence, operator access controls, compromise response, and any future migration procedure remain to be specified.

### Owner decision — secret generation standard

The owner has approved a minimum secret-generation standard for both `VISITOR_COOKIE_SECRET` and `VISITOR_HASH_SECRET`: each secret must be generated independently using a cryptographically secure random number generator and contain at least **32 random bytes (256 bits) of entropy**. The generated bytes may be encoded as hexadecimal or Base64 for environment-variable storage. The two secrets must not be derived from one another, reused, or generated from predictable values. Store them only in server-side deployment environment configuration (including Vercel), never in source control, browser code, logs, or public API responses. This decision establishes the minimum generation strength and permitted encodings; it does not specify an exact generation command/tool, environment-specific secret provisioning workflow, rotation cadence, or operator access policy.

### Owner decision — fail-closed handling of invalid or missing secrets

The owner has approved **fail-closed** handling for `VISITOR_COOKIE_SECRET` and `VISITOR_HASH_SECRET`. If either required secret is missing, empty, malformed, or does not meet the approved minimum of 32 random bytes (256 bits), the application must not silently generate a replacement at runtime, use a hardcoded or otherwise predictable fallback, or continue the affected security-dependent operation with an invalid secret. The affected functionality must remain unavailable until valid configuration is supplied. Configuration validation should detect the problem at startup where practical; if detected during a request, the server must fail safely and return a generic error without disclosing secret values or other sensitive configuration details. This decision does not prescribe a particular startup-validation library or exact HTTP status/error response mapping; those remain part of the API/configuration contract to be specified.

### Owner decision — invalid, tampered, or expired visitor cookies

The owner has approved the following handling for an invalid, tampered, expired, or incorrectly signed anonymous visitor cookie: the server must reject the cookie and must not trust or use its contents; generate a new cryptographically secure random visitor identifier; sign the new identifier using `VISITOR_COOKIE_SECRET`; and issue a replacement cookie with the previously approved 24-hour fixed lifetime and security attributes (`HttpOnly`, `Secure` in production HTTPS, and `SameSite=Lax`). The replacement identity is treated as a new anonymous visitor identity. Consequently, the visitor may be able to like content again under that new identity. This behavior does not authorize extending or resetting the lifetime of a valid cookie on visits or interactions. Exact identifier byte length/encoding, cookie name and path/domain scope, parsing/serialization details, and HTTP response behavior remain to be specified in the implementation/API contract.

### Owner decision — anonymous visitor identifier format

The owner has approved generating the raw anonymous visitor identifier as **32 cryptographically random bytes (256 bits)** and encoding those bytes as **Base64URL without padding** before cookie signing. The encoded identifier is the cookie payload value; its HMAC-SHA-256 signature is a separate value and must be verified before the identifier is trusted. The identifier must be generated using a cryptographically secure random number generator. This format decision does not change the separate `VISITOR_HASH_SECRET` derivation process, the 24-hour fixed cookie lifetime, or the approved cookie security attributes. Exact signed-cookie serialization/delimiter format and signature encoding remain to be specified in the implementation contract.

### Owner decision — HMAC signature encoding

The owner has approved encoding the HMAC-SHA-256 signature for the anonymous visitor cookie as **Base64URL without padding**, matching the approved visitor identifier encoding. The signed cookie therefore contains two separately encoded components: the Base64URL-without-padding visitor identifier and its Base64URL-without-padding HMAC-SHA-256 signature. The server must verify the signature before trusting the identifier. This decision specifies the signature encoding only; the exact serialization/delimiter format, cookie name, and cookie path/domain scope remain to be specified in the implementation contract.

### Owner decision — signed-cookie serialization format

The owner has approved the signed anonymous visitor cookie serialization format **`<visitor-id>.<signature>`**, using a single period (`.`) as the delimiter between the separately encoded Base64URL-without-padding visitor identifier and Base64URL-without-padding HMAC-SHA-256 signature. Because Base64URL does not use the period character, the two components can be parsed unambiguously. The server must verify the signature before trusting the visitor identifier. This decision specifies serialization only; the cookie name and cookie path/domain scope remain to be specified.

### Owner decision — anonymous visitor cookie name

The owner has approved **`cwk_visitor`** as the cookie name for the signed anonymous visitor identifier. The approved name is used without the `__Host-` prefix. This decision establishes the cookie name only; cookie path and domain scope, and any related browser-enforced prefix policy, remain to be specified separately.

### Owner decision — anonymous visitor cookie path

The owner has approved **`/`** as the `cwk_visitor` cookie path. This makes the cookie available across the website's paths, including portfolio pages and API routes where the browser's cookie rules permit it. This decision specifies the cookie path only; cookie domain scope remains to be specified separately.

### Owner decision — anonymous visitor cookie domain scope

The owner has approved **omitting the `Domain` attribute** from the `cwk_visitor` cookie. The cookie is therefore host-only and is sent only to the exact hostname that issued it, rather than being shared automatically with sibling subdomains. This decision specifies domain scope only; the production hostname and any future need for cross-subdomain identity remain separate decisions.

### Owner decision — anonymous visitor cookie expiration attributes

The owner has approved setting both **`Max-Age=86400`** and **`Expires`** on the `cwk_visitor` cookie. `Max-Age` is 86,400 seconds (24 hours), and `Expires` must represent the corresponding UTC expiration timestamp calculated from the cookie's original issuance time. Neither attribute may be refreshed or extended by ordinary visits or interactions; the approved lifetime remains fixed at 24 hours from first issuance. This decision specifies browser cookie expiration attributes and does not change server-side signature validation or the approved fixed-lifetime policy.

### Owner decision — visitor-cookie association for the introduction proceed event

The owner has approved expanding the intended use of the signed anonymous visitor cookie **`cwk_visitor`** to include association with the specific introduction-screen engagement event **`proceed_to_dual_profile`**, representing a visitor clicking the introduction screen's Proceed control to continue to the Dual Profile selection experience. This is a narrowly scoped addition to the previously documented Portfolio Likes use; it does not authorize general page-view tracking, browsing-history collection, or tracking of other interactions. The event's storage location, event schema and metadata, retention period, reporting/analytics implementation, privacy disclosure or consent requirements, and the precise cookie-issuance trigger when no valid cookie exists remain unresolved and must be specified before implementation. This owner decision records the approved purpose only; it does not close those design or compliance questions.

### Owner decision — lazy issuance of the anonymous visitor cookie

The owner has approved **lazy issuance** of the `cwk_visitor` cookie. The system must not issue this cookie merely because someone opens the website or browses ordinary pages. It may issue a new cookie only when a visitor first performs one of the currently approved identity-requiring actions: (1) clicks the introduction screen's Proceed control, which triggers the approved `proceed_to_dual_profile` event; or (2) performs a Portfolio Like interaction. If a valid cookie already exists, the system uses it for these approved purposes subject to its previously approved fixed 24-hour lifetime and validation rules. This decision does not authorize cookie issuance for unrelated page views or interactions. The exact request/response behavior, event persistence, and how the Likes interface handles visitor-specific `hasLiked` state before a cookie exists remain to be specified in the relevant API and implementation contracts.



### Owner decision — Durable retry queue cleanup failure policy

The owner has approved the following cleanup-failure policy for durable retry queue records: when automatic deletion fails after a queue record has completed or reached the exhausted/failed terminal state and its 7-day retention period has elapsed, retry deletion **once every hour**. If the record remains undeleted **24 hours after its scheduled deletion time**, send **one administrative email alert** (not recurring alerts) to `laurenceegay1@gmail.com` using **Resend**, the project-selected email provider. This uses the previously approved administrative alert recipient and provider. The alert must identify the cleanup failure without exposing secrets or sensitive event payloads. This policy does not extend the record's approved retention period intentionally; it defines recovery attempts after the scheduled deletion time. The exact retry scheduler, alert sender identity/address/domain, alert delivery-failure handling, and final escalation/cleanup behavior remain to be specified before implementation.

### Owner decision — Durable retry queue record retention

The owner has approved a **7-day retention period** for durable retry queue records after they reach a terminal state, whether successfully processed or exhausted/failed. Queue records must be automatically deleted after that retention period. This retention decision applies to retry-queue records only; it does not change the separately approved 90-day retention for individual `proceed_to_dual_profile` event records or the indefinite lifetime of the cumulative Proceed count. The exact timestamp basis, cleanup mechanism/schedule, handling of cleanup failures, and verification/monitoring of deletion remain to be specified before implementation.

### Owner decision — Durable retry queue storage provider

The owner has approved **Upstash Redis** as the storage provider for the durable retry queue used by `proceed_to_dual_profile` event processing. Queue data must use logically separate Redis keys and data structures from Portfolio Like sets and the Proceed event records/cumulative count. This decision selects the provider only; the queue key design, queue record schema and states, atomic enqueue/dequeue and idempotency strategy, scheduling/recovery implementation, persistence/eviction/backup characteristics, retention and cleanup, concurrency controls, and operational failure handling remain to be specified and verified before implementation. The implementation must not assume that provider selection alone establishes the required durability guarantees.

### Owner decision — Durable retry queue

The owner has approved **durable retry-queue behavior** for `proceed_to_dual_profile` event writes. Pending events must survive application process restarts and deployments rather than being silently lost. The retry mechanism must resume eligible pending work after recovery, preserving the approved bounded retry policy (initial attempt immediately, then retries after 5 seconds, 15 seconds, and 30 seconds; four total attempts maximum) where practical. Queue processing must preserve event idempotency and prevent duplicate event records or duplicate cumulative-count increments, including when a write may have succeeded before an ambiguous failure or interruption. Once the approved attempt limit is exhausted, the event is marked as exhausted/failed and is not retried indefinitely. This owner decision approves durability and recovery behavior only; the queue technology and storage location, event state/schema, atomic enqueue/write design, exact retry timing across downtime, concurrency/locking, cleanup/retention of queue records, observability, and operational failure handling remain to be specified before implementation.

### Owner decision — Proceed event retry schedule

The owner has approved the following bounded retry schedule for a failed `proceed_to_dual_profile` event write: make the initial write attempt immediately; if it fails, retry after **5 seconds**, then after **15 seconds**, then after **30 seconds**. This means a maximum of **four total write attempts** (one initial attempt plus three retries). After the final retry fails, stop automatic retries and safely log the unresolved failure. The retry mechanism must preserve the previously approved non-blocking visitor experience and must prevent duplicate event records or duplicate cumulative-count increments if an earlier attempt may have succeeded despite an ambiguous response. This approval defines the retry timing and attempt limit only; durable queueing, process restarts, idempotency implementation, replay/recovery, and alerting remain to be specified before implementation.

### Owner decision — Proceed event retry approach

The owner has approved a **non-blocking, limited automatic retry approach** for failed `proceed_to_dual_profile` event writes to Upstash Redis. The visitor must be allowed to continue to the Dual Profile selection experience without waiting for retries. Retry processing must be designed to prevent duplicate event records and duplicate cumulative-count increments when an earlier write may have succeeded despite an ambiguous response; the approved unique-visitor deduplication rule remains in force. Retries must be bounded rather than continuing indefinitely, and failures that remain unresolved must be logged safely. This approval establishes the retry approach only; the retry schedule, maximum attempts or elapsed retry period, whether/how work is queued, persistence and durability of retry jobs, idempotency key and atomic Redis operation design, replay/recovery behavior, and alerting remain unresolved and must be specified before implementation.

### Owner decision — Proceed event recording failure behavior

The owner has approved the following failure-handling behavior for the `proceed_to_dual_profile` event when Upstash Redis is temporarily unavailable or the event cannot be persisted: (1) the visitor must still be allowed to continue to the Dual Profile selection experience; (2) the system must not indicate or represent that the event was successfully recorded; (3) the failure must be logged server-side using safe diagnostic information and without exposing secrets or sensitive internals to the visitor; and (4) the cumulative Proceed count must increase only when the event has been successfully recorded according to the approved deduplication rule. This approval does not define retries, queuing, replay, alerting, log retention, or recovery/reconciliation behavior; those remain open for specification before implementation.

### Owner decision — cumulative Proceed count deduplication

The owner has approved counting **unique anonymous visitor-cookie identities**, rather than every click, toward the cumulative `proceed_to_dual_profile` count. A visitor clicking Proceed repeatedly while presenting the same valid `cwk_visitor` identity must contribute at most one increment to the cumulative count. Because the approved cookie has a fixed 24-hour lifetime and is not renewed by activity, a visitor whose cookie expires and who later receives a new anonymous identity may be counted again; this is a count of distinct anonymous cookie identities, not a guaranteed count of distinct human beings or lifetime unique people. The exact atomic deduplication mechanism and any supporting Redis data structure/retention requirements remain to be specified before implementation.

### Owner decision — engagement-event retention and cumulative count

The owner has approved a **90-day retention period** for individual `proceed_to_dual_profile` event records in Upstash Redis, with automatic deletion when each record reaches the end of its retention period. The system must maintain a separate cumulative Proceed count that is not deleted or reset when individual event records expire; the aggregate is retained indefinitely unless a future owner decision changes this policy. Expiration of these engagement-event records must not reset, decrement, or otherwise alter Portfolio Like counts or Like membership records, which remain governed by their separate storage and retention policy. This approval establishes the retention period and aggregate-count behavior only; exact Redis key/data structures, expiry enforcement, reporting, privacy controls, and failure/recovery behavior remain to be specified before implementation.

### Owner decision — engagement-event storage provider

The owner has approved **Upstash Redis** as the storage provider for the approved introduction engagement event **`proceed_to_dual_profile`**. Engagement-event records must be kept logically separate from the existing Portfolio Likes Redis sets; the event implementation must not reuse or alter the Like set data model. This approval selects the provider only. The Redis key design, event schema and metadata, write/read access patterns, retention and expiry policy, privacy controls, reporting/query approach, operational limits, and failure behavior remain unresolved and must be specified before implementation. This decision does not authorize storing general page views or other unapproved visitor activity.

### Owner decision — administrative alert delivery failure policy

The owner has approved the following bounded failure policy for administrative email alerts associated with durable retry-queue cleanup failures: if an alert cannot be delivered through **Resend**, retry alert delivery **once every hour for up to 24 hours**. If delivery remains unsuccessful after that 24-hour retry window, stop automatic delivery retries and write a **critical diagnostic entry** for manual intervention. Do not retry indefinitely or generate repeated alert attempts beyond the approved window. This policy applies to delivery of the single administrative alert already authorized for a given cleanup failure; it does not authorize duplicate alerts for the same failure. The previously approved recipient remains `laurenceegay1@gmail.com`, and the sender identity/address/domain, precise retry-window boundary and attempt-count interpretation, delivery-status detection, critical-log destination/retention, and manual escalation ownership remain to be specified before implementation.

### Owner decision — critical diagnostic log destination

The owner has approved **Vercel Runtime Logs** as the destination for critical diagnostic entries created when administrative alert delivery remains unsuccessful after the approved 24-hour retry window. Entries must use structured server-side logging and must exclude secrets, credentials, raw visitor identifiers, and sensitive event payloads. This decision selects the logging destination only; Vercel plan eligibility and log access, retention and availability, access permissions, monitoring/notification coverage, exact structured fields and severity conventions, and manual escalation ownership remain to be verified or specified before implementation. Do not treat a log entry alone as proof that an operator has been notified or has acted.

### Owner decision — critical diagnostic log retention

The owner has approved a **30-day retention period** for critical diagnostic entries written to **Vercel Runtime Logs** under the approved administrative-alert failure policy. This retention period is conditional on the selected Vercel plan and applicable logging configuration supporting it; that capability must be verified before implementation. If 30-day retention is not supported, do not silently shorten the period or assume an alternative provider: return to the owner with the verified limitation and a proposed alternative for approval. This decision does not authorize logging secrets, credentials, raw visitor identifiers, or sensitive event payloads. Log access permissions, monitoring/notification coverage, exact structured fields and severity conventions, and manual escalation ownership remain to be specified.

### Owner decision — critical diagnostic log access control

The owner has approved **least-privilege access** to critical diagnostic logs in Vercel Runtime Logs. Access is limited to the project owner and explicitly authorized maintainers who require it for their responsibilities. Users must authenticate through their own individual Vercel accounts; shared credentials or shared accounts must not be used. Access should be granted only at the minimum role/scope needed and revoked when authorization is no longer required. This decision establishes the access-control principle only; the exact Vercel team membership, role assignments, review cadence, audit-log availability, and process for emergency access remain to be specified and verified before implementation.

### Owner decision — critical diagnostic log access review cadence

The owner has approved a **90-day access review cadence** for permissions to view critical diagnostic logs in Vercel Runtime Logs. Reviews must also occur promptly whenever a maintainer leaves the project or changes responsibilities; access no longer required must be revoked promptly rather than waiting for the next scheduled review. This cadence supplements the approved least-privilege policy and individual-account requirement. The review owner, evidence/recordkeeping method, and exact Vercel role assignments remain to be specified before implementation.

### Owner decision — critical diagnostic log access review ownership

The owner has approved the **project owner as the accountable owner** for scheduled and event-driven access reviews covering critical diagnostic logs in Vercel Runtime Logs. The project owner may delegate the execution of a review to an explicitly authorized maintainer, but remains accountable for ensuring the review is completed, access is appropriate, and unnecessary permissions are revoked promptly. The review evidence/recordkeeping format and exact Vercel role assignments remain to be specified before implementation.

### Owner decision — critical diagnostic log access review register

The owner has approved a **restricted access-review register** as the evidence record for scheduled and event-driven reviews of access to critical diagnostic logs in Vercel Runtime Logs. Each review record must capture the review date, reviewer, authorized accounts and assigned roles, whether each permission remains necessary, changes made (including access revocations), and outstanding actions with their completion status. The register must be access-restricted to the project owner and explicitly authorized maintainers with a need to perform or verify the review. It must not contain credentials, secrets, or diagnostic-log contents. The register's storage location, exact format, and retention period remain to be specified before implementation.

### Owner decision — access-review register storage location

The owner has approved storing the critical diagnostic log access-review register as **restricted project administrative documentation**, separate from public project documentation and application source code. Access must be limited to the project owner and explicitly authorized maintainers who need it for review or oversight. The register must not be placed in a publicly accessible location. The exact storage location and platform must be verified to provide the required private access controls before the register is created; do not assume that the existing application repository is private. The register's format and retention period remain to be specified.

### Owner decision — access-review record retention

The owner has approved retaining each critical diagnostic log access-review register record for **one year after the date of that review**. At the end of the retention period, the record must be securely deleted unless an unresolved security incident or another legitimate requirement justifies retaining it longer. Any extended retention must be limited to the relevant record, have a documented reason and an accountable owner, and be reviewed for deletion when that reason no longer applies. The secure deletion method, storage platform's deletion capabilities, and process for documenting approved extensions remain to be specified and verified before implementation.

### Owner decision — access-review register format

The owner has approved **Markdown (.md)** as the format for the critical diagnostic log access-review register. The register must use a consistent table for review entries and a separate section for outstanding actions. It remains restricted project administrative documentation, subject to the approved least-privilege access policy and one-year record-retention rule. Markdown format approval does not select a storage platform or location; the platform must still be verified to provide the required private access controls and secure deletion capability before the register is created.

### Access-revocation evidence requirement

The project owner approved requiring evidence of completed access revocations in the restricted access-review register. For each revocation, record the affected account, the date, the reviewer, and confirmation that the permission was removed. Do not include credentials or sensitive screenshots. This requirement supplements the approved access-review register format, storage restrictions, review ownership, and retention policy.

### Project-owner sign-off for access reviews

The project owner approved requiring explicit project-owner sign-off for every access review, including reviews performed by a delegated authorized maintainer. The review record must identify the project owner who approved it and record the sign-off date. Delegation of review execution does not transfer the project owner's accountability.

### Overdue access-review handling

The project owner approved the following policy for overdue scheduled access reviews:
- Notify the project owner when a review becomes overdue.
- Record the overdue status and notification date in the restricted access-review register.
- Keep the review outstanding until it has been completed and received the required project-owner sign-off.
- Do not automatically extend or renew access merely because a review is overdue. Existing access remains subject to the approved least-privilege policy and any independent authorization or expiry requirements.

### Seven-calendar-day overdue review resolution period

The project owner approved a resolution period of seven calendar days after the overdue notification for completing an overdue access review and obtaining the required project-owner sign-off. If the review cannot be completed within that period, the project owner must document the reason, outstanding actions, and a revised completion date in the restricted access-review register. This resolution period does not automatically extend or renew any access.

### Escalation for access reviews exceeding the seven-day resolution period

The project owner approved escalation when an overdue access review is not completed within the approved seven-calendar-day resolution period:
- Notify the project owner again and mark the review as escalated in the restricted access-review register.
- Require a documented corrective action and a new completion date.
- Preserve the existing access-control policy; escalation does not silently grant, renew, or extend access and does not change existing permissions.

### Formal security incident trigger for persistently unresolved access reviews

The project owner approved treating an access review that remains unresolved for a further seven calendar days after escalation as a formal security incident for assessment and tracking. The project owner must document the incident, assess whether the outstanding access presents a security risk, and determine appropriate corrective action. This trigger is a formal incident-classification and assessment step; it does not automatically mean a security breach or compromise has occurred. The incident record must distinguish confirmed facts from suspected or unverified conditions.

### Notification recipients for formal access-review security incidents

The project owner approved the following notification policy when a persistently unresolved access review is classified as a formal security incident:
- Notify the project owner immediately.
- Notify any explicitly authorized security or technical maintainer assigned to incident response.
- Notifications must not include credentials, secrets, raw visitor identifiers, or sensitive diagnostic payloads.

### Email notification channel for formal security incidents

The project owner approved email as the notification channel when a persistently unresolved access review is classified as a formal security incident. Notifications are to be individually addressed to the project owner and assigned, explicitly authorized incident-response maintainers. The project-selected email provider is Resend, using the dedicated administrative sender identity separate from the contact-form sender. The exact sender address and domain remain pending until the Resend account is established and sender-domain verification is completed.

### Incident notification email delivery-failure handling

The project owner approved the following policy if formal security incident notification email delivery fails:
- Retry delivery once every hour for up to 24 hours.
- Avoid duplicate incident notifications when delivery status is ambiguous; use an idempotent notification identity or equivalent delivery-state control where supported.
- If delivery remains unsuccessful after 24 hours, stop automatic retries and create a critical diagnostic log entry for manual intervention.
- Keep the incident open until the project owner confirms that the notification issue has been addressed.
- Do not include credentials, secrets, raw visitor identifiers, or sensitive diagnostic payloads in retry records or diagnostic logs.

### Successful incident notification status and delivery confirmation

The project owner approved the following confirmation policy for formal security incident email notifications:
- Treat a notification as successfully submitted for workflow purposes only when Resend reports an accepted/sent status.
- Distinguish provider acceptance/sent status from actual inbox delivery; do not represent acceptance as proof that the recipient received or read the email.
- Record the Resend provider message ID, reported status, and status timestamp in the restricted incident record or other approved operational record.
- If Resend subsequently reports a bounce or delivery failure, reopen the notification issue for manual handling.
- Keep notification records free of credentials, secrets, raw visitor identifiers, and sensitive diagnostic payloads.

### One-year retention of formal incident notification records

The project owner approved retaining formal incident notification records for one year after the associated incident is closed. Retention may be extended only when an investigation remains unresolved or another legitimate requirement justifies it. Each extension must have its reason and accountable owner documented. Records must be securely deleted when the applicable retention period ends. The exact storage location, deletion mechanism, and any legal or provider-specific retention constraints remain subject to verification before implementation.

### Project-owner-only formal incident closure authority

The project owner approved the rule that only the project owner may formally close a security incident. Assigned incident-response maintainers may investigate, document evidence, carry out corrective actions, and recommend closure, but they may not independently close the incident. The project owner must review the available evidence and corrective-action status and explicitly approve closure. The incident record must document the closure decision, approver, and closure date. Closure criteria, required evidence fields, and the restricted incident-record location remain to be specified and verified before implementation.

### Owner decision — formal security incident closure evidence requirements

The project owner approved the following evidence requirements before a formal security incident may be closed:

1. The incident has been investigated and the findings are documented.
2. Required corrective actions are completed, or any remaining actions have documented justification and assigned ownership.
3. Relevant incident notifications have been addressed.
4. Outstanding risks and follow-up actions are documented.
5. The closure decision and date are recorded, including the project owner's explicit approval.

Only the project owner may formally close an incident. Assigned incident-response maintainers may investigate, document evidence, carry out corrective actions, and recommend closure, but may not independently close it. The project owner must review the evidence and corrective-action status before approving closure.

This decision defines the evidence checklist; it does not by itself specify the incident-record schema, exact closure workflow, or restricted storage location. Those details remain to be specified and verified before implementation.

### Owner decision — formal security incident record storage location

The project owner approved storing formal security incident records as **restricted project administrative documentation**, separate from public project documentation and application source code. Access must be limited to the project owner and explicitly authorized incident-response maintainers who need the records for investigation, response, oversight, or closure.

The selected storage platform and exact location must be verified to support private access controls and the approved one-year retention period after incident closure, including documented, justified extensions and secure deletion when retention ends. Do not assume the existing application repository is private or select a platform without verifying its access and retention capabilities. The platform, exact location, record format/schema, and deletion procedure remain to be specified and verified before implementation.

### Owner decision — formal security incident record format

The project owner approved **Markdown (.md)** as the format for formal security incident records. Records must use a consistent template that captures, at minimum, incident identification, timeline, investigation findings, notifications and their status, corrective actions, outstanding risks and follow-up actions, and the project owner's explicit closure decision, approver, and closure date.

Incident records remain restricted project administrative documentation, separate from public project documentation and application source code, with access limited to the project owner and explicitly authorized incident-response maintainers who need access. Markdown format approval does not select the storage platform or exact location; those must still be verified to support private access controls, the approved one-year retention period after incident closure (including documented justified extensions), and secure deletion. The exact template fields and storage/deletion procedures remain to be specified before implementation.

### Owner decision — formal security incident identifier format

The project owner approved the unique formal security incident identifier format **`CWK-INC-YYYY-NNN`**. The four-digit year represents the calendar year in which the incident is first recorded; the three-digit sequence is assigned to each new incident within that year (for example, `CWK-INC-2026-001`). Each identifier must be unique and remain associated with the incident throughout its lifecycle and in all related restricted records and notifications. The sequence-allocation mechanism, concurrency protection, behavior when more than 999 incidents occur in a year, and any correction/voiding rules remain to be specified before implementation.

### Owner decision — formal security incident severity classification

The project owner approved a four-level severity classification for formal security incidents:

1. **Critical** — confirmed or strongly suspected compromise with immediate, serious impact.
2. **High** — significant security risk requiring urgent investigation and corrective action.
3. **Medium** — limited security concern requiring investigation and tracked remediation.
4. **Low** — minor security concern with limited impact and no immediate threat.

The project owner retains authority to confirm or change an incident's severity. The classification labels and high-level descriptions are approved; detailed objective criteria, impact/likelihood thresholds, response time targets, escalation rules, and severity reassessment triggers remain to be specified before implementation.

### Owner decision — initial incident severity assignment authority

The project owner approved allowing **explicitly authorized incident-response maintainers** to assign an initial **provisional severity** during the incident's initial assessment. The provisional classification must be identified as provisional and recorded with the assigning maintainer and assignment timestamp. The project owner must review and confirm the severity; the project owner retains final authority to confirm or change the classification at any point.

This decision authorizes provisional assignment only. It does not grant every project maintainer incident-response authority or transfer final severity authority. The process and target timeframe for project-owner review, interim handling if the owner is unavailable, and detailed reassessment/escalation triggers remain to be specified before implementation.

### Owner decision — project-owner review targets for provisional incident severity

The project owner approved the following target timeframes for reviewing and confirming provisional incident severity assignments:

- **Critical:** immediately.
- **High:** within 4 hours.
- **Medium:** within 24 hours.
- **Low:** within 3 calendar days.

These are project-owner review targets. They do not authorize delaying urgent containment, investigation, notification, or corrective action while review is pending. The clock-start definition, time-zone convention, after-hours coverage, owner-unavailability procedure, and escalation when a target is missed remain to be specified before implementation.

### Owner decision — start of the provisional severity review clock

The project owner approved that the review clock for a provisional incident severity assignment starts at the timestamp when an explicitly authorized incident-response maintainer first records that provisional severity in the formal incident record. That recorded timestamp is the reference point for calculating the applicable project-owner review target. The timestamp must be recorded consistently and must not be backdated or silently changed; any correction must preserve an auditable explanation and the original value.

The time-zone convention, authoritative timestamp source/format, after-hours coverage, owner-unavailability procedure, and missed-target escalation remain to be specified before implementation.

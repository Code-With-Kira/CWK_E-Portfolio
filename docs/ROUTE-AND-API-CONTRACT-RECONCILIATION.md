# Route and API Contract Reconciliation

| Field | Value |
|---|---|
| Project | CodeWithKira E-Portfolio System |
| Branch | `chore/repository-foundation` |
| Document type | Source-based reconciliation / owner decision aid |
| Status | Draft for owner decisions — not an amendment to approved SRS/SDD |
| Governing baselines | SRS-CWK-001 v1.0; SDD-CWK-001 v1.0; TSS-CWK-001 v1.0 Rev 1; UIR-CWK-001 v1.0; RFP-CWK-001 v1.0 (controlled amendments) |

## 1. Purpose and decision boundary

This document reconciles the route proposal in SDD Section 5.2 with SRS PD-014 and the approved UIR page inventory. It also records the API behavior explicitly described in the SDD and separates that behavior from missing request/response details.

This is a planning artifact only. It does not close SRS PD-014, approve new URLs, define missing API schemas, or authorize route handlers. The original UI PDFs and prototype remain authoritative for page identity, navigation labels, layout, and interaction behavior. UIR-CWK-001 is an inventory, not a substitute for those references.

## 2. Route reconciliation

### 2.1 SDD Section 5.2 proposed routes

Every route below remains a **candidate**, not a canonical approved URL, until PD-014 is resolved against the original navigation and prototype.

| Proposed path | SDD purpose | UIR correspondence | Current disposition |
|---|---|---|---|
| `/` | Introduction | Introduction / landing, profile selection, Personal and Professional previews | Candidate; verify exact entry and selection behavior in prototype |
| `/personal` | Personal Homepage | Personal Home | Candidate; verify label and destination |
| `/personal/about` | About | Personal About | Candidate; verify navigation |
| `/personal/projects` | Personal Projects | Personal Projects | Candidate; verify listing/detail relationship |
| `/personal/projects/[slug]` | Project Details | Personal project detail implied by Projects | Candidate; slug rules and invalid-slug behavior unspecified |
| `/personal/blog` | Blog | Personal Blog | Candidate; verify exact destination and content scope |
| `/personal/blog/[slug]` | Blog Article | Personal article detail implied by Blog | Candidate; slug rules and invalid-slug behavior unspecified |
| `/professional` | Professional Homepage | Professional Home | Candidate; verify label and destination |
| `/professional/resume` | Resume | Professional Resume | Candidate; verify navigation and verified resume file |
| `/professional/experience` | Experience | Professional Experience | Candidate; verify navigation |
| `/professional/work` | Professional Work | Professional Work | Candidate; verify whether entries are case studies |
| `/professional/work/[slug]` | Case Study | Professional work detail implied by Work | Candidate; slug rules and invalid-slug behavior unspecified |
| `/professional/services` | Services | Professional Services | Candidate; verify navigation |
| `/professional/articles` | Articles and Research | Professional Articles & Researches | Candidate; verify exact label and scope |
| `/professional/articles/[slug]` | Article Details | Professional article detail implied by Articles & Researches | Candidate; slug rules and invalid-slug behavior unspecified |
| `/contact` | Shared Contact | Shared Contact; Personal Contact / Send a Message; professional inquiry pathways | **Owner decision recorded for review (PD-014-A):** one shared canonical `/contact` page with Personal/Professional visual context; formal route-map closure still pending |
| `/license` | License | Shared License | Candidate |
| `/terms` | Terms | Shared Terms | Candidate |
| `/privacy` | Privacy | Shared Privacy | Candidate |
| `/changelog` | Changelog | Shared Changelog | Candidate |

SDD Section 5.2 also lists `/api/contact`, `/api/likes`, and `/api/github`; these are API endpoint candidates and are inventoried separately below.

### 2.2 UIR identities without an established standalone route

The UIR identifies these experiences/elements, but does not settle whether each is a route, section, embedded component, or navigation action.

| UIR identity | What must be resolved |
|---|---|
| Personal Work With Me | Home section, standalone page, or entry point to a contact experience |
| Personal Contact / Send a Message | **Owner decision recorded for review (PD-014-A):** use the shared canonical `/contact` destination with Personal visual context; formal route-map closure still pending |
| Personal Common Questions | Standalone page or section; confirm navigation and interaction |
| Personal Activity | Embedded component or standalone activity destination |
| Professional More About Me | Standalone page or section |
| Professional Resource / Activity | Standalone page, section, or shared activity component |
| GitHub Activity | UIR says Activity defaults to GitHub Activity; confirm placement and whether it is only a component |
| AI Usage Activity | UIR says this is an alternate Activity selection; provider and metrics remain pending |
| Visits / Likes / Stars | Engagement indicators/components unless the references establish separate destinations |

### 2.3 Navigation rules still requiring source verification

Before PD-014 can close, inspect the original PDFs and prototype and record:
- Exact navigation labels, order, grouping, and destinations for Introduction, Personal, Professional, and shared navigation.
- Whether Work With Me, Common Questions, More About Me, Resource, and Activity are pages, sections, or component states.
- Whether Personal and Professional contact entry points share one page or have distinct form/context experiences.
- Dynamic content slug format, uniqueness scope, case sensitivity, and invalid-slug/not-found behavior.
- Canonical URL, trailing-slash policy, redirects/aliases, and browser navigation behavior.
- Whether legal and changelog pages are global or portfolio-contextual.

Do not infer these answers from page names alone.

## 3. API contract inventory

### 3.1 Source-defined endpoint and method inventory

| Endpoint | Method | Source-defined responsibility | Contract status |
|---|---|---|---|
| `/api/contact` | POST | Receive, validate, sanitize, protect, and email contact submission through Resend | Path/method/workflow are stated; exact field constraints, schema, status codes, and error body remain undefined |
| `/api/likes` | GET | Retrieve current like count and whether the current anonymous visitor has liked the content item | Method and purpose stated; query parameter names, content type/ID format, response schema, and status codes undefined |
| `/api/likes` | POST | Submit a like and return updated engagement information | Method and purpose stated; request schema, duplicate response representation, status codes, and error body undefined |
| `/api/github` | GET | Retrieve GitHub repository information / Stargazer counts | Method and purpose stated; repository selection inputs, response schema, cache policy, status codes, and fallback contract undefined |

**Owner decision recorded for review (FB-001):** Feedback is included in Version 1.0 as a separate workflow from Contact, with three approved submission categories:

1. **Bug Report** — report a problem and provide reproduction steps.
2. **General Feedback** — suggestions, comments, and improvement ideas.
3. **Security Concern** — a safe initial description, with clear guidance not to submit credentials or sensitive exploit details through the public form.

For the Bug Report category, the owner has additionally decided that the form shall include a **Steps to Reproduce** field and that this field is **optional**. A Bug Report may be submitted without reproduction steps when all required fields are completed. This decision does not define which other fields are required or their validation constraints. The owner has also decided that **Bug Title** is a required field summarizing the issue. A Bug Report must include a Bug Title and all other required fields; Steps to Reproduce may be omitted. The owner has additionally approved an **Expected Result** field describing what the user thought should happen; this field is **optional**. The owner has also approved an **Actual Result** field describing what happened instead; this field is **optional**. The owner has also approved an **Environment** field as **optional**, for relevant context such as browser, operating system, and device. The owner has additionally decided to include an optional **Screenshot or Attachment** field so a reporter may provide visual evidence; the field may be omitted. The owner selected **images and documents** as the accepted file categories: PNG, JPG/JPEG, WebP, and PDF. The owner further decided to allow **one file per Bug Report**. The maximum attachment size is **5 MB per file**. The attachment shall be uploaded directly with the Bug Report submission as part of the same submission flow, not through a separate post-submission upload step. This records the user-facing workflow only. The owner has also decided that Bug Report attachments shall be stored temporarily for processing and then deleted; the owner has specified deletion **24 hours after upload**. The owner has approved automatic deletion retries until deletion succeeds if an initial deletion attempt fails; the attachment must remain unavailable to users during retry/recovery. If the attachment remains undeleted 24 hours after its scheduled deletion time (that is, 48 hours after upload), the system must send an internal administrative alert. The administrative alert shall be sent **once only**, when the 48-hour-after-upload threshold is first reached (24 hours after scheduled deletion); it shall not be repeated periodically. The owner has approved **email via Resend**, reusing the project's selected email provider, as the administrative alert channel, with **laurenceegay1@gmail.com** as the recipient. The owner has approved a **dedicated administrative-alert sender identity**, separate from the contact-form sender identity. The exact sender email address and verified sending domain must be confirmed; do not assume `system-alerts@your-domain` is an actual approved address. The owner has confirmed that the system will be deployed on **Vercel** (consistent with the approved TSS hosting baseline). The production custom domain and dedicated sender email address/domain cannot be confirmed yet and remain **deferred/open**; no domain or sender address is to be inferred. Vercel deployment does not itself establish a custom domain or a verified Resend sender domain. Resend-specific sender configuration, delivery-failure handling, retry schedule, maximum retry duration, and final cleanup escalation remain to be specified.

No feedback endpoint is established in the SDD API table; SDD TD-011 remains open for processing design. Do not silently route feedback through `/api/contact` or invent a feedback endpoint, schema, or retention policy. The remaining UI fields and constraints, processing path, provider/storage, abuse controls, response behavior, and retention must be specified before implementation.

### 3.2 Contact behavior established by SDD

- Processing flow: browser form → Next.js backend → server-side validation and spam/abuse protection → Resend → backend result → UI success/failure state.
- Fields identified by the SDD: name, email address, subject, and message. Exact required/optional status, length limits, formats, and UI-specific constraints are not stated here; verify the original form reference and requirements.
- No permanent application-side contact-submission database.
- Distinguish invalid input, spam/rejected submissions, provider errors, and accepted email requests.
- Do not show success until Resend accepts the send request; provider acceptance does not guarantee inbox delivery.
- On failure, provide an appropriate failure state and retry opportunity.
- Security requirements include server-side validation, rate limiting, spam prevention, secure credentials, safe errors, and email-header-injection protection.

### 3.3 Likes behavior established by SDD

- Upstash Redis is the persistent like store; conceptual operations are set membership, atomic insertion, and set cardinality (`SISMEMBER`, `SADD`, `SCARD`).
- One like means one per persistent anonymous visitor identity per content item, not one per human.
- The frontend requests count and visitor-like status; the backend obtains/validates visitor identity and content identity.
- Duplicate requests, refreshes, and simultaneous requests must not create duplicate records for the same visitor/content pair.
- Like counts must persist across redeployments. No automatic expiration unless explicitly approved.
- Failed requests must not falsely increase the displayed count.
- Invalid content identifiers, missing identity, duplicates, storage failures, network errors, and rate limiting must be handled.
- Signed server-issued HttpOnly cookie and server-side visitor hash are described as recommended security design; lifetime, rotation, SameSite, and exact identity policy remain unresolved.
- Raw visitor identifiers and secrets must not appear in public API responses.

### 3.4 GitHub behavior established by SDD

- GitHub REST API is authoritative for public repository metadata and Stargazer counts.
- Associate counts with the correct repositories; do not create a separate application-side star counter.
- Cache results, handle rate limits and unavailable repositories, and display the latest successfully retrieved count.
- Exact repositories, endpoints, authentication/token policy, cache duration, stale-data behavior, and response/error schema remain unresolved.

### 3.5 Cross-cutting API requirements

- Use Next.js Route Handlers within the modular monolith.
- Validate public input server-side using the approved Zod technology; client validation is not a substitute.
- Keep credentials server-side and out of source control/browser bundles.
- Protect public endpoints against abuse and apply appropriate rate limits.
- Avoid exposing visitor identifiers or secrets.
- Do not invent HTTP status codes, JSON envelopes, field names beyond the source-identified contact fields, or retry semantics where the source does not specify them.

## 4. Environment variable inventory

The SDD-listed names currently recorded in the foundation register are:

| Variable | Source purpose | Unresolved detail |
|---|---|---|
| `RESEND_API_KEY` | Resend credential | Credential provisioning and sender identity/domain |
| `CONTACT_EMAIL` | Contact recipient | Owner-confirmed recipient address |
| `UPSTASH_REDIS_REST_URL` | Upstash REST endpoint | Instance and environment mapping |
| `UPSTASH_REDIS_REST_TOKEN` | Upstash credential | Secret provisioning and environment mapping |
| `VISITOR_COOKIE_SECRET` | Visitor identity protection | Signing algorithm, lifetime, rotation, cookie policy |
| `VISITOR_HASH_SECRET` | Protected visitor hash derivation | Hashing scheme and rotation/migration policy |
| `GITHUB_TOKEN` | Conditional GitHub API authentication | Whether required for selected public read operations and least-privilege policy |

These names are not a complete environment contract. No secret values belong in the repository. TSS calls for Local Development, Preview, and Production separation; Preview must not send real contact messages or mutate production likes.

## 5. Open decision register and gates

| ID / topic | Current state | Required closure evidence |
|---|---|---|
| SRS PD-014 / SDD TD-007 — canonical routes | Partially resolved; still open and blocking route skeleton. PD-014-A owner decision recorded for review: one shared `/contact` destination with Personal/Professional visual context. | Owner-reviewed route/navigation matrix verified against original UI PDFs and prototype; remaining mappings and URL rules still require closure |
| UIR page identity mapping | Open | Page/section/component/destination classification for every unmapped identity |
| Dynamic slug and not-found behavior | Open | Approved content identity and URL rules |
| Contact field constraints and API schema | Partial | Exact UI fields and validation constraints, request/response/error contract |
| Contact anti-abuse and rate limits | Open | Approved abuse controls, thresholds, and failure behavior |
| Contact sender/recipient and Resend operations | Open | Verified sender identity, recipient, environment mapping, retry/idempotency policy |
| Feedback MOD-010 / SDD TD-011 | **Scope decision recorded for review (FB-001): included in Version 1.0 as a workflow separate from Contact.** Processing design remains open. | Define UI and fields, processing destination/endpoint, request/response/error contract, abuse controls, failure behavior, and retention; verify against SRS/UI references |
| Visitor identity / SDD TD-013 | Partial | Cookie lifetime, signing/rotation, SameSite, secure settings, identity migration |
| Likes API schema | Partial | Content type/ID contract, GET/POST payloads and response/error contract |
| Redis / SDD TD-012 and TD-014 | Open | Instance/environment separation, key naming, retention, backup/recovery, no-expiry confirmation |
| GitHub / SDD TD-005 | Partial | Repository mapping, API selection, token policy, cache duration, rate-limit and stale fallback |
| AI Usage / SDD TD-006 | Open | Provider, source data, metrics, display meaning; no inferred provider |
| Analytics / SDD TD-009 | Open | Vercel plan eligibility and approved event/privacy configuration |
| Deployment / SRS PD-015 and SDD TD-008/010 | Open | Domain, hosting configuration, monitoring, alerting, operational ownership |

## 6. Implementation disposition

| Work item | Disposition |
|---|---|
| Preserve foundation branch and current package bootstrap | Proceed |
| Maintain source-based route reconciliation | Proceed |
| Create canonical public route files | Blocked on PD-014 and UI verification |
| Implement contact/likes/GitHub handlers | Blocked on complete endpoint contracts and security/operational decisions |
| Implement separate Version 1.0 Feedback workflow | Scope confirmed by owner (FB-001); implementation remains blocked on SDD TD-011 processing and API/UI contracts |
| Implement AI Usage activity provider | Blocked on SDD TD-006 |
| Add route-specific visual components | Blocked on original reference inspection and route/page identity verification |
| Production deployment configuration | Defer to deployment planning |

## 7. Owner decisions requested

To close the next planning gate, the owner needs to decide or provide evidence for:
1. The page/section/component classification and navigation destinations for the nine UIR identities in Section 2.2.
2. **PD-014-A — recorded owner decision for review:** Personal and Professional contact entry points use one shared canonical `/contact` page with Personal/Professional visual context. This does not yet close PD-014; remaining route mappings and URL rules remain open.
3. **FB-001 — owner scope decision recorded for review:** include Feedback (SRS MOD-010) in Version 1.0 as a workflow separate from Contact. Its processing design remains pending under SDD TD-011.
4. The canonical route policy and dynamic slug rules after reviewing the original prototype and PDFs.
5. The missing API schema details and operational policies listed in Sections 3 and 5.

No default choices are silently selected in this document. PD-014-A and FB-001 are explicit owner decisions recorded for review. PD-014-A does not close the full route decision; FB-001 confirms Feedback scope only and does not close SDD TD-011 or authorize an endpoint. Once remaining decisions are supplied, update the route register and API specification through controlled review before creating route files or handlers.

## 8. Source references

- SRS-CWK-001 v1.0: project scope, MOD-007 Contact, MOD-008 Activity, MOD-010 Feedback, PD-014 routes, PD-015 deployment, and open decisions.
- SDD-CWK-001 v1.0: Sections 2, 5, 9, 10, 12, 13, and 22; proposed route map, endpoint methods, processing workflows, security controls, and pending technical decisions.
- TSS-CWK-001 v1.0 Revision 1: approved toolchain and environment separation expectations.
- UIR-CWK-001 v1.0: page/component inventory and navigation verification gaps.
- RFP-CWK-001 v1.0 (controlled amendments): staged implementation and no-guessing boundary.

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

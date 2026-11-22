# Route Reconciliation Record

**Record ID:** RRR-CWK-001  
**Version:** 1.0  
**Date:** 2026-11-22  
**Repository:** Code-With-Kira/CWK_E-Portfolio  
**Working branch:** `chore/repository-foundation`  
**Status:** Author reconciliation completed; PD-014-A owner decision recorded for review; other owner decisions remain open

## 1. Purpose and authority

This record compares the proposed route inventory in SDD-CWK-001 Version 1.0, the page identities in approved UIR-CWK-001 Version 1.0, and the pending route decision PD-014 in SRS-CWK-001 Version 1.0.

It is a reconciliation aid, not an amendment to the approved SDD/SRS and not owner approval of canonical URLs. Where the sources do not settle a path, the mapping remains unresolved.

## 2. Source-grounded route candidates

The following paths are transcribed from SDD Section 5.2. Their presence in the SDD does not make them final: Section 5.2 explicitly calls them proposed and requires reconciliation with UI navigation and the SRS.

| SDD proposed path | SDD purpose | UIR identity / coverage | Reconciliation status |
|---|---|---|---|
| `/` | Introduction | Introduction / landing; profile selection; Personal and Professional previews | Candidate is consistent with the entry experience; exact navigation behavior still needs prototype verification |
| `/personal` | Personal Homepage | Personal Home | Candidate; verify navigation label and destination |
| `/personal/about` | About | Personal About | Candidate; verify navigation |
| `/personal/projects` | Personal Projects | Personal Projects | Candidate; verify listing and detail relationship |
| `/personal/projects/[slug]` | Project Details | Personal project details implied by Projects | Candidate; slug format and invalid-slug behavior not specified |
| `/personal/blog` | Blog | Personal Blog | Candidate; verify whether this is the exact UIR Blog destination |
| `/personal/blog/[slug]` | Blog Article | Personal blog article implied by Blog | Candidate; slug format and invalid-slug behavior not specified |
| `/professional` | Professional Homepage | Professional Home | Candidate; verify navigation label and destination |
| `/professional/resume` | Resume | Professional Resume | Candidate; verify navigation |
| `/professional/experience` | Experience | Professional Experience | Candidate; verify navigation |
| `/professional/work` | Professional Work | Professional Work | Candidate; verify whether work items are case studies |
| `/professional/work/[slug]` | Case Study | Professional work detail implied by Work | Candidate; slug format and invalid-slug behavior not specified |
| `/professional/services` | Services | Professional Services | Candidate; verify navigation |
| `/professional/articles` | Articles and Research | Professional Articles & Researches | Candidate; verify exact label and content scope |
| `/professional/articles/[slug]` | Article Details | Professional article detail implied by Articles & Researches | Candidate; slug format and invalid-slug behavior not specified |
| `/contact` | Shared Contact | Shared Contact; Personal Contact / Send a Message; Professional inquiry pathways | **Owner decision recorded for review (PD-014-A):** one shared canonical `/contact` page with Personal/Professional visual context; full PD-014 closure remains pending |
| `/license` | License | Shared License | Candidate |
| `/terms` | Terms | Shared Terms | Candidate |
| `/privacy` | Privacy | Shared Privacy | Candidate |
| `/changelog` | Changelog | Shared Changelog | Candidate |
| `/api/contact` | Contact Processing | Contact form behavior | Endpoint candidate; complete API contract not defined |
| `/api/likes` | Like Processing | Like indicators for projects/articles | Endpoint candidate; complete API contract not defined |
| `/api/github` | GitHub Information Retrieval | GitHub Activity and Stargazer indicators | Endpoint candidate; complete API contract not defined |

## 3. UIR identities not mapped to standalone SDD routes

The following UIR page/component identities do not have a dedicated standalone route in the SDD Section 5.2 table. The sources do not establish whether each is a page, section, component, modal, or navigation destination.

| UIR identity | Known context | Required resolution |
|---|---|---|
| Personal Work With Me | Personal portfolio | Determine whether this is a section on Personal Home, a standalone page, or an entry point to Contact |
| Personal Contact / Send a Message | Personal portfolio | **Owner decision recorded for review (PD-014-A):** use the shared `/contact` page with Personal visual context |
| Personal Common Questions | Personal portfolio | Determine whether it is a standalone page or a section |
| Personal Activity | Personal portfolio activity/footer elements | Determine whether this is an embedded component or a standalone activity page |
| Professional More About Me | Professional worksite | Determine whether it is a standalone page or a section |
| Professional Resource / Activity | Professional worksite | Determine whether it is a standalone page, section, or shared activity component |
| GitHub Activity | Shared activity component | UIR notes the Activity component defaults to GitHub Activity; standalone route not established |
| AI Usage Activity | Alternate Activity component view | UIR notes this is selected through the Activity component; standalone route not established |
| Visits / Likes / Stars | Shared engagement indicators | Treat as UI indicators/components unless the source references establish a separate destination |

## 4. Navigation and URL decisions still open

PD-014 remains pending. Before route files are authored, the project owner must resolve or approve a controlled route map covering:

1. Whether the SDD proposed paths are accepted unchanged.
2. Whether Personal Work With Me, Common Questions, and Professional More About Me are pages or sections.
3. **PD-014-A — owner decision recorded for review:** Personal and Professional contact entry points share one canonical `/contact` page with Personal/Professional visual context. This resolves only the contact-destination question; PD-014 remains open for all other route decisions.
4. Where Resource/Activity and the GitHub/AI Usage activity selector appear in the navigation and page hierarchy.
5. Exact navigation labels and destination mapping from the original UI references.
6. Dynamic content slug constraints, uniqueness scope, case handling, and invalid-slug behavior.
7. Trailing-slash and canonical URL policy.
8. Redirects and aliases, if any.
9. Not-found and error-page behavior.

No route group, redirect, alias, or page file should be created on the assumption that a page identity implies a URL.

## 5. Feedback scope decision and API boundary

**FB-001 — owner decision recorded for review:** Feedback is included in Version 1.0 as a workflow separate from Contact, with three approved categories:

1. **Bug Report** — report a problem and provide reproduction steps.
2. **General Feedback** — suggestions, comments, and improvement ideas.
3. **Security Concern** — a safe initial description, with guidance not to submit credentials or sensitive exploit details through the public form.

For the Bug Report category, the owner has additionally decided that the form shall include a **Steps to Reproduce** field and that this field is **optional**. A Bug Report may be submitted without reproduction steps when all required fields are completed. This does not establish the required status or constraints of any other field. The owner has also decided that **Bug Title** is a required field summarizing the issue. A Bug Report must include a Bug Title and all other required fields; Steps to Reproduce may be omitted. The owner has additionally approved an **Expected Result** field describing what the user thought should happen; this field is **optional**. The owner has also approved an **Actual Result** field describing what happened instead; this field is **optional**. The owner has also approved an **Environment** field as **optional**, for relevant context such as browser, operating system, and device. The owner has additionally decided to include an optional **Screenshot or Attachment** field so a reporter may provide visual evidence; the field may be omitted. The owner selected **images and documents** as the accepted file categories: PNG, JPG/JPEG, WebP, and PDF. The owner further decided to allow **one file per Bug Report**. The maximum attachment size is **5 MB per file**. The attachment shall be uploaded directly with the Bug Report submission as part of the same submission flow, not through a separate post-submission upload step. This records the user-facing workflow only. The owner has also decided that Bug Report attachments shall be stored temporarily for processing and then deleted; the owner has specified deletion **24 hours after upload**. The owner has approved automatic deletion retries until deletion succeeds if an initial deletion attempt fails; the attachment must remain unavailable to users during retry/recovery. If the attachment remains undeleted 24 hours after its scheduled deletion time (that is, 48 hours after upload), the system must send an internal administrative alert. The administrative alert shall be sent **once only**, when the 48-hour-after-upload threshold is first reached (24 hours after scheduled deletion); it shall not be repeated periodically. The owner has approved **email via Resend**, reusing the project's selected email provider, as the administrative alert channel, with **laurenceegay1@gmail.com** as the recipient. The owner has approved a **dedicated administrative-alert sender identity**, separate from the contact-form sender identity. The exact sender email address and verified sending domain must be confirmed; do not assume `system-alerts@your-domain` is an actual approved address. The owner has confirmed that the system will be deployed on **Vercel** (consistent with the approved TSS hosting baseline). The production custom domain and dedicated sender email address/domain cannot be confirmed yet and remain **deferred/open**; no domain or sender address is to be inferred. Vercel deployment does not itself establish a custom domain or a verified Resend sender domain. Resend-specific sender configuration, delivery-failure handling, retry schedule, maximum retry duration, and final cleanup escalation remain to be specified.

It must not be silently processed through `/api/contact`. The SDD does not establish a feedback endpoint or complete processing contract. SDD TD-011 remains open. The remaining UI fields, processing destination, endpoint (if required), validation, response/error behavior, anti-abuse controls, failure handling, and retention must be defined and reconciled with SRS MOD-010 and the original Shared Components reference before implementation. This scope decision does not authorize a guessed route or handler.

## 6. API route boundary

The three SDD API paths are retained as endpoint candidates only. The SDD describes responsibilities but does not provide a complete machine-readable contract for request fields, response schemas, status codes, error envelopes, rate-limit thresholds, origin policy, or idempotency.

Do not implement handlers until those contracts and their security controls are approved or explicitly recorded as implementation decisions under the governing change process.

## 7. Implementation disposition

- The root introduction route is present in the SDD proposal and is consistent with the UIR entry experience, but the exact screen implementation must still follow the original PDF/prototype.
- All other SDD routes remain proposed until PD-014 is closed.
- UIR-only identities listed in Section 3 remain unmapped.
- No application route files are created by this record.
- No API handlers are created by this record.

## 8. Source references

- SDD-CWK-001 Version 1.0, Sections 2, 4, 5.2, 5.3, and 6.
- SRS-CWK-001 Version 1.0, PD-014 and the system/page/navigation requirements.
- UIR-CWK-001 Version 1.0, Sections 4–7.
- Original UI references: Introduction & Profile Selection, Personal Portfolio, Professional Worksite, Shared Components & Pages, and Interactive Prototypes.

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

### Owner decision — engagement-event storage provider

The owner has approved **Upstash Redis** as the storage provider for the approved introduction engagement event **`proceed_to_dual_profile`**. Engagement-event records must be kept logically separate from the existing Portfolio Likes Redis sets; the event implementation must not reuse or alter the Like set data model. This approval selects the provider only. The Redis key design, event schema and metadata, write/read access patterns, retention and expiry policy, privacy controls, reporting/query approach, operational limits, and failure behavior remain unresolved and must be specified before implementation. This decision does not authorize storing general page views or other unapproved visitor activity.

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

For the Bug Report category, the owner has additionally decided that the form shall include a **Steps to Reproduce** field and that this field is **optional**. A Bug Report may be submitted without reproduction steps when all required fields are completed. This decision does not define which other fields are required or their validation constraints. The owner has also decided that **Bug Title** is a required field summarizing the issue. A Bug Report must include a Bug Title and all other required fields; Steps to Reproduce may be omitted. The owner has additionally approved an **Expected Result** field describing what the user thought should happen; this field is **optional**. The owner has also approved an **Actual Result** field describing what happened instead; this field is **optional**. The owner has also approved an **Environment** field as **optional**, for relevant context such as browser, operating system, and device. The owner has additionally decided to include an optional **Screenshot or Attachment** field so a reporter may provide visual evidence; the field may be omitted. The owner selected **images and documents** as the accepted file categories: PNG, JPG/JPEG, WebP, and PDF. The owner further decided to allow **one file per Bug Report**. The maximum attachment size is **5 MB per file**. The attachment shall be uploaded directly with the Bug Report submission as part of the same submission flow, not through a separate post-submission upload step. This records the user-facing workflow only. The owner has also decided that Bug Report attachments shall be stored temporarily for processing and then deleted; the owner has specified deletion **24 hours after upload**. The owner has approved automatic deletion retries until deletion succeeds if an initial deletion attempt fails; the attachment must remain unavailable to users during retry/recovery. Retry schedule, maximum retry duration, alerting, and final cleanup escalation remain to be specified.

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

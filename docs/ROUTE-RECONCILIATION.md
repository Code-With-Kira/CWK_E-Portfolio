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

For the Bug Report category, the owner has additionally decided that the form shall include a **Steps to Reproduce** field and that this field is **optional**. A Bug Report may be submitted without reproduction steps when all required fields are completed. This does not establish the required status or constraints of any other field. The owner has also decided that **Bug Title** is a required field summarizing the issue. A Bug Report must include a Bug Title and all other required fields; Steps to Reproduce may be omitted. The owner has additionally approved an **Expected Result** field describing what the user thought should happen; this field is **optional**. The owner has also approved an **Actual Result** field describing what happened instead; this field is **optional**. The owner has also approved an **Environment** field as **optional**, for relevant context such as browser, operating system, and device. The owner has additionally decided to include an optional **Screenshot or Attachment** field so a reporter may provide visual evidence; the field may be omitted. The owner selected **images and documents** as the accepted file categories: PNG, JPG/JPEG, WebP, and PDF.

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

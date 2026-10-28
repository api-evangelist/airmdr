# AirMDR

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

AirMDR is an AI-native managed detection and response (MDR) provider whose virtual security analyst, Darryl, automates alert triage, investigation and response across endpoint, cloud, SaaS, identity, email and network tools. The platform ingests alerts from 200+ integrations, runs automated or AI-generated investigation playbooks, and produces documented cases; it is sold as a full-service MDR for small security teams, an AI SOC platform for MSSPs and enterprise SOCs, and a free plan with 100 alert investigations. Programmatic access is a REST API on app.airmdr.com (Case Manager and User Management services, documented in Redoc), authenticated with an API token sent as a Session cookie, plus a webhook endpoint for pushing alerts into the platform.

**Areas:** Security · Managed Detection and Response · Security Operations · Alert Triage · Incident Response · AI Agents · SOC Automation · Threat Detection · MCP · A2A

## AirMDR on APIs.io

Everything profiled for AirMDR is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/airmdr/](https://apis.io/providers/airmdr/)** — or go straight to one of the APIs or properties below.

### APIs (23)

- [AirMDR Documentation MCP Server](https://apis.io/apis/airmdr/airmdr-documentation-mcp-server/) — Hosted, unauthenticated Streamable-HTTP MCP server on the AirMDR documentation host (Mintlify-operated) exposing three tools: search the AirMDR…
- [AirMDR Alert Catalog API](https://apis.io/apis/airmdr/airmdr-alertcatalog-api/) — The AlertCatalog API from AirMDR — 8 operation(s) for alertcatalog.
- [AirMDR Alerts API](https://apis.io/apis/airmdr/airmdr-alerts-api/) — The Alerts API from AirMDR — 15 operation(s) for alerts.
- [AirMDR Alert Types API](https://apis.io/apis/airmdr/airmdr-alerttypes-api/) — The AlertTypes API from AirMDR — 3 operation(s) for alerttypes.
- [AirMDR Case Manager API](https://apis.io/apis/airmdr/airmdr-case-manager-api/) — The Case Manager API from AirMDR — 32 operation(s) for case manager.
- [AirMDR Case Manager Internal API](https://apis.io/apis/airmdr/airmdr-case-manager-internal-api/) — The Case Manager Internal API from AirMDR — 10 operation(s) for case manager internal.
- [AirMDR Case Manager V2 API](https://apis.io/apis/airmdr/airmdr-case-manager-v2-api/) — The Case Manager V2 API from AirMDR — 43 operation(s) for case manager v2.
- [AirMDR Case Decision Automation API](https://apis.io/apis/airmdr/airmdr-casedecisionautomation-api/) — The CaseDecisionAutomation API from AirMDR — 4 operation(s) for casedecisionautomation.
- [AirMDR Dashboard API](https://apis.io/apis/airmdr/airmdr-dashboard-api/) — The Dashboard API from AirMDR — 20 operation(s) for dashboard.
- [AirMDR Internal API](https://apis.io/apis/airmdr/airmdr-internal-api/) — The Internal API from AirMDR — 8 operation(s) for internal.
- [AirMDR Mitre Tactics API](https://apis.io/apis/airmdr/airmdr-mitretactics-api/) — The MitreTactics API from AirMDR — 1 operation(s) for mitretactics.
- [AirMDR Organization API](https://apis.io/apis/airmdr/airmdr-organization-api/) — Endpoints to manage organizations
- [AirMDR Password API](https://apis.io/apis/airmdr/airmdr-password-api/) — Endpoints to manage user password
- [AirMDR Permission API](https://apis.io/apis/airmdr/airmdr-permission-api/) — Endpoints to read system permissions
- [AirMDR Ping API](https://apis.io/apis/airmdr/airmdr-ping-api/) — The Ping API from AirMDR — 1 operation(s) for ping.
- [AirMDR Query DSL API](https://apis.io/apis/airmdr/airmdr-query-dsl-api/) — The Query DSL API from AirMDR — 3 operation(s) for query dsl.
- [AirMDR Security Review API](https://apis.io/apis/airmdr/airmdr-security-review-api/) — The Security Review API from AirMDR — 5 operation(s) for security review.
- [AirMDR Session API](https://apis.io/apis/airmdr/airmdr-session-api/) — Endpoints to manage sessions
- [AirMDR Token API](https://apis.io/apis/airmdr/airmdr-token-api/) — Endpoints to manage tokens
- [AirMDR Trial API](https://apis.io/apis/airmdr/airmdr-trial-api/) — The Trial API from AirMDR — 1 operation(s) for trial.
- [AirMDR User API](https://apis.io/apis/airmdr/airmdr-user-api/) — Endpoints to manager users
- [AirMDR User Group API](https://apis.io/apis/airmdr/airmdr-user-group-api/) — Endpoints to manage user groups
- [AirMDR Webhooks API](https://apis.io/apis/airmdr/airmdr-webhooks-api/) — The Webhooks API from AirMDR — 3 operation(s) for webhooks.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Airmdr Webhooks](https://apis.io/asyncapis/airmdr/airmdr-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [AirMDR documentation MCP](https://apis.io/servers/airmdr/airmdr-documentation-mcp/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Airmdr Case Manager Overlay](https://apis.io/overlays/airmdr/airmdr-case-manager-overlay/)
- [Airmdr User Management Service Overlay](https://apis.io/overlays/airmdr/airmdr-user-management-service-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Airmdr Authentication](https://apis.io/security/airmdr/airmdr-authentication/)
- [Airmdr Domain Security](https://apis.io/security/airmdr/airmdr-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Airmdr Plans Pricing](https://apis.io/plans/airmdr/airmdr-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Airmdr Rate Limits](https://apis.io/rate-limits/airmdr/airmdr-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://airmdr.com/)
- [Documentation](https://docs.airmdr.com/essentials/Landingpage)
- [Getting started](https://docs.airmdr.com/api-reference/apitoken)
- [API reference](https://docs.airmdr.com/api-reference/apilandingpage)
- [Pricing](https://airmdr.com/pricing)
- [Support](https://airmdr.com/contact-us)
- [Changelog](https://docs.airmdr.com/changelog/changelog)
- [Blog](https://airmdr.com/blog)
- [Privacy policy](https://airmdr.com/privacy)
- [GitHub](https://github.com/AirMDR)

## API Evangelist rating

**Kin Score 55.1** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 81.7 |
| Contract quality | 52.2 |
| Contract governance | 4.5 |
| Operational transparency | 26.3 |
| Developer ergonomics | 59.5 |
| Access clarity | 59.2 |

**Agent readiness 45.4** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | documented (partial credit) |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | verified |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 20.6** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/airmdr/](https://apis.io/providers/airmdr/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for AirMDR: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/airmdr/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).

---
name: airmdr-ingest-alert-and-track-investigation
description: Push a security alert into AirMDR by API so Darryl investigates it, then follow the investigation through to the case it produces.
api: AirMDR Case Manager API
generated: '2026-09-19'
method: generated
source: openapi/airmdr-case-manager-openapi.yml, openapi/airmdr-user-management-service-openapi.yml, https://docs.airmdr.com/api-reference/WebHook
operations:
  - getOrganizationListAPI
  - createAlertsAPI
  - createAlertFromWebhookAPI
  - getAlertAPI
  - getCaseAPIV2
---

# Ingest an alert and track its investigation

Base URL: `https://app.airmdr.com/airmdrapi`. Authenticate every call with `Cookie: Session="<API token>"`
(see `authentication/airmdr-authentication.yml`) and send `User-ID` and `Organization-ID` headers.

## Steps

1. **Resolve the organization code.** `getOrganizationListAPI` (`GET /organization`, User Management
   service) returns the organizations the token can act on; take `organization_code` (e.g. `ASO`).
2. **Create the alert.** `createAlertsAPI` (`POST /alerts`) with a `CreateAlertsRequest` body carrying
   `alert_content`, `alert_provider`, `alert_type` and `organization_code` (`created_at_source` epoch seconds
   is optional). Supply `alert_type`: without it Darryl does not auto-investigate. The 201 response returns
   `alert_uuid`, `alert_id` (`ORG-PROVIDER-<seq>`) and `investigation_status: 0`.
   - Alternative for sources that cannot set headers: `createAlertFromWebhookAPI`
     (`POST /webhooks/{webhook_id}/{secret}/alerts`) — the whole body is the alert content; a repeat of the same
     alert answers `409 Duplicate alert`, so do not retry a 409.
3. **Poll the investigation.** `getAlertAPI` (`GET /alerts/{alert_id}`) until `investigation_status` reaches
   15 (Completed) or 20 (Failed); intermediate values are 5 Submitted and 10 InProgress. Back off between polls —
   no rate-limit headers are published (`rate-limits/airmdr-rate-limits.yml`).
4. **Read the case.** When the investigation completes, the alert's case identifier (`ORG-<n>`) resolves through
   `getCaseAPIV2` (`GET /v2/case/{case_uuid}`), which accepts the UUID or the human case id.

## Rules

- Errors are `{ "message": string }`; a `401` means the token is missing or expired — regenerate it, do not loop.
- There is no idempotency key on `createAlertsAPI` (`conventions/airmdr-conventions.yml`, `idempotency.coverage: none`):
  a retried POST creates a second alert. Use the webhook route if you need duplicate rejection.
- Alert hard deletes (`hardDeleteAlertAPI`) are irreversible; prefer leaving investigated alerts in place.

---
name: airmdr-triage-and-close-case
description: List open AirMDR cases, read one, update its status or severity with a comment, and archive it when done.
api: AirMDR Case Manager API
generated: '2026-09-19'
method: generated
source: openapi/airmdr-case-manager-openapi.yml
operations:
  - getCasesForOrgAPIV2
  - getCaseAPIV2
  - updateCaseAPIV2
  - addCaseCommentAPI
  - getCaseHistoryAPI
  - archiveCaseAPI
---

# Triage and close a case

Base URL: `https://app.airmdr.com/airmdrapi`, `Cookie: Session="<API token>"`, plus `User-ID` and
`Organization-ID` headers on every call.

## Steps

1. **List cases.** `getCasesForOrgAPIV2` (`POST /v2/case/list?page=1&size=50`) with a `CaseListRequest` body:
   `requested_view` is required; filter with `CaseFilter` (`status`, `severity`, `priority`, `assignee`,
   `from_modified_date`/`to_modified_date` as epoch seconds) and order with `sort[] {field, sort_order}`.
   `page` and `size` are required query parameters; the response carries `data[]` and `total`.
2. **Read the case.** `getCaseAPIV2` (`GET /v2/case/{case_uuid}`) — UUID or human id (`ASO-13812`).
3. **Update it.** `updateCaseAPIV2` (`PATCH /v2/case/{case_uuid}`) with an `UpdateCaseRequestV2` body.
   `CaseStatus` is an integer enum: 0 New, 1 In progress, 5 Pending, 10 Waiting for customer, 20 Contained,
   30 Closed. Send only the fields you change.
4. **Record why.** `addCaseCommentAPI` (`POST /v2/case/{case_uuid}/comment`) with an `UpsertCaseCommentRequest`.
5. **Verify the trail.** `getCaseHistoryAPI` (`GET /v2/case/{case_uuid}/history?page=1&size=20`) shows the change
   log; `getCaseAtHistoryEntryAPI` reconstructs any prior state read-only.
6. **Archive when finished.** `archiveCaseAPI` (`DELETE /v2/case/{case_uuid}`) archives; it is not the hard delete.

## Rules

- No unarchive operation exists in the spec (`conventions/airmdr-conventions.yml` reversibility) — confirm before
  archiving. Never call `deleteCaseAPI` (`/hard_delete`) from an automated flow; it is terminal.
- PATCH carries no idempotency key; make updates convergent (set absolute values, never increment).
- `403` bodies carry the fixed message "User does not have permission to perform this action" — the token's role,
  not the request, is the problem.

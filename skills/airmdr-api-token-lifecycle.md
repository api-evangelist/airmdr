---
name: airmdr-api-token-lifecycle
description: Create, list and revoke AirMDR API tokens by API, scoped to an organization the caller can access.
api: AirMDR User Management Service API
generated: '2026-09-19'
method: generated
source: openapi/airmdr-user-management-service-openapi.yml, https://docs.airmdr.com/api-reference/apitoken
operations:
  - createAPITokenForUserAPI
  - listTokensForUserAPI
  - deleteTokenAPI
  - getSessionAPI
---

# API token lifecycle

Base URL: `https://app.airmdr.com/airmdrapi`. An existing token (or console session) authenticates these calls via
`Cookie: Session="<token>"`. Token management requires the Admin or Super Admin role.

## Steps

1. **Check who you are.** `getSessionAPI` (`GET /session`) returns the session's user and organization context.
2. **Create a token.** `createAPITokenForUserAPI` (`POST /users/tokens`) with `{ "name": "<purpose>" }` and an
   optional `organization_id` to scope it to another accessible organization (a non-accessible one answers `403`).
   The token value is returned once — store it in a secrets manager immediately.
3. **Inventory tokens.** `listTokensForUserAPI` (`GET /users/tokens`) lists tokens the user created.
4. **Revoke.** `deleteTokenAPI` (`DELETE /users/tokens/{token_id}`) — the documented revocation path; there is no
   rotate endpoint, so create the replacement first, cut over, then delete the old one.

## Rules

- Tokens can expire; treat `401` as "regenerate", per https://docs.airmdr.com/api-reference/apitoken.
- No scope vocabulary is published (`scopes/` not emitted); scoping is by organization only.
- Use one token per integration, as the docs recommend, so revocation is surgical.

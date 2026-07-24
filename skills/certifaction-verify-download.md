---
name: Verify and retrieve a signed document with Certifaction
description: Download and decrypt an archived signed document and revoke Certifaction's access when done.
api: openapi/certifaction-local-api-openapi.yml
operations: [download_file, remove_access, get_user]
generated: '2026-07-18'
method: generated
---

# Verify and retrieve a signed document with Certifaction

Retrieve a signed document from the digital archive and manage access.

## Auth
`Authorization` header with an API key or OIDC access token
(`authentication/certifaction-authentication.yml`).

## Steps
1. `get_user` (`GET /user`) — confirm the authenticated account.
2. `download_file` (`GET /download`) — download and decrypt a document from the
   digital archive by its `hash`.
3. `remove_access` (`POST /delete-access`) — remove Certifaction's access to a
   file when it should no longer be retrievable through the platform.

## Notes
- Verification of a document's authenticity can also be done client-side with the
  `@certifaction/verification-core` library against the Certifaction Ethereum
  smart contract (see `components/certifaction-components.yml`).
- Errors are plain HTTP status codes (`errors/certifaction-problem-types.yml`).

---
name: Sign a document with Certifaction
description: Prepare and sign a PDF with Certifaction while keeping the document content local (Zero Document Knowledge).
api: openapi/certifaction-local-api-openapi.yml
operations: [prepare_file, sign_file, get_user]
generated: '2026-07-18'
method: generated
---

# Sign a document with Certifaction

Use the Certifaction Local API (run `certifaction server`, default `http://localhost:8081`)
to sign a PDF. Documents are hashed and E2E-encrypted client-side; only the hash
reaches Certifaction.

## Auth
Send the `Authorization` header with a server-side API key (from the Certifaction
web app) or an OIDC access token. See `authentication/certifaction-authentication.yml`.

## Steps
1. Confirm the account with `get_user` (`GET /user`) — verifies credentials and
   returns account data.
2. (Optional) `prepare_file` (`POST /prepare`) — prepare the PDF for signing,
   choosing the `prepare_scope` (`sign` or `attachment`) and signature placement
   (`page`, `position-x`, `position-y`).
3. `sign_file` (`POST /sign`) — sign the prepared file. Choose the `legal-weight`
   / signature level (SES, AES, or QES per jurisdiction).

## Conventions & errors
- Errors are plain HTTP status codes with a description (see
  `errors/certifaction-problem-types.yml`): 401 = bad key, 403 = missing role,
  400 = malformed request.
- There is no idempotency key; do not blindly retry a `sign_file` that may have
  succeeded — re-check with the document status flow first.

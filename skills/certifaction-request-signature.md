---
name: Request signatures and track them with Certifaction
description: Send a document for signature to one or more signers, track status, and handle the completion webhook.
api: openapi/certifaction-local-api-openapi.yml
operations: [request_signature, request_status, file_requests_status, list_requests, cancel_request, cancel_request_all]
generated: '2026-07-18'
method: generated
---

# Request signatures and track them with Certifaction

Drive the Certifaction Local API to request signatures from others and follow the
request to completion.

## Auth
`Authorization` header with an API key or OIDC access token
(`authentication/certifaction-authentication.yml`).

## Steps
1. `request_signature` (`POST /request/create`) — create a signature request.
   Supply signer details (`email`, `first-name`, `last-name`, `mobile-phone`),
   optional `message`, an optional `transaction-id` for your own correlation, and
   an optional URL-encoded `webhook-url` for a completion callback.
2. `request_status` (`GET /request/status`) — check the status of a single
   signer's request; or `file_requests_status` (`GET /request/file/status`) for
   all requests on a file.
3. `list_requests` (`POST /request/list`) — list the signature requests on a file.
4. To abort: `cancel_request` (`POST /request/cancel`) for one signer, or
   `cancel_request_all` (`POST /request/cancel/all`) for the whole file.

## Webhook
On completion Certifaction POSTs (empty body) to your `webhook-url`. If an
account-level secret is configured, verify the `authorization: Bearer <secret>`
header. See `asyncapi/certifaction-webhooks.yml`.

## Conventions & errors
- `transaction-id` is a correlation id, not an idempotency key.
- Errors are plain HTTP status codes (`errors/certifaction-problem-types.yml`).

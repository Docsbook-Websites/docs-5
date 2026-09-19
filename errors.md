---
title: "Errors"
description: "Understand what the docs API returns when a call fails, which failures are worth retrying, and how to log them usefully."
status: generated
version: "0.1"
---

# Errors

A failed call to docs answers with an HTTP status code and a body describing what went wrong. Read both: the status says what class of problem it is, the body says which field or resource caused it.

## Status codes

| Status | Meaning | What to do |
| --- | --- | --- |
| `400` | The request was malformed. | Fix the request; retrying changes nothing. |
| `401` | No valid token was present. | Check the header, then the token itself. |
| `403` | The token is valid but not allowed here. | Ask for access rather than retrying. |
| `404` | Nothing exists at that path or identifier. | Confirm the id and the base URL. |
| `409` | The change conflicts with the current state. | Re-read the resource and decide again. |
| `422` | The shape was right, the values were not. | Correct the fields named in the body. |
| `429` | Too many requests. | Back off, then retry. |
| `5xx` | Something failed on our side. | Retry with backoff; report it if it persists. |

## The error body

```json
{
  "error": {
    "code": "invalid_field",
    "message": "name must be at least one character",
    "field": "name"
  }
}
```

Put a machine-readable `code` next to the human `message` and keep the codes stable. Callers branch on the code; they should never have to match on the wording of a sentence you might improve next month. If docs returns a different shape, edit the example above rather than leaving both in a reader's head.

## Retrying safely

Reads can be retried freely. Writes can be retried when they are idempotent — the same request twice leaving the same result. Say here how docs handles a repeated write, because a caller who does not know will either retry and double-charge something or fail to retry and lose the request.

Exponential backoff with a little jitter is the safe default: wait a second, then two, then four, and give up rather than hammering a service that is already struggling.

## Next steps

- [Endpoints](reference/endpoints.md) — errors specific to a route.
- [Quickstart](guides/quickstart.md) — a call with error handling in it.
- [Authentication](authentication.md) — the usual cause of a 401.

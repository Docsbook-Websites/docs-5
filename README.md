---
title: "docs API"
description: "Call the docs API with confidence — authenticate, make a first request, look up any endpoint and understand the errors you get back."
status: generated
version: "0.1"
---

# docs API

These pages cover what you need to talk to docs over HTTP: how a request is authenticated, what each endpoint does, and what the API tells you when something goes wrong. They are published at https://docsbook.io/Docsbook-websites/docs-5.

## Your first request

Every call carries a bearer token issued from your docs dashboard, and responses come back as JSON unless a page here says otherwise.

```bash
curl https://api.example.com/v1/items \
  -H "Authorization: Bearer $API_TOKEN" \
  -H "Accept: application/json"
```

Swap `api.example.com` for the base URL shown in your dashboard, and `API_TOKEN` for a token you created there. If that call answers, the rest of this documentation is variations on it: a different path, a different method, a body.

## What is on these pages

[Authentication](authentication.md) explains where tokens come from and how to keep them out of a repository. [Quickstart](guides/quickstart.md) walks the first call end to end, including the part where it fails. [Endpoints](reference/endpoints.md) is the table to keep open in a second tab. [Errors](errors.md) covers status codes, the error body and what is worth retrying.

## Conventions

Rules that hold across every endpoint belong here, stated once, so the reference pages never repeat them: how the version in the path is pinned, how long lists are paged, which timezone timestamps use, what an identifier looks like. Readers assume anything left unstated, and they tend to assume wrong — a caller who guesses your pagination writes a loop that quietly stops at the first page.

Write the rules down in the order a caller meets them, not in the order you built them.

## Next steps

- [Quickstart](guides/quickstart.md) — a working call in a few minutes.
- [Authentication](authentication.md) — get a token and send it correctly.
- [Endpoints](reference/endpoints.md) — every route in one table.

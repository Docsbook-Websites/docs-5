---
title: "Endpoints"
description: "Look up any docs endpoint in one table — the method, the path, what it does and whether the call needs a token."
status: generated
version: "0.1"
---

# Endpoints

One row per route, so a reader finds the call they need without opening five pages. The rows below show the shape of the table; replace each one with a real docs route before you publish.

| Method | Path | What it does | Auth |
| --- | --- | --- | --- |
| `GET` | `/v1/items` | Lists items, newest first, one page at a time. | Bearer |
| `POST` | `/v1/items` | Creates an item from the JSON body and returns it. | Bearer |
| `GET` | `/v1/items/:id` | Returns a single item by its identifier. | Bearer |
| `PATCH` | `/v1/items/:id` | Updates only the fields present in the body. | Bearer |
| `DELETE` | `/v1/items/:id` | Removes the item and returns no content. | Bearer |
| `GET` | `/v1/health` | Reports whether the API is accepting traffic. | None |

Paths are relative to your base URL. A reader who can see the method, the path and the auth in one glance can decide whether the route is the one they want before reading a word of prose.

## Giving an endpoint its own section

Anything that needs more than a row gets a section underneath: the parameters it accepts, one example request, one example response, and the errors that are specific to it.

### GET /v1/items

```bash
curl "https://api.example.com/v1/items?limit=2" \
  -H "Authorization: Bearer $API_TOKEN"
```

```json
{
  "data": [
    { "id": "itm_28", "name": "Second item", "created_at": "2026-04-02T09:31:00Z" },
    { "id": "itm_27", "name": "First item", "created_at": "2026-04-01T17:02:00Z" }
  ],
  "next_cursor": "itm_27"
}
```

Copy a real response out of your own API rather than hand-writing one — hand-written examples drift from the implementation, and a caller who codes against a drifted example blames the API. Every field in the example deserves a line saying what it means and when it is absent.

## Next steps

- [Authentication](../authentication.md) — the header every row above assumes.
- [Errors](../errors.md) — what comes back when a call is rejected.
- [Quickstart](../guides/quickstart.md) — these routes in a working script.

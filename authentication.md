---
title: "Authentication"
description: "Authenticate every docs API request with a bearer token, keep that token out of your source tree, and rotate it without downtime."
status: generated
version: "0.1"
---

# Authentication

docs identifies a caller by the token on the request. A call without one, or with a token that has been revoked, never reaches your data.

## Send the token

Put it in an `Authorization` header on every request.

```bash
curl https://api.example.com/v1/items \
  -H "Authorization: Bearer $API_TOKEN"
```

The same header from JavaScript:

```js
const res = await fetch("https://api.example.com/v1/items", {
  headers: { Authorization: "Bearer " + process.env.API_TOKEN },
})
const items = await res.json()
```

And from Python:

```python
import os
import requests

res = requests.get(
    "https://api.example.com/v1/items",
    headers={"Authorization": "Bearer " + os.environ["API_TOKEN"]},
)
res.raise_for_status()
```

## Where tokens come from

Tokens are issued from your docs dashboard. Create one per integration rather than sharing a single token everywhere: when something has to be revoked, you want to cut off one caller, not all of them at once.

## Keep tokens out of the repository

Read the token from an environment variable or a secret manager, never from a checked-in file. Anything shipped to a browser or a mobile app is public no matter how it is obfuscated, so calls that need a token belong on a server you control. A token that has been committed is a token that has to be rotated, even if the repository is private.

## Expiry, scope and rotation

If docs tokens expire, or carry scopes that limit what they reach, write the rule in this section. It is the first thing an integrator looks for and the thing support ends up answering by hand when it is missing. Say what a caller sees when a token goes stale, too — a `401` and a clear message is a support ticket avoided.

## Next steps

- [Quickstart](guides/quickstart.md) — put the token to work on a real call.
- [Endpoints](reference/endpoints.md) — which routes need which access.
- [Errors](errors.md) — what an authentication failure looks like.

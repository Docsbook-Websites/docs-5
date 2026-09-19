---
title: "Quickstart"
description: "Make your first successful call to the docs API in a few minutes, then create something and read the response back."
status: generated
version: "0.1"
---

# Quickstart

By the end of this page you will have called the docs API twice: once to read, once to write. Nothing here needs a framework, only a terminal.

## 1. Get a token

Create an API token in your docs dashboard and keep it somewhere your shell can reach it. Treat it like a password — it acts as you.

```bash
export API_TOKEN="paste-your-token-here"
```

## 2. Read something

```bash
curl "https://api.example.com/v1/items?limit=1" \
  -H "Authorization: Bearer $API_TOKEN"
```

A `200` with a JSON body means the token, the base URL and the path all line up. A `401` means the header did not arrive as expected — check for a missing `Bearer ` prefix before you suspect the token itself.

## 3. Create something

```bash
curl -X POST https://api.example.com/v1/items \
  -H "Authorization: Bearer $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name":"My first item"}'
```

The response carries the created record, including the identifier the server assigned. Keep that identifier: it is what the read, update and delete routes take.

Two things are worth checking before you move on. A successful create often answers with a 201 rather than a 200, so code that tests for equality with 200 will reject its own successful write. And when a body is rejected, the error names the field that caused it — read that before changing the request at random.

## 4. Do it from code

```js
const res = await fetch("https://api.example.com/v1/items", {
  method: "POST",
  headers: {
    Authorization: "Bearer " + process.env.API_TOKEN,
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ name: "My first item" }),
})

if (!res.ok) throw new Error("Request failed with status " + res.status)
console.log(await res.json())
```

That `res.ok` check is the line most first integrations forget. A failed call still returns a body, and parsing it as if it succeeded turns a clear error into a confusing one three functions later.

## Next steps

- [Endpoints](../reference/endpoints.md) — everything else you can call.
- [Errors](../errors.md) — how to handle the calls that fail.
- [Authentication](../authentication.md) — tokens, scope and rotation.

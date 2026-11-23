# Find content

> What you already made, newest first, with the ids the other tools take.

| | |
|---|---|
| MCP tool | `find_content` |
| REST route | `GET /api/v1/agent/content` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

What this account already made, newest first: id, kind, title, brand and date.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `kind` | string | No | article, post, email, listing or ad; omitted, all. |
| `limit` | integer | No | Up to 50; default 20. |

## Example

An agent calls `find_content` with these arguments:

```json
{}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/content" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "items": [
    {
      "id": "gen_a7c2f0",
      "kind": "article",
      "title": "How to choose a coffee grinder for home",
      "brand_id": "bv_3c9d0e",
      "created_at": "2026-11-23T10:02:00+00:00"
    }
  ]
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/find-content/

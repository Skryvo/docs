# List brands

> Your brands and which one is the default.

| | |
|---|---|
| MCP tool | `list_brands` |
| REST route | `GET /api/v1/agent/brands` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

The person's brands: id, name and whether it is the default. In a team workspace an editor also sees whether a brand's posts wait for approval.

## Inputs

None.

## Example

An agent calls `list_brands` with these arguments:

```json
{}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/brands" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "brands": [
    {
      "id": "bv_3c9d0e",
      "name": "Northside Coffee",
      "is_default": true
    }
  ]
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/list-brands/

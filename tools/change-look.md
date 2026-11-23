# Change the look

> Designs your look again bolder, calmer, closer to your site or with another photo, or keeps the one on show.

| | |
|---|---|
| MCP tool | `change_look` |
| REST route | `POST /api/v1/agent/design/look` |
| Changes anything | Yes. An agent asks the person before it calls it. |
| Cost | Free, up to two new designs of the look. |

## What it does

`design` draws a brand's first three posts; `closer` (to its website), `bolder`, `calmer` or `photo` (another of its photos) draw them again, at most twice and free; `keep` makes the look on show the one every new picture wears. A design takes about two minutes and shows in the brand's design once it lands. Admins and owners only.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `change` | string | Yes | design, closer, bolder, calmer, photo or keep. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |

## Example

An agent calls `change_look` with these arguments:

```json
{
  "change": "bolder",
  "brand_id": "bv_3c9d0e"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/design/look" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "change": "bolder",
  "brand_id": "bv_3c9d0e"
}'
```

The reply:

```json
{
  "look": {
    "state": "making",
    "round": 1,
    "verb": "",
    "direction": "",
    "design": null,
    "drawn": {},
    "left": 1,
    "cost": 0,
    "kept": false,
    "posts": []
  }
}
```

## What it costs

Free, up to two new designs of the look. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/change-look/

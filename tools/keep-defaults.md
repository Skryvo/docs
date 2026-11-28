# Keep as defaults

> Keeps your choices as the brand's defaults, after you say yes. Inputs, an example and the cost of keep_defaults for agents and the API.

| | |
|---|---|
| MCP tool | `keep_defaults` |
| REST route | `POST /api/v1/agent/defaults` |
| Changes anything | Yes. An agent asks the person before it calls it. |
| Cost | Free. |

## What it does

Saves the person's choices as a brand's defaults, so later posts or articles use them without asking. `kind` post keeps platforms, tone, pictures, hashtags and call_to_action; article keeps word_count, tone, writing_style, cover_picture and inside_pictures. When a summary lists `differs_from_brand`, offer once to keep those and call only after the person says yes. Admins and owners only.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `kind` | string | Yes | post or article. |
| `settings` | object | Yes | The values to keep. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |

## Example

An agent calls `keep_defaults` with these arguments:

```json
{
  "kind": "post",
  "settings": {
    "tone": "friendly"
  },
  "brand_id": "bv_3c9d0e"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/defaults" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "kind": "post",
  "settings": {
    "tone": "friendly"
  },
  "brand_id": "bv_3c9d0e"
}'
```

The reply:

```json
{
  "brand_id": "bv_3c9d0e",
  "kind": "post",
  "saved": {
    "tone": "friendly"
  }
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/keep-defaults/

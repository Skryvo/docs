# Brand design

> Your brand's logo, colours and fonts, and the look every new post is designed in.

| | |
|---|---|
| MCP tool | `brand_design` |
| REST route | `GET /api/v1/agent/design` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

A brand's design as data: logo, colour roles, fonts, the look its pictures keep (three designed posts every new picture follows, the changes left and whether it is kept) and what would make its designs better.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |

## Example

An agent calls `brand_design` with these arguments:

```json
{}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/design" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "brand_id": "bv_3c9d0e",
  "name": "Northside Coffee",
  "logo_url": "https://media.skryvo.ai/brands/b1/logo.png",
  "colours": {
    "primary": "#1F3A2E",
    "accent": "#E8A33D",
    "surface": "#FAF6EF"
  },
  "fonts": {
    "heading": "Fraunces",
    "body": "Inter"
  },
  "look": {
    "state": "done",
    "round": 1,
    "verb": "",
    "direction": "",
    "design": null,
    "drawn": {},
    "left": 1,
    "cost": 0,
    "kept": true,
    "posts": [
      {
        "kind": "quote",
        "url": "https://media.skryvo.ai/looks/b1/post-1.jpg",
        "line": "Good coffee, close to home",
        "round": 1,
        "photo": true
      }
    ]
  },
  "readiness": {
    "logo": true,
    "colours": 3,
    "fonts": true,
    "shots": [
      {
        "key": "counter",
        "label": "Your counter",
        "tip": "In daylight",
        "have": true
      }
    ]
  },
  "changes": [
    "closer",
    "bolder",
    "calmer",
    "photo"
  ]
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/brand-design/

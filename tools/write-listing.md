# Write a product listing

> Writes a product listing shaped for its marketplace's rules. Inputs, an example and the cost of write_listing for agents and the API.

| | |
|---|---|
| MCP tool | `write_listing` |
| REST route | `POST /api/v1/agent/listings` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | One generation. |

## What it does

Writes a product listing in the brand's voice, shaped for its marketplace's rules: a title and the marketplace's own fields in `listing`. `features` takes one to ten key features. When `marketplace` was left out, the call writes nothing and returns `status: confirm` first. One generation.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `product` | string | Yes | What is advertised or listed. |
| `features` | string[] | Yes | 1 to 10 key features. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |
| `marketplace` | string | No | amazon, shopify, etsy, ebay, walmart, tiktok_shop, google_shopping, woocommerce, saas or landing_page. |
| `tone` | string | No | Omitted, the brand's tone. |
| `audience` | string | No | Who it is for. |
| `language` | string | No | A language code; omitted, the brand's writing language. |
| `overview` | string | No | The seller's own words. |
| `price` | number | No | The price. |
| `keywords` | string | No | Search terms. |
| `confirmed` | boolean | No | true once the person approved the summary. |

## Example

An agent calls `write_listing` with these arguments:

```json
{
  "product": "House Blend 1 kg",
  "features": [
    "Roasted weekly",
    "Medium roast",
    "Whole beans"
  ],
  "marketplace": "shopify",
  "confirmed": true
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/listings" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "product": "House Blend 1 kg",
  "features": [
    "Roasted weekly",
    "Medium roast",
    "Whole beans"
  ],
  "marketplace": "shopify",
  "confirmed": true
}'
```

The reply:

```json
{
  "status": "written",
  "brand_id": "bv_3c9d0e",
  "generation_id": "gen_l1st1n",
  "title": "Northside House Blend, 1 kg whole beans",
  "listing": {
    "title": "Northside House Blend, 1 kg whole beans",
    "description": "A balanced medium roast…",
    "bullet_points": [
      "Roasted weekly in Leeds"
    ]
  },
  "settings": [
    {
      "field": "platform",
      "value": "shopify",
      "from": "you"
    }
  ]
}
```

## What it costs

One generation. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/write-listing/

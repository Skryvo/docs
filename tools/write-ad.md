# Write ad copy

> Writes ad copy in the brand's voice, shaped for each ad platform. No ad is run.

| | |
|---|---|
| MCP tool | `write_ad` |
| REST route | `POST /api/v1/agent/ads` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | One generation. |

## What it does

Writes ad copy in the brand's voice, shaped to each ad platform's limits. `platforms` names ad platforms; a wrong one's refusal lists them all. `variations` is 1 to 6. One generation. No ad is created or run anywhere.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `product` | string | Yes | What is advertised or listed. |
| `platforms` | string[] | Yes | Ad platforms, such as google_ads or meta_ads. |
| `what_it_is` | string | No | What the product is. |
| `benefits` | string[] | No | Up to five. |
| `goal` | string | No | awareness, consideration or conversion; default conversion. |
| `link` | string | No | The landing page. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |
| `language` | string | No | A language code; omitted, the brand's writing language. |
| `variations` | integer | No | 1 to 6; default 3. |

## Example

An agent calls `write_ad` with these arguments:

```json
{
  "product": "House Blend 1 kg",
  "platforms": [
    "google_ads"
  ],
  "benefits": [
    "Roasted weekly"
  ],
  "link": "https://northside.coffee/shop"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/ads" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "product": "House Blend 1 kg",
  "platforms": [
    "google_ads"
  ],
  "benefits": [
    "Roasted weekly"
  ],
  "link": "https://northside.coffee/shop"
}'
```

The reply:

```json
{
  "generation_id": "gen_ad0c0p",
  "platforms": {
    "google_ads": {
      "platform": "google_ads",
      "label": "Google Ads",
      "variations": [
        {
          "angle": "freshness",
          "angle_label": "Freshness",
          "angle_reason": "Roasted weekly is the brief's strongest proof.",
          "assets": {
            "headlines": [
              {
                "text": "Roasted This Week",
                "chars": 17
              }
            ]
          },
          "cta": "Shop now"
        }
      ],
      "limits": [
        {
          "key": "headlines",
          "label": "Headline",
          "max_chars": 30,
          "recommended_chars": 25,
          "serves_count": 3
        }
      ]
    }
  }
}
```

## What it costs

One generation. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/write-ad/

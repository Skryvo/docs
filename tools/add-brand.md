# Add a brand

> Adds a brand and reads its voice, kit and facts from its website, using one voice training.

| | |
|---|---|
| MCP tool | `add_brand` |
| REST route | `POST /api/v1/agent/brands` |
| Changes anything | Yes. An agent asks the person before it calls it. |
| Cost | One of the month's voice trainings. The plan sets how many brands an account holds. |

## What it does

Adds a brand and reads its voice, colours, fonts, logo and facts from its website. It runs in the background for a few minutes, then the brand appears in the list. Uses one of the month's brand readings; plans limit how many brands an account holds.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `name` | string | Yes | The brand's name. |
| `website` | string | Yes | Its website address. |

## Example

An agent calls `add_brand` with these arguments:

```json
{
  "name": "Northside Coffee",
  "website": "https://northside.coffee"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/brands" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "name": "Northside Coffee",
  "website": "https://northside.coffee"
}'
```

The reply, HTTP 202:

```json
{
  "id": "bv_7a1f22",
  "name": "Northside Coffee",
  "status": "reading the site"
}
```

## What it costs

One of the month's voice trainings. The plan sets how many brands an account holds. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/add-brand/

# Balance

> Says what your plan still allows this month.

| | |
|---|---|
| MCP tool | `balance` |
| REST route | `GET /api/v1/agent/balance` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

Generations and picture credits left this month, article plans left, when a trial ends, and how many articles, post batches and post pictures that covers. Check it before a large request.

## Inputs

None.

## Example

An agent calls `balance` with these arguments:

```json
{}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/balance" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "plan": "pro",
  "access": "active",
  "trial_ends_at": null,
  "left": {
    "generations": 41,
    "image_credits": 180,
    "resets_at": "2026-12-01T00:00:00+00:00"
  },
  "article_plans_left": 18,
  "enough_for": {
    "articles": 13,
    "post_batches": 41,
    "post_pictures": 45
  }
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/balance/

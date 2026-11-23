# Post results

> Reach and engagement, best posting times and top posts for the days you ask about.

| | |
|---|---|
| MCP tool | `post_results` |
| REST route | `GET /api/v1/agent/results` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

The last 7, 30 or 90 days of published posts: totals against the period before, reach, engagements and clicks per channel, the best times to post, what stood out and the top ten posts.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `days` | integer | No | 7, 30 or 90; default 30. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |

## Example

An agent calls `post_results` with these arguments:

```json
{}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/results" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "days": 30,
  "as_of": "2026-11-23T06:00:00+00:00",
  "totals": {
    "posts": 24,
    "measured": 22,
    "unmeasured": 0,
    "reach": 18200,
    "engagements": 640,
    "clicks": 120,
    "rate": 0.0352
  },
  "previous_totals": {
    "posts": 20,
    "measured": 20,
    "unmeasured": 0,
    "reach": 15100,
    "engagements": 480,
    "clicks": 90,
    "rate": 0.0318
  },
  "channels": [
    {
      "platform": "linkedin",
      "access": "ok",
      "posts": 12,
      "measured": 12,
      "unmeasured": 0,
      "reach": 11000,
      "engagements": 420,
      "clicks": 80,
      "rate": 0.0382
    }
  ],
  "best_times": [
    {
      "platform": "linkedin",
      "time": "09:00",
      "rate": 0.051,
      "lift": 0.34,
      "posts": 5,
      "of": 12
    }
  ],
  "findings": [
    {
      "kind": "hook",
      "text": "Posts that open with a question get 40% more engagement than your other posts.",
      "lift": 0.4,
      "sample": "6 posts vs 16 others · 30 days",
      "postIds": [
        "pub_1a2b"
      ],
      "action": {
        "type": "write_like",
        "hint": "open with a question"
      }
    }
  ],
  "top_posts": []
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/post-results/

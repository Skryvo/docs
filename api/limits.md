# API rate limits and plan limits

> How many calls a key may make, the limits on a single call, and what each plan allows a month.

## Rate limit

Each key or sign-in may make 60 requests a minute and 1,000 an hour. Past that, the API answers 429:

```text
HTTP/1.1 429 Too Many Requests
Retry-After: 12
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 12
```

Wait the seconds in `Retry-After` before the next call.

## Limits on one call

| Limit | Value |
|---|---|
| API keys per person | 10 |
| Platforms in one `write_post` | 4 |
| A post's topic | 3 to 200 characters |
| Plan rows in one `accept_plan` | 100 |
| A video from `add_video` | MP4 or MOV, up to 1 GB |

## What a plan allows a month

The API spends the same allowance as the app. Prices and the trial are on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/); [`balance`](https://skryvo.ai/docs/tools/balance/) says what is left.

| | Hobby | Pro | Enterprise |
|---|---|---|---|
| Generations | 150 | 500 | 5,000 |
| Image credits | 75 | 300 | 3,000 |
| Brands | 2 | 5 | 10 |
| Scheduled posts waiting at once | 20 | 100 | Unlimited |
| X posts | 30 | 100 | 1,500 |
| Article imports | 50 | 200 | 500 |

A post batch from `write_post` uses one generation; a researched article uses 2. On X, a post with a link counts as 10.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/api/limits/

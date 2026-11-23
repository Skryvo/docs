# Article SEO

> Checks an article's SEO for free: score, search phrase and every issue the editor's SEO card shows.

| | |
|---|---|
| MCP tool | `article_seo` |
| REST route | `GET /api/v1/agent/articles/{article_id}/seo` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

A free SEO check: score out of 100, the search phrase it aims at and each issue found (phrase missing from the title, no meta description, no links to sources, heading structure), the improvements on offer and whether the next one is free.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `article_id` | string | Yes | An article id, or its generation id. |

## Example

An agent calls `article_seo` with these arguments:

```json
{
  "article_id": "<article_id>"
}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/articles/$ARTICLE_ID/seo" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "article_id": "gen_a7c2f0",
  "score": 74,
  "keyword": "best coffee grinder for home",
  "issues": [
    "Missing meta description (need 155-160 characters with keyword)"
  ],
  "improvements": [
    "accuracy",
    "geo_citations",
    "seo"
  ],
  "next_improvement_free": true,
  "left": {
    "generations": 41,
    "image_credits": 180,
    "resets_at": "2026-12-01T00:00:00+00:00"
  }
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/article-seo/

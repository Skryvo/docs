# Article results

> Shows where a published article went and how it does, with its Google search numbers.

| | |
|---|---|
| MCP tool | `article_results` |
| REST route | `GET /api/v1/agent/articles/{article_id}/results` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

Every place an article went out, each with its link, reach, engagements and clicks, and its search clicks, impressions, click rate and position when the person connected their search console. Takes the article's id or its generation id.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `article_id` | string | Yes | An article id, or its generation id. |

## Example

An agent calls `article_results` with these arguments:

```json
{
  "article_id": "<article_id>"
}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/articles/$ARTICLE_ID/results" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "article_id": "gen_a7c2f0",
  "title": "How to choose a coffee grinder for home",
  "places": [
    {
      "platform": "wordpress",
      "url": "https://northside.coffee/blog/grinder",
      "published_at": "2026-11-25T08:00:00+00:00",
      "removed": false,
      "reach": 1240,
      "reach_kind": "views",
      "engagements": 31,
      "clicks": 12,
      "search": {
        "clicks": 40,
        "impressions": 1900,
        "ctr": 0.021,
        "position": 8.4
      },
      "read_at": "2026-12-02T06:00:00+00:00"
    }
  ],
  "open_in_skryvo": "https://app.skryvo.ai/generate/blog/gen_a7c2f0"
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/article-results/

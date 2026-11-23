# Article status

> Says where an article is, and hands back the finished text with its score and every checked claim with its sources.

| | |
|---|---|
| MCP tool | `article_status` |
| REST route | `GET /api/v1/agent/articles/{article_id}` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

Where an article is: `writing` with its stage, `failed` with why (and that it was not charged), or `done` with its title, word count, score out of 100, markdown, every claim the fact check read and a link that opens it in Skryvo. Check about once a minute while it writes.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `article_id` | string | Yes | An article id, or its generation id. |

## Example

An agent calls `article_status` with these arguments:

```json
{
  "article_id": "<article_id>"
}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/articles/$ARTICLE_ID" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "article_id": "pl_91ab3e",
  "status": "done",
  "generation_id": "gen_a7c2f0",
  "title": "How to choose a coffee grinder for home",
  "words": 1512,
  "score": 88,
  "markdown": "# How to choose a coffee grinder for home\n\n…",
  "complete": true,
  "claims": {
    "checked": 9,
    "verified": 9,
    "by_verdict": {
      "verified": 9
    },
    "items": [
      {
        "claim": "Burr grinders give a more even grind.",
        "verdict": "verified",
        "why": "Two sources measure the spread of particle sizes.",
        "sources": [
          "https://example.org/grind"
        ]
      }
    ]
  },
  "open_in_skryvo": "https://app.skryvo.ai/generate/blog/gen_a7c2f0"
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/article-status/

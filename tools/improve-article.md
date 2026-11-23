# Improve an article

> Fixes those issues, adds an FAQ citing its sources or rewrites only disputed sentences, saved as a new version.

| | |
|---|---|
| MCP tool | `improve_article` |
| REST route | `POST /api/v1/agent/articles/{article_id}/improve` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | An article's first improvement is free; each one after costs one generation. |

## What it does

Improves an article and saves it as a new version; the earlier one stays in its history. `seo` fixes every issue the SEO check found; `geo_citations` adds questions and answers that cite the article's own sources; `accuracy` rewrites only the sentences the fact check disputed. An article's first improvement is free, each after costs one generation. About a minute.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `article_id` | string | Yes | An article id, or its generation id. |
| `goal` | string | No | seo, geo_citations or accuracy; default seo. |

## Example

An agent calls `improve_article` with these arguments:

```json
{
  "article_id": "<article_id>",
  "goal": "seo"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/articles/$ARTICLE_ID/improve" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "goal": "seo"
}'
```

The reply:

```json
{
  "article_id": "gen_a7c2f0",
  "goal": "seo",
  "score_before": 74,
  "score_after": 91,
  "changes": [
    "Added a meta description with the search phrase"
  ],
  "remaining_issues": [],
  "saved_as_version": 2,
  "charged": false,
  "open_in_skryvo": "https://app.skryvo.ai/generate/blog/gen_a7c2f0"
}
```

## What it costs

An article's first improvement is free; each one after costs one generation. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/improve-article/

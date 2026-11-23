# Write an article

> Writes the planned article in the background, researched, fact-checked and scored as in the app.

| | |
|---|---|
| MCP tool | `write_article` |
| REST route | `POST /api/v1/agent/articles` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | 2 generations, plus image credits for its pictures. A failed article is not charged. |

## What it does

Writes the planned article in the background, about four minutes: researched, fact-checked and scored, the same article the app writes. Pass the person's chosen `headline`, their `answers` to the plan's questions and any `notes`. Tone, audience and point of view can change here; a new length, style or language needs a new plan. A failed article is not charged. Poll `GET /articles/{article_id}` or subscribe to `article.ready` and `article.failed`. Nothing is published.
[`article_status`](https://skryvo.ai/docs/tools/article-status/) reports it while it writes and hands back the finished text.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `plan_id` | string | Yes | A plan from plan_article. |
| `headline` | string | No | The person's chosen headline. |
| `answers` | string[] | No | [{question, answer}] for the plan's questions. |
| `notes` | string | No | Anything else for the writer. |
| `pictures` | boolean | No | false for none, true for a cover. |
| `inside_pictures` | integer | No | 0 to 3 more inside the article. |
| `tone` | string | No | Omitted, the brand's tone. |
| `audience` | string | No | Who it is for. |
| `point_of_view` | string | No | The point of view to write in. |
| `length` | integer | No | A new length needs a new plan. |
| `style` | string | No | A new style needs a new plan. |
| `language` | string | No | A new language needs a new plan. |

## Example

An agent calls `write_article` with these arguments:

```json
{
  "plan_id": "pl_91ab3e",
  "headline": "How to choose a coffee grinder for home",
  "answers": [
    {
      "question": "Which grinder do you use behind your own counter?",
      "answer": "A flat-burr grinder we have had for six years."
    }
  ]
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/articles" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "plan_id": "pl_91ab3e",
  "headline": "How to choose a coffee grinder for home",
  "answers": [
    {
      "question": "Which grinder do you use behind your own counter?",
      "answer": "A flat-burr grinder we have had for six years."
    }
  ]
}'
```

The reply, HTTP 202:

```json
{
  "article_id": "pl_91ab3e",
  "status": "writing",
  "minutes": 4,
  "settings": [
    {
      "field": "word_count",
      "value": 1500
    }
  ]
}
```

## What it costs

2 generations, plus image credits for its pictures. A failed article is not charged. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/write-article/

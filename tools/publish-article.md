# Publish an article

> Schedules a finished article to a connected blog, or sends it there as a draft.

| | |
|---|---|
| MCP tool | `publish_article` |
| REST route | `POST /api/v1/agent/articles/{article_id}/publish` |
| Changes anything | Yes. An agent asks the person before it calls it. |
| Cost | Free. |

## What it does

Schedules a finished article to a blog channel; Skryvo publishes it with its pictures, headings and search fields and reads it back to confirm it is live. `at` moves to the next quarter hour; omitted, about five minutes from now. `as_draft: true` sends it to the blog now as a draft to review there and returns its edit link instead. `original_url` names the article's first home so a copy credits it.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `article_id` | string | Yes | An article id, or its generation id. |
| `channel_id` | string | Yes | A blog channel from list_channels. |
| `at` | string | No | ISO 8601 time, moved to the next quarter hour. |
| `as_draft` | boolean | No | true sends it to the blog now as a draft. |
| `original_url` | string | No | Where the article first lives. |

## Example

An agent calls `publish_article` with these arguments:

```json
{
  "article_id": "<article_id>",
  "channel_id": "conn_wp41c0",
  "at": "2026-11-25T08:00:00+00:00"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/articles/$ARTICLE_ID/publish" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "channel_id": "conn_wp41c0",
  "at": "2026-11-25T08:00:00+00:00"
}'
```

The reply, HTTP 201:

```json
{
  "post": {
    "id": "c1a2b3c4d5",
    "platform": "wordpress",
    "channel_id": "conn_8f2e1a",
    "date": "2026-11-24",
    "time": "09:00",
    "status": "scheduled",
    "reason": null,
    "awaiting_approval": false,
    "reviewer_approval": null,
    "auto_publish": true,
    "text": null,
    "topic": "Grinder guide",
    "written": true,
    "publish_error": null,
    "posted_url": null,
    "open_in_skryvo": "https://app.skryvo.ai/calendar?date=2026-11-24"
  }
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/publish-article/

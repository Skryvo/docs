# Change a post

> Moves a scheduled post that has not gone out, changes its words, or both.

| | |
|---|---|
| MCP tool | `change_post` |
| REST route | `PATCH /api/v1/agent/posts/{id}` |
| Changes anything | Yes. An agent asks the person before it calls it. |
| Cost | Free. |

## What it does

Moves a post that has not gone out, changes its words, or both. `at` moves to the next quarter hour; `text` replaces the post's words on its platform.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `post_id` | string | Yes | A post id from list_scheduled_posts. |
| `at` | string | No | ISO 8601 time, moved to the next quarter hour. |
| `text` | string | No | The post's new words. |

## Example

An agent calls `change_post` with these arguments:

```json
{
  "post_id": "<post_id>",
  "at": "2026-11-24T10:15:00+00:00"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X PATCH "https://api.skryvo.ai/api/v1/agent/posts/$POST_ID" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "at": "2026-11-24T10:15:00+00:00"
}'
```

The reply:

```json
{
  "id": "c1a2b3c4d5",
  "platform": "linkedin",
  "channel_id": "conn_8f2e1a",
  "date": "2026-11-24",
  "time": "10:15",
  "status": "scheduled",
  "reason": null,
  "awaiting_approval": false,
  "reviewer_approval": null,
  "auto_publish": true,
  "text": "We just opened our new studio in Leeds. Come say hello this Saturday.",
  "topic": "New studio opening",
  "written": true,
  "publish_error": null,
  "posted_url": null,
  "open_in_skryvo": "https://app.skryvo.ai/calendar?date=2026-11-24"
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/change-post/

# List scheduled posts

> Upcoming and recent posts with their status and any publishing problem.

| | |
|---|---|
| MCP tool | `list_scheduled_posts` |
| REST route | `GET /api/v1/agent/posts` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

Social posts from yesterday to `days` ahead, with status and any publish error. A post with `written: false` is a planned topic Skryvo writes before its time.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `days` | integer | No | How far ahead, up to 90; default 30. |

## Example

An agent calls `list_scheduled_posts` with these arguments:

```json
{}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/posts" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "posts": [
    {
      "id": "c1a2b3c4d5",
      "platform": "linkedin",
      "channel_id": "conn_8f2e1a",
      "date": "2026-11-24",
      "time": "09:00",
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
  ]
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/list-scheduled-posts/

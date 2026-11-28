# Review a post

> Records your decision on a team post waiting for approval. Inputs, an example and the cost of review_post for agents and the API.

| | |
|---|---|
| MCP tool | `review_post` |
| REST route | `POST /api/v1/agent/posts/{id}/review` |
| Changes anything | Yes. An agent asks the person before it calls it. |
| Cost | Free. |

## What it does

The person's decision on a team post waiting for approval: `approve: true` lets it go out at its time; `false` sends it back with `note` saying what should change. Only reviewers, admins and owners can decide.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `post_id` | string | Yes | A post id from list_scheduled_posts. |
| `approve` | boolean | Yes | true lets it go out; false sends it back. |
| `note` | string | No | What should change; needed when sending back. |

## Example

An agent calls `review_post` with these arguments:

```json
{
  "post_id": "<post_id>",
  "approve": false,
  "note": "Mention the opening hours."
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/posts/$POST_ID/review" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "approve": false,
  "note": "Mention the opening hours."
}'
```

The reply:

```json
{
  "id": "c1a2b3c4d5",
  "platform": "linkedin",
  "channel_id": "conn_8f2e1a",
  "date": "2026-11-24",
  "time": "09:00",
  "status": "scheduled",
  "reason": null,
  "awaiting_approval": false,
  "reviewer_approval": "approved",
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

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/review-post/

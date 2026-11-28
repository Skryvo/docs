# Cancel a post

> Removes a scheduled post before it goes out. Inputs, an example and the cost of cancel_post for agents and the API.

| | |
|---|---|
| MCP tool | `cancel_post` |
| REST route | `DELETE /api/v1/agent/posts/{id}` |
| Changes anything | Yes. An agent asks the person before it calls it. |
| Cost | Free. |

## What it does

Removes a scheduled post before it goes out. Returns no body.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `post_id` | string | Yes | A post id from list_scheduled_posts. |

## Example

An agent calls `cancel_post` with these arguments:

```json
{
  "post_id": "<post_id>"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X DELETE "https://api.skryvo.ai/api/v1/agent/posts/$POST_ID" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/cancel-post/

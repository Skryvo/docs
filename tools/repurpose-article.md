# Turn an article into posts

> Turns a finished article into one post per platform, ready to schedule.

| | |
|---|---|
| MCP tool | `repurpose_article` |
| REST route | `POST /api/v1/agent/articles/{article_id}/posts` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | One generation for every platform in the call. |

## What it does

Turns a finished article into one native post per platform in the brand's voice, keeping the article's facts. One generation for all of them; how many platforms at once follows the plan. Each post's text is ready for `POST /posts`.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `article_id` | string | Yes | An article id, or its generation id. |
| `platforms` | string[] | Yes | The platforms to write for. |

## Example

An agent calls `repurpose_article` with these arguments:

```json
{
  "article_id": "<article_id>",
  "platforms": [
    "linkedin",
    "x"
  ]
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/articles/$ARTICLE_ID/posts" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "platforms": [
    "linkedin",
    "x"
  ]
}'
```

The reply:

```json
{
  "article_id": "gen_a7c2f0",
  "posts": [
    {
      "platform": "linkedin",
      "text": "Buying your first grinder? Start with the burrs.",
      "generation_id": "gen_r3p0s7",
      "error": null
    }
  ],
  "left": {
    "generations": 41,
    "image_credits": 180,
    "resets_at": "2026-12-01T00:00:00+00:00"
  }
}
```

## What it costs

One generation for every platform in the call. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/repurpose-article/

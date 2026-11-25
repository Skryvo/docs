# Write a post

> Drafts a post for up to four platforms in the brand's voice. One generation covers them all. Nothing is scheduled.

| | |
|---|---|
| MCP tool | `write_post` |
| REST route | `POST /api/v1/agent/drafts` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | One generation for the whole batch, plus image credits when pictures is true. |

## What it does

Writes a post about `topic` for up to four platforms in the brand's own voice. Pass only what the person said. When platforms or pictures were left out, the call writes nothing and returns `status: confirm` with every setting, where it came from (`you`, `brand`, `brand profile`, `Skryvo default`), the cost and what is left; call again with the person's final values and `confirmed: true`. One generation for the whole batch, plus picture credits when pictures are on. Nothing is scheduled.

With `callback_url` the call answers 202 at once with a job; the work runs as it would have, charged and refunded the same way, and its answer (or refusal) is posted to `callback_url` as `job.done` or `job.failed`, signed with the job's `secret` like a webhook and retried the same way. `GET /jobs/{job_id}` reads it meanwhile.
With pictures, a call that needs more than about 45 seconds answers `status: working` with a `job_id`; [`job_status`](https://skryvo.ai/docs/tools/job-status/) hands back the finished posts.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `topic` | string | Yes | What the post is about, 3 to 200 characters. |
| `platforms` | string[] | No | Up to 4 platforms; omitted, the brand's default. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |
| `tone` | string | No | Omitted, the brand's tone. |
| `language` | string | No | A language code; omitted, the brand's writing language. |
| `audience` | string | No | Who the post is for. |
| `call_to_action` | string | No | What the reader should do next. |
| `hashtags` | string[] | No | Hashtags the person asked for. |
| `link` | string | No | A web page the post points to. |
| `pictures` | boolean | No | A picture in the brand's kept look with each post. |
| `confirmed` | boolean | No | true once the person approved the summary of what was assumed. |

## Example

An agent calls `write_post` with these arguments:

```json
{
  "topic": "Our new studio opens Saturday",
  "platforms": [
    "linkedin",
    "x"
  ],
  "tone": "friendly",
  "pictures": false,
  "confirmed": true
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/drafts" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "topic": "Our new studio opens Saturday",
  "platforms": [
    "linkedin",
    "x"
  ],
  "tone": "friendly",
  "pictures": false,
  "confirmed": true
}'
```

The reply:

```json
{
  "status": "written",
  "topic": "Our new studio opens Saturday",
  "brand_id": "bv_3c9d0e",
  "generation_id": "gen_5d1c9a",
  "posts": [
    {
      "platform": "linkedin",
      "text": "Our new studio opens this Saturday in Leeds. #coffee",
      "hashtags": [
        "coffee"
      ]
    }
  ],
  "settings": [
    {
      "field": "platforms",
      "value": [
        "linkedin",
        "x"
      ],
      "from": "brand"
    },
    {
      "field": "tone",
      "value": "friendly",
      "from": "you"
    },
    {
      "field": "pictures",
      "value": true,
      "from": "Skryvo default"
    }
  ],
  "differs_from_brand": [
    {
      "field": "tone",
      "value": "friendly",
      "brand_default": "professional"
    }
  ]
}
```

## What it costs

One generation for the whole batch, plus image credits when pictures is true. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/write-post/

# Job status

> Says where a slow post or picture is, and hands back its answer once it is done.

| | |
|---|---|
| MCP tool | `job_status` |
| REST route | `GET /api/v1/agent/jobs/{job_id}` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

Where a call made with `callback_url` is: `running`, `done` with the route's own answer, or `failed` with the status and sentence the route would have answered. A job whose process is lost ends failed within about 15 minutes and is not charged.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `job_id` | string | Yes | The job a slow call answered with. |

## Example

An agent calls `job_status` with these arguments:

```json
{
  "job_id": "<job_id>"
}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/jobs/$JOB_ID" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "job_id": "job_5e4d3c2b1a09f8e7d6c5b4a3",
  "kind": "pictures",
  "status": "done",
  "answer": {
    "brand_id": "bv_3c9d0e",
    "headline": "Our new studio opens Saturday",
    "pictures": [
      {
        "platform": "linkedin",
        "image_url": "https://media.skryvo.ai/images/u1/p-1200.jpg",
        "width": 1200,
        "height": 1200
      }
    ],
    "credits_used": 4,
    "credits_left": 176
  },
  "error": null,
  "started_at": "2026-11-24T09:00:00+00:00",
  "finished_at": "2026-11-24T09:01:12+00:00"
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/job-status/

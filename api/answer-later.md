# Calls that answer later

> Send a callback_url with a long call and get a 202 at once; the answer arrives signed at your address, or by polling the job.

Some calls take a minute or more: [`write_post`](https://skryvo.ai/docs/tools/write-post/) (`POST /api/v1/agent/drafts`), [`design_picture`](https://skryvo.ai/docs/tools/design-picture/) (`POST /api/v1/agent/pictures`), [`plan_article`](https://skryvo.ai/docs/tools/plan-article/) (`POST /api/v1/agent/articles/plan`) and [`job_status`](https://skryvo.ai/docs/tools/job-status/) (`GET /api/v1/agent/jobs/{job_id}`). A tool that waits on an answer, such as an automation step with a time limit, can pass `callback_url` instead and carry on. Without it, nothing changes: the call answers when the work is done, as before.

## When to use it

- The tool running the call stops waiting after a fixed time, as many automation steps do.
- The answer goes to another step anyway, such as a scenario that resumes on a webhook.
- A script starts several pictures or plans and collects them as they finish.

## The 202 answer

Add `callback_url` to the body: an `https://` address on the public internet, checked the same way as a webhook address. The call answers **202** at once:

```json
{
  "job_id": "job_5e4d3c2b1a09f8e7d6c5b4a3",
  "status": "running",
  "secret": "whsec_…",
  "poll_url": "https://api.skryvo.ai/api/v1/agent/jobs/job_5e4d3c2b1a09f8e7d6c5b4a3"
}
```

The `secret` is shown this once and signs the callback. Keep it with the job.

## The callback

When the work ends, Skryvo POSTs to `callback_url`:

| Event | When | What it carries |
|---|---|---|
| `job.done` | A long call finished | Posted to a call's own `callback_url`, never to a webhook. `data` is the job, with the route's answer. |
| `job.failed` | A long call could not finish | Posted to a call's own `callback_url`, never to a webhook. `data` is the job, with the refusal; nothing was charged. |

```json
{
  "id": "evt_6f1d0c9e8b7a6f5e4d3c2b1a",
  "type": "job.done",
  "created": "2026-11-24T09:00:03+00:00",
  "test": false,
  "data": {
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
}
```

The request carries `Skryvo-Event`, `Skryvo-Delivery` and `Skryvo-Signature`, signed with the job's secret exactly as a [webhook](https://skryvo.ai/docs/api/webhooks/) is, and the same code checks it. Answer with any 2xx within 10 seconds. Anything else is tried again after 5 minutes, 30 minutes, 2 hours, 6 hours and 12 hours. Redirects are not followed.

A job's `answer` is the route's own answer, exactly as it would have come without `callback_url`. When the call needed the person's choices first, the job is `done` and its answer says `status: "confirm"`: nothing was spent, so call again with `"confirmed": true`, and a `callback_url` again if you want one.

## Polling instead

`GET /jobs/{job_id}` with the same key reads the job at any time: `running`, `done` with its `answer`, or `failed` with an `error` holding the HTTP status and the sentence the route would have answered.

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

## What happens to the charge

A job spends exactly what the route spends without `callback_url`: the same generations, picture credits and article plans. Each charge is tied to the job, so a retry never charges twice. When the work fails, its charges are handed back, as the route does. A job still running after 10 minutes has lost its process: the next publish sweep, every 5 minutes, ends it `failed` with a sentence saying nothing was charged, hands back each of its charges once and sends the callback.

Jobs and their answers are kept for 30 days, then deleted.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/api/answer-later/

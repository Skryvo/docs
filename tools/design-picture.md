# Design a picture

> Designs a picture for the post in your brand's look, at each platform's own size, using Image Studio credits.

| | |
|---|---|
| MCP tool | `design_picture` |
| REST route | `POST /api/v1/agent/pictures` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Image credits: one picture's worth for each page shape the platforms need, square or wide. A shape that fails its checks is not charged. |

## What it does

Designs one picture for a post in the brand's kept look (its colours, type, logo and own photos), with a copy sized for each platform. The post's opening line is set on the picture unless `headline` (up to nine words) is given. `direction` carries the person's own words, such as warmer or calmer; `photo_id` picks one of the brand's photos. Takes about a minute and spends one picture's credits for each page shape the platforms need. The brand must have kept a look first. Nothing is scheduled.

With `callback_url` the call answers 202 at once with a job; the work runs as it would have, charged and refunded the same way, and its answer (or refusal) is posted to `callback_url` as `job.done` or `job.failed`, signed with the job's `secret` like a webhook and retried the same way. `GET /jobs/{job_id}` reads it meanwhile.
Until the brand keeps a look, the call is refused; [`change_look`](https://skryvo.ai/docs/tools/change-look/) designs and keeps one. A picture that needs more than about 45 seconds answers `status: working` with a `job_id`; [`job_status`](https://skryvo.ai/docs/tools/job-status/) hands back the finished picture.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `text` | string | Yes | The post the picture goes with. |
| `platforms` | string[] | Yes | The platforms to size it for. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |
| `direction` | string | No | What the person wants for the picture, in their words, or a steer: warmer, closer, bolder, calmer. |
| `headline` | string | No | The line set on the picture, up to nine words; omitted, the post's opening. |
| `photo_id` | string | No | One of the brand's own photos, as brand_design lists them. |

## Example

An agent calls `design_picture` with these arguments:

```json
{
  "text": "Our new studio opens this Saturday in Leeds.",
  "platforms": [
    "linkedin",
    "instagram"
  ],
  "direction": "warmer"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/pictures" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "text": "Our new studio opens this Saturday in Leeds.",
  "platforms": [
    "linkedin",
    "instagram"
  ],
  "direction": "warmer"
}'
```

The reply:

```json
{
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
}
```

## What it costs

Image credits: one picture's worth for each page shape the platforms need, square or wide. A shape that fails its checks is not charged. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/design-picture/

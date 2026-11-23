# Plan the calendar

> Plans a week or a month of social posts for a brand, using one generation. Adds nothing yet.

| | |
|---|---|
| MCP tool | `plan_calendar` |
| REST route | `POST /api/v1/agent/calendar/plan` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | One generation and one of the month's calendar plans. |

## What it does

Plans a week or a month of social posts for a brand from `start_date`: each row has a date, time, platform, topic and why. Uses one generation and one of the month's calendar plans. Adds nothing to the calendar; show it to the person and send the rows they keep to `POST /calendar/accept`.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `start_date` | string | Yes | YYYY-MM-DD. |
| `period` | string | No | week or month; default week. |
| `topics` | string[] | No | What to focus on. |
| `platforms` | string[] | No | Where to post. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |

## Example

An agent calls `plan_calendar` with these arguments:

```json
{
  "start_date": "2026-11-30",
  "period": "week",
  "platforms": [
    "linkedin"
  ]
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/calendar/plan" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "start_date": "2026-11-30",
  "period": "week",
  "platforms": [
    "linkedin"
  ]
}'
```

The reply:

```json
{
  "period": "week",
  "start_date": "2026-11-30",
  "end_date": "2026-12-06",
  "items": [
    {
      "day": "Monday",
      "date": "2026-11-30",
      "time": "09:00",
      "content_type": "social_media",
      "platform": "linkedin",
      "topic": "Behind the counter: our roasting day",
      "reasoning": "Process posts lead the brand's engagement.",
      "is_repurpose": false
    }
  ],
  "summary": {
    "total_items": 5,
    "blogs": 0,
    "social_posts": 5,
    "emails": 0,
    "repurposed": 0
  }
}
```

## What it costs

One generation and one of the month's calendar plans. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/plan-calendar/

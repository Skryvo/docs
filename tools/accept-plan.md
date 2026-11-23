# Accept a plan

> Adds the plan rows you keep to your calendar as planned topics. Nothing is published.

| | |
|---|---|
| MCP tool | `accept_plan` |
| REST route | `POST /api/v1/agent/calendar/accept` |
| Changes anything | Yes. An agent asks the person before it calls it. |
| Cost | Free. |

## What it does

Adds the rows of a plan the person keeps to the calendar as planned topics, each with its date, time, content_type, topic and platform. Nothing is written or published by this. Free.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `items` | object[] | Yes | The plan rows the person keeps. |

## Example

An agent calls `accept_plan` with these arguments:

```json
{
  "items": [
    {
      "date": "2026-11-30",
      "time": "09:00",
      "content_type": "social_media",
      "platform": "linkedin",
      "topic": "Behind the counter: our roasting day"
    }
  ]
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/calendar/accept" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "items": [
    {
      "date": "2026-11-30",
      "time": "09:00",
      "content_type": "social_media",
      "platform": "linkedin",
      "topic": "Behind the counter: our roasting day"
    }
  ]
}'
```

The reply, HTTP 201:

```json
{
  "added": 3
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/accept-plan/

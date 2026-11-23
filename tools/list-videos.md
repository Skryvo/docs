# List videos

> Your own finished videos, uploaded here or in Skryvo.

| | |
|---|---|
| MCP tool | `list_videos` |
| REST route | `GET /api/v1/agent/videos` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

The person's own finished videos, uploaded here or in the app: id, name and size.

## Inputs

None.

## Example

An agent calls `list_videos` with these arguments:

```json
{}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/videos" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "videos": [
    {
      "id": "clip_9e8d7c",
      "name": "opening-day.mp4",
      "bytes": 48213504
    }
  ]
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/list-videos/

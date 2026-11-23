# Finish a video

> Reads an uploaded video and makes it ready to schedule.

| | |
|---|---|
| MCP tool | `finish_video` |
| REST route | `POST /api/v1/agent/videos/{video_id}/finish` |
| Changes anything | Yes. An agent asks the person before it calls it. |
| Cost | Free. |

## What it does

Reads a video once its upload ended and makes it ready to schedule with `by_channel.video_id`. Refused, with the reason, when the file can't be read.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `video_id` | string | Yes | A video id from add_video or list_videos. |

## Example

An agent calls `finish_video` with these arguments:

```json
{
  "video_id": "<video_id>"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/videos/$VIDEO_ID/finish" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "video_id": "clip_9e8d7c",
  "status": "ready",
  "seconds": 42,
  "width": 1080,
  "height": 1920
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/finish-video/

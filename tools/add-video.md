# Add a video

> Opens an upload for your own video file. Skryvo never makes video.

| | |
|---|---|
| MCP tool | `add_video` |
| REST route | `POST /api/v1/agent/videos` |
| Changes anything | Yes. An agent asks the person before it calls it. |
| Cost | Free. The file counts against the plan's video storage. |

## What it does

Opens an upload for the person's own video file (mp4 or mov, up to 1 GB). Send the file to `upload_url` with an HTTP PUT, then call finish. Counts against the plan's video storage.
Then call [`finish_video`](https://skryvo.ai/docs/tools/finish-video/) and pass the id to `schedule_post` as `by_channel.<channel_id>.video_id`.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `name` | string | Yes | Its file name. |
| `size` | integer | Yes | The file size in bytes. |
| `mime` | string | No | video/mp4 or video/quicktime. |

## Example

An agent calls `add_video` with these arguments:

```json
{
  "name": "opening-day.mp4",
  "size": 48213504,
  "mime": "video/mp4"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/videos" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "name": "opening-day.mp4",
  "size": 48213504,
  "mime": "video/mp4"
}'
```

The reply, HTTP 201:

```json
{
  "id": "clip_9e8d7c",
  "upload_url": "https://storage.skryvo.ai/upload/clip_9e8d7c?sig=…",
  "chunk_bytes": 8388608
}
```

## What it costs

Free. The file counts against the plan's video storage. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/add-video/

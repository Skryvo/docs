# Schedule a post

> Puts a post on your calendar for each chosen account, with its picture. Skryvo publishes it on the quarter hour and checks it went live.

| | |
|---|---|
| MCP tool | `schedule_post` |
| REST route | `POST /api/v1/agent/posts` |
| Changes anything | Yes. An agent asks the person before it calls it. |
| Cost | Free. Scheduled posts count toward the plan's queue, and posts to X count against its monthly X allowance. |

## What it does

Schedules one post to each social channel; Skryvo publishes it at its time and reads it back to confirm it went live. `at` is moved to the calendar's next quarter hour; omitted, about five minutes from now. `image_url` gives every channel one picture, `images` gives a channel its own, and `by_channel` gives a channel its own words, picture, video, title, options, thread, poll and comments. A channel that cannot take the post is refused before anything is written. Get the person's go-ahead on the words, channels and time first.
A channel takes only what its listing in [`list_channels`](https://skryvo.ai/docs/tools/list-channels/) says it takes. Over REST, TikTok settings go in a `tiktok` object: `privacy` (required), `allow_comments`, `allow_duet`, `allow_stitch`, `your_brand` and `branded_content`; an agent passes `tiktok_privacy`.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `text` | string | Yes | The post the person approved. |
| `channel_ids` | string[] | Yes | Social channels from list_channels. |
| `at` | string | No | ISO 8601 time, moved to the next quarter hour; omitted, about 5 minutes from now. |
| `image_url` | string | No | One picture for every channel. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |
| `tiktok_privacy` | string | No | PUBLIC_TO_EVERYONE, MUTUAL_FOLLOW_FRIENDS, FOLLOWER_OF_CREATOR or SELF_ONLY, as the person chose. |
| `link` | string | No | A web page the post points to. |
| `images` | object | No | {channel_id: image_url}: a channel's own picture, such as its sized copy. |
| `button` | string | No | A Google Business Profile button: learn_more, book, order, shop, sign_up or call. |
| `by_channel` | object | No | {channel_id: ...}: a channel's own text, image_url, video_id, title, options, thread, numbered, poll, comments, tiktok and youtube, as its listing says it takes. |

## Example

An agent calls `schedule_post` with these arguments:

```json
{
  "text": "Our new studio opens this Saturday in Leeds. Come say hello.",
  "channel_ids": [
    "conn_8f2e1a"
  ],
  "at": "2026-11-24T09:00:00+00:00",
  "image_url": "https://media.skryvo.ai/images/u1/p-1200.jpg"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/posts" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "text": "Our new studio opens this Saturday in Leeds. Come say hello.",
  "channel_ids": [
    "conn_8f2e1a"
  ],
  "at": "2026-11-24T09:00:00+00:00",
  "image_url": "https://media.skryvo.ai/images/u1/p-1200.jpg"
}'
```

The reply, HTTP 201:

```json
{
  "posts": [
    {
      "id": "c1a2b3c4d5",
      "platform": "linkedin",
      "channel_id": "conn_8f2e1a",
      "date": "2026-11-24",
      "time": "09:00",
      "status": "scheduled",
      "reason": null,
      "awaiting_approval": false,
      "reviewer_approval": null,
      "auto_publish": true,
      "text": "We just opened our new studio in Leeds. Come say hello this Saturday.",
      "topic": "New studio opening",
      "written": true,
      "publish_error": null,
      "posted_url": null,
      "open_in_skryvo": "https://app.skryvo.ai/calendar?date=2026-11-24"
    }
  ]
}
```

## What it costs

Free. Scheduled posts count toward the plan's queue, and posts to X count against its monthly X allowance. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/schedule-post/

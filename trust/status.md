# Channel status

> How many posts each channel published and how many failed, day by day for the last 90 days.

The chart above is drawn from the public status route each time the page opens. Counting began the day the route went live, so the chart names that day and leaves earlier days empty instead of calling them clear.

## What the chart counts

Each channel's row shows the last 90 days. A day shows how many posts Skryvo published to that channel and how many the platform refused, counted across every Skryvo account as each post is recorded. A post counts as published once Skryvo has read it back live, and as failed when the platform refused it; a post Skryvo itself could not send in time is not counted against the channel. Nothing is sampled or estimated.

| A day shows | It means |
|---|---|
| Published and no failures | Every post due that day went out. |
| Some failures | The platform refused some posts. A refusal can be the post's own (too long, a missing picture, an account that needs reconnecting), so a failure on one day does not mean the channel was down. |
| No posts | Nobody had a post due on that channel that day. Skryvo cannot say whether the channel worked, so the day is shown as no posts, never as working or as down. |
| Not counted yet | The day is before `counted_since`, when counting began. It is left empty rather than shown as a day with no failures. |

## Read it yourself

The numbers are public at one route, with no key:

```bash
curl https://api.skryvo.ai/api/v1/status/channels
```

```json
{
  "updated_at": "2026-11-23T09:00:00Z",
  "counted_since": "2026-11-23",
  "channels": [
    {"platform": "linkedin", "days": [{"date": "2026-11-22", "published": 0, "failed": 0}]}
  ]
}
```

The route is cached, so `updated_at` says when the numbers were last counted.

## When your own post failed

The calendar shows the platform's reason in plain words on the post itself, and the Desk groups failed posts with one fix each. Each [channel page](https://skryvo.ai/docs/channels/) lists the reasons a post can fail there and the fix. An account whose access ended asks to be reconnected; Skryvo renews access before it lapses wherever the platform allows it.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/trust/status/

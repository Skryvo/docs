# Cron and other CI

> A shell script on a schedule that plans next week's posts and adds them to the calendar as planned topics.

Any machine or CI that runs a shell step on a schedule can drive Skryvo with `curl` and `jq`. This script plans next week's posts for a brand and adds them to the calendar as planned topics. Skryvo writes each one before its time and sets none to publish, so a person checks them and schedules the ones they keep.

Skryvo's own [Skryvo CLI](https://www.npmjs.com/package/skryvo) is published under the MIT licence and does the same steps without the HTTP settings.

## Before you start

1. In Skryvo, open **Settings › API & agents** and create an API key. Store it as a secret in the tool, never in the workflow's text.
2. Find the ids of the channels to post to:

```bash
curl https://api.skryvo.ai/api/v1/agent/channels \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

Each channel's `id` goes in `channel_ids`, and its `can` says what it takes.

## The script
```bash
#!/bin/sh
set -eu
API=https://api.skryvo.ai/api/v1/agent
AUTH="Authorization: Bearer $SKRYVO_API_KEY"
MONDAY=$(date -d 'next monday' +%F)

curl -sf -X POST "$API/calendar/plan" -H "$AUTH" -H "Content-Type: application/json" \
  -d "{\"start_date\": \"$MONDAY\", \"period\": \"week\", \"platforms\": [\"linkedin\", \"instagram\"]}" \
  | jq '{items: [.items[] | {date, time, content_type, platform, topic}]}' \
  | curl -sf -X POST "$API/calendar/accept" -H "$AUTH" -H "Content-Type: application/json" -d @-
```

`date -d 'next monday'` is GNU date; on macOS use `date -v+monday +%F`. Planning uses one generation and one of the month's calendar plans; adding the rows is free.

## Run it every Monday

```text
0 7 * * 1 SKRYVO_API_KEY=sk_skryvo_… /usr/local/bin/skryvo-week.sh
```

In a CI, keep the key in the CI's secrets and run the same script from a scheduled job.

## Keep a person in the loop

`write_post` returns drafts and schedules nothing, so the workflow decides when a person sees them. Three ways that work today:

- **Send the drafts for a yes.** Email or message the drafts to the person, and schedule only the ones they approve.
- **Let the team's approval hold them.** A key made by an editor on a brand that needs approval puts each scheduled post in the reviewer's queue: `schedule_post` answers with `awaiting_approval: true`, and nothing goes out until a reviewer approves it in Skryvo. [Approvals](https://skryvo.ai/docs/using/approvals/).
- **Plan topics instead of posts.** [`plan_calendar`](https://skryvo.ai/docs/tools/plan-calendar/) and [`accept_plan`](https://skryvo.ai/docs/tools/accept-plan/) add planned topics: Skryvo writes each one before its time and sets none to publish, so the person checks them in the calendar and schedules the ones they keep.

Any scheduled post can be moved, changed or cancelled in the calendar before it goes out.

## Know when a post is out

Register a [webhook](https://skryvo.ai/docs/api/webhooks/) for `post.published` and `post.failed`, and the workflow starts the moment a post goes out or fails. Without one, poll `GET https://api.skryvo.ai/api/v1/agent/posts?days=1` a few minutes after the post's time. A post with `posted_url` set is live and was read back from the platform; one with `publish_error` set did not go out, and the error says why in plain words.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/automate/cron/

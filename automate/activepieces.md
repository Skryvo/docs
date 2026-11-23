# Skryvo in Activepieces

> An Activepieces flow that writes posts in a brand's voice and schedules them, over the REST API.

A flow that writes posts in the brand's voice on a schedule and schedules the approved ones. It uses the HTTP piece against the [REST API](https://skryvo.ai/docs/api/overview/).

Skryvo's own [Activepieces piece](https://www.npmjs.com/package/@skryvo/piece-skryvo) is published under the MIT licence and does the same steps without the HTTP settings.

## Before you start

1. In Skryvo, open **Settings › API & agents** and create an API key. Store it as a secret in the tool, never in the workflow's text.
2. Find the ids of the channels to post to:

```bash
curl https://api.skryvo.ai/api/v1/agent/channels \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

Each channel's `id` goes in `channel_ids`, and its `can` says what it takes.

## Build the flow

1. **Trigger.** Schedule › Every Week, or any piece that hands over a topic.
2. **Write the posts.** HTTP › **Send HTTP request**: method `POST`, URL `https://api.skryvo.ai/api/v1/agent/drafts`, a header `Authorization` with `Bearer sk_skryvo_…` (keep the key in a connection or a secret), body type JSON:

   ```json
   {"topic": "What we shipped this week", "platforms": ["linkedin", "bluesky"], "pictures": false}
   ```

3. **Get a yes.** Send the drafts by email or chat and wait for the person's approval.
4. **Schedule.** HTTP › **Send HTTP request** to `https://api.skryvo.ai/api/v1/agent/posts` with `{"text": "…", "channel_ids": ["…"], "at": "…"}` for each approved post.

## Keep a person in the loop

`write_post` returns drafts and schedules nothing, so the workflow decides when a person sees them. Three ways that work today:

- **Send the drafts for a yes.** Email or message the drafts to the person, and schedule only the ones they approve.
- **Let the team's approval hold them.** A key made by an editor on a brand that needs approval puts each scheduled post in the reviewer's queue: `schedule_post` answers with `awaiting_approval: true`, and nothing goes out until a reviewer approves it in Skryvo. [Approvals](https://skryvo.ai/docs/using/approvals/).
- **Plan topics instead of posts.** [`plan_calendar`](https://skryvo.ai/docs/tools/plan-calendar/) and [`accept_plan`](https://skryvo.ai/docs/tools/accept-plan/) add planned topics: Skryvo writes each one before its time and sets none to publish, so the person checks them in the calendar and schedules the ones they keep.

Any scheduled post can be moved, changed or cancelled in the calendar before it goes out.

## Know when a post is out

Register a [webhook](https://skryvo.ai/docs/api/webhooks/) for `post.published` and `post.failed`, and the workflow starts the moment a post goes out or fails. Without one, poll `GET https://api.skryvo.ai/api/v1/agent/posts?days=1` a few minutes after the post's time. A post with `posted_url` set is live and was read back from the platform; one with `publish_error` set did not go out, and the error says why in plain words.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/automate/activepieces/

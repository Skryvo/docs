# Skryvo in Zapier

> A Zap that writes posts in a brand's voice from each new item and schedules them, over the REST API.

A Zap that writes posts in the brand's voice from each new item, then schedules them once a person approves. It uses Zapier's own Webhooks by Zapier action against the [REST API](https://skryvo.ai/docs/api/overview/).

Skryvo's own [Zapier app](https://zapier.com/developer/public-invite/251283/89dd6215f58e09902a7fc68d78433dda/) is published under the MIT licence and does the same steps without the HTTP settings.

## Before you start

1. In Skryvo, open **Settings › API & agents** and create an API key. Store it as a secret in the tool, never in the workflow's text.
2. Find the ids of the channels to post to:

```bash
curl https://api.skryvo.ai/api/v1/agent/channels \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

Each channel's `id` goes in `channel_ids`, and its `can` says what it takes.

## Build the Zap

1. **Trigger.** Schedule by Zapier, RSS by Zapier (a new item in your blog's feed), or any app's trigger that hands over a topic.
2. **Write the posts.** Webhooks by Zapier › **Custom Request**: method `POST`, URL `https://api.skryvo.ai/api/v1/agent/drafts`, headers `Authorization: Bearer sk_skryvo_…` and `Content-Type: application/json`, and data:

   ```json
   {"topic": "the trigger's title", "platforms": ["linkedin", "bluesky"], "pictures": false}
   ```

   Map the topic from the trigger, up to 200 characters.
3. **Get a yes.** Send the drafts to the person by email or chat and continue only on approval.
4. **Schedule.** Another Custom Request: method `POST`, URL `https://api.skryvo.ai/api/v1/agent/posts`, data `{"text": "…", "channel_ids": ["…"]}` with the approved text and the channel's id. With no `at`, the post goes out in about five minutes.
## Plan an article or design a picture

Planning an article and designing a picture take a minute or more, longer than a Zapier step should wait on one request. Pass a `callback_url` and Skryvo answers at once, then posts the result to that address when it is done ([calls that answer later](https://skryvo.ai/docs/api/answer-later/)).

1. **Make the address.** Make a second Zap whose trigger is Webhooks by Zapier › **Catch Hook**, and copy its address.
2. **Start the work.** In the first Zap, Webhooks by Zapier › **Custom Request** with method `POST` to `https://api.skryvo.ai/api/v1/agent/articles/plan` with `{"topic": "…", "callback_url": "<the address>"}`, or `https://api.skryvo.ai/api/v1/agent/pictures` with `{"text": "…", "platforms": ["linkedin"], "callback_url": "<the address>"}`. The answer is 202 with a `job_id`.
3. **Take the answer.** The second Zap receives `job.done` or `job.failed` with the job in `data`. Read it again with your key, `GET https://api.skryvo.ai/api/v1/agent/jobs/{job_id}`, and use that copy: an answer read with your own key needs no signature check. `answer` holds the plan or the pictures, exactly as the call would have returned them.

A plan whose choices were guessed comes back `done` with `status: "confirm"` and nothing spent: show it to the person, then call again with `"confirmed": true`.

## Keep a person in the loop

`write_post` returns drafts and schedules nothing, so the workflow decides when a person sees them. Three ways that work today:

- **Send the drafts for a yes.** Email or message the drafts to the person, and schedule only the ones they approve.
- **Let the team's approval hold them.** A key made by an editor on a brand that needs approval puts each scheduled post in the reviewer's queue: `schedule_post` answers with `awaiting_approval: true`, and nothing goes out until a reviewer approves it in Skryvo. [Approvals](https://skryvo.ai/docs/using/approvals/).
- **Plan topics instead of posts.** [`plan_calendar`](https://skryvo.ai/docs/tools/plan-calendar/) and [`accept_plan`](https://skryvo.ai/docs/tools/accept-plan/) add planned topics: Skryvo writes each one before its time and sets none to publish, so the person checks them in the calendar and schedules the ones they keep.

Any scheduled post can be moved, changed or cancelled in the calendar before it goes out.

## Know when a post is out

Register a [webhook](https://skryvo.ai/docs/api/webhooks/) for `post.published` and `post.failed`, and the workflow starts the moment a post goes out or fails. Without one, poll `GET https://api.skryvo.ai/api/v1/agent/posts?days=1` a few minutes after the post's time. A post with `posted_url` set is live and was read back from the platform; one with `publish_error` set did not go out, and the error says why in plain words.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/automate/zapier/

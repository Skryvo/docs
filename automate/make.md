# Skryvo in Make

> A Make scenario that writes posts in a brand's voice and schedules the approved ones, over the REST API.

A scenario that writes posts in the brand's voice for each new item, sends them for a yes, and schedules the approved ones. It uses Make's own HTTP module against the [REST API](https://skryvo.ai/docs/api/overview/).

Skryvo's own [Make app](https://github.com/Skryvo/make-skryvo) is published under the MIT licence and does the same steps without the HTTP settings.

## Before you start

1. In Skryvo, open **Settings › API & agents** and create an API key. Store it as a secret in the tool, never in the workflow's text.
2. Find the ids of the channels to post to:

```bash
curl https://api.skryvo.ai/api/v1/agent/channels \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

Each channel's `id` goes in `channel_ids`, and its `can` says what it takes.

## Build the scenario

1. **Trigger.** Any module that hands over a topic: a schedule, a new RSS item, a new row.
2. **Write the posts.** HTTP › **Make a request**: URL `https://api.skryvo.ai/api/v1/agent/drafts`, method `POST`, a header `Authorization` with `Bearer sk_skryvo_…`, body type *Raw*, content type *JSON (application/json)*, **Parse response** on, and request content:

   ```json
   {
     "topic": "{{1.title}}",
     "platforms": ["linkedin", "bluesky"],
     "pictures": false
   }
   ```

3. **Split the reply.** An Iterator over `posts`, so each platform's post is its own bundle with `platform` and `text`.
4. **Get a yes.** Email or message each post to the person, and schedule only the ones they approve, for example from a second scenario they start.
5. **Schedule.** HTTP › **Make a request** again: URL `https://api.skryvo.ai/api/v1/agent/posts`, method `POST`, the same header, and content `{"text": "…", "channel_ids": ["…"], "at": "2026-12-01T09:00:00Z"}` mapped from the post and its channel.
## Plan an article or design a picture

Planning an article and designing a picture take a minute or more, longer than a Make step should wait on one request. Pass a `callback_url` and Skryvo answers at once, then posts the result to that address when it is done ([calls that answer later](https://skryvo.ai/docs/api/answer-later/)).

1. **Make the address.** In a second scenario, add Webhooks › **Custom webhook** as its trigger and copy the address Make gives it.
2. **Start the work.** In the first scenario, HTTP › **Make a request** with method `POST` to `https://api.skryvo.ai/api/v1/agent/articles/plan` with `{"topic": "…", "callback_url": "<the address>"}`, or `https://api.skryvo.ai/api/v1/agent/pictures` with `{"text": "…", "platforms": ["linkedin"], "callback_url": "<the address>"}`. The answer is 202 with a `job_id`.
3. **Take the answer.** The second scenario receives `job.done` or `job.failed` with the job in `data`. Read it again with your key, `GET https://api.skryvo.ai/api/v1/agent/jobs/{job_id}`, and use that copy: an answer read with your own key needs no signature check. `answer` holds the plan or the pictures, exactly as the call would have returned them.

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

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/automate/make/

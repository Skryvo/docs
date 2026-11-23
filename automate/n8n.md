# Skryvo in n8n

> An n8n workflow that writes posts in a brand's voice, gets a yes and schedules them, over the REST API.

A workflow that writes posts in the brand's voice from a topic, waits for a person's yes, then schedules them. It uses n8n's own HTTP Request node against the [REST API](https://skryvo.ai/docs/api/overview/).

Skryvo's own [n8n node](https://www.npmjs.com/package/n8n-nodes-skryvo) is published under the MIT licence and does the same steps without the HTTP settings.

## Before you start

1. In Skryvo, open **Settings › API & agents** and create an API key. Store it as a secret in the tool, never in the workflow's text.
2. Find the ids of the channels to post to:

```bash
curl https://api.skryvo.ai/api/v1/agent/channels \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

Each channel's `id` goes in `channel_ids`, and its `can` says what it takes.

## Set up the credential

In n8n, create a **Header Auth** credential: name `Authorization`, value `Bearer sk_skryvo_…` with your key. Every HTTP Request node below uses it, with **Authentication** set to *Generic Credential Type* and *Header Auth*.

## Build the workflow

1. **Trigger.** A Schedule Trigger (every Monday at 08:00, say), or any trigger that hands over a topic, such as a new row in a sheet or a new item in a feed.
2. **Write the posts.** An HTTP Request node: method `POST`, URL `https://api.skryvo.ai/api/v1/agent/drafts`, **Send Body** on, body content type JSON:

   ```json
   {
     "topic": "{{ $json.topic }}",
     "platforms": ["linkedin", "bluesky"],
     "pictures": false
   }
   ```


   The reply's `posts` holds one post per platform, each with its `platform` and `text`. Naming the platforms and `pictures` makes it write at once; leave one out and the reply is a `status: "confirm"` summary instead.
3. **Get a yes.** Send the posts to the person with an email or chat node that waits for their answer, and continue only on approval.
4. **Schedule.** An HTTP Request node: method `POST`, URL `https://api.skryvo.ai/api/v1/agent/posts`, body:

   ```json
   {
     "text": "{{ $json.text }}",
     "channel_ids": ["your LinkedIn channel id"],
     "at": "{{ $now.plus({days: 1}).toISO() }}"
   }
   ```

   Run it once per post, each with its own channel's id. The time moves to the next quarter hour.

## Keep a person in the loop

`write_post` returns drafts and schedules nothing, so the workflow decides when a person sees them. Three ways that work today:

- **Send the drafts for a yes.** Email or message the drafts to the person, and schedule only the ones they approve.
- **Let the team's approval hold them.** A key made by an editor on a brand that needs approval puts each scheduled post in the reviewer's queue: `schedule_post` answers with `awaiting_approval: true`, and nothing goes out until a reviewer approves it in Skryvo. [Approvals](https://skryvo.ai/docs/using/approvals/).
- **Plan topics instead of posts.** [`plan_calendar`](https://skryvo.ai/docs/tools/plan-calendar/) and [`accept_plan`](https://skryvo.ai/docs/tools/accept-plan/) add planned topics: Skryvo writes each one before its time and sets none to publish, so the person checks them in the calendar and schedules the ones they keep.

Any scheduled post can be moved, changed or cancelled in the calendar before it goes out.

## Know when a post is out

Register a [webhook](https://skryvo.ai/docs/api/webhooks/) for `post.published` and `post.failed`, and the workflow starts the moment a post goes out or fails. Without one, poll `GET https://api.skryvo.ai/api/v1/agent/posts?days=1` a few minutes after the post's time. A post with `posted_url` set is live and was read back from the platform; one with `publish_error` set did not go out, and the error says why in plain words.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/automate/n8n/

# What an agent can and cannot do

> The limits on a connected agent: its tools, the approvals it waits for, what Skryvo sees and how to stop it.

## Only these tools

A connected agent can use the 35 [agent tools](https://skryvo.ai/docs/tools/) and nothing else. It cannot change the person's plan, password, connected accounts or billing, and it sees only the signed-in account: asking for another person's posts is refused.

## Tools that change something

11 tools change the calendar, a brand or its videos. The server's instructions tell an agent to show a draft and get the person's go-ahead before `schedule_post`, and the descriptions of `publish_article`, `change_post`, `change_look`, `keep_defaults` and `add_brand` ask for the same:

- [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/): Puts a post on your calendar for each chosen account, with its picture. Skryvo publishes it on the quarter hour and checks it went live.
- [`cancel_post`](https://skryvo.ai/docs/tools/cancel-post/): Removes a scheduled post before it goes out.
- [`change_look`](https://skryvo.ai/docs/tools/change-look/): Designs your look again bolder, calmer, closer to your site or with another photo, or keeps the one on show.
- [`publish_article`](https://skryvo.ai/docs/tools/publish-article/): Schedules a finished article to a connected blog, or sends it there as a draft.
- [`keep_defaults`](https://skryvo.ai/docs/tools/keep-defaults/): Keeps your choices as the brand's defaults, after you say yes.
- [`change_post`](https://skryvo.ai/docs/tools/change-post/): Moves a scheduled post that has not gone out, changes its words, or both.
- [`review_post`](https://skryvo.ai/docs/tools/review-post/): Records your decision on a team post waiting for approval.
- [`accept_plan`](https://skryvo.ai/docs/tools/accept-plan/): Adds the plan rows you keep to your calendar as planned topics. Nothing is published.
- [`add_brand`](https://skryvo.ai/docs/tools/add-brand/): Adds a brand and reads its voice, kit and facts from its website, using one voice training.
- [`add_video`](https://skryvo.ai/docs/tools/add-video/): Opens an upload for your own video file. Skryvo never makes video.
- [`finish_video`](https://skryvo.ai/docs/tools/finish-video/): Reads an uploaded video and makes it ready to schedule.

The rest read, or return a draft for the person to see. Writing tools publish nothing: a post goes out only through `schedule_post` and an article only through `publish_article`.

## The person's rules still apply

Plan limits, brand settings and each platform's own rules apply exactly as in the app. In a team, the member's role decides what the agent may do: only reviewers, admins and owners decide posts waiting for approval, only admins and owners change a brand's look or keep defaults, and an editor's post on a brand that needs approval waits for a reviewer. A refusal arrives as a sentence the agent can show.

## What Skryvo receives

Only the tool calls the agent makes, never the rest of the conversation with it.

## Keys and sign-ins

- An API key is shown once, stored only as its hash and opens the agent API and nothing else in the account.
- OAuth tokens are stored the same way. Access tokens last 1 hour; refresh tokens last 90 days and rotate on each use.
- Each key or sign-in may make 60 requests a minute, and a looping agent is held back by the [rate limit](https://skryvo.ai/docs/api/limits/).

## Stop an agent

In Skryvo, **Settings › API & agents** lists every connected app and every key. Disconnecting an app or revoking a key stops it at once. Any post an agent scheduled stays on the calendar, where it can be moved, changed or cancelled before it goes out.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/agents/safety/

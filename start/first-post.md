# Your first post, from sign-up to live

> Sign up, let Skryvo read your brand, connect a channel, approve a post and watch it go live.

This is the shortest path from a new account to a post that is published and checked. Each step names the screen you will see.

## 1. Sign up

Create an account at https://app.skryvo.ai/signup with your email, Google or Bluesky. Setup then runs four steps: **Use**, **Brand**, **Channels** and **Plan**.

## 2. Tell Skryvo what you will use it for

The **Use** step asks what kind of work you do (a marketing team, an agency, a shop, a blog, a freelancer). It sets what your dashboard shows first. You can change it later.

## 3. Let it read your brand

In the **Brand** step, give your website's address. Skryvo reads its pages and builds the brand's kit: logo, colours, fonts, the photos it can use, and what the business does. Beside the kit it designs your first posts in a look made from all of it.

- If the site does not say something outright, such as who you serve, Skryvo asks, with a few likely answers to pick from.
- **Make it yours** changes the direction, a photo or the fonts. Two redesigns are free.
- **Use this look** keeps the look. Every picture Skryvo designs for the brand from then on wears it.

No website? Start from your social accounts, from photos you upload, or from a starting look.

## 4. Connect a channel

The **Channels** step lists every channel. Pick one and sign in on the platform's own page; Skryvo keeps the access it is given, encrypted with its own key. Telegram, Dev.to and self-hosted WordPress connect differently; each [channel page](https://skryvo.ai/docs/channels/) says how.

## 5. Start the trial

The **Plan** step offers Hobby and Pro, each with a 7-day free trial and no card. See [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/).

## 6. Approve your first week

Setup ends on your dashboard. Skryvo has drafted a first week of posts for the brand, and they wait there for your approval. Read each one, change the words if you want, and approve it. An approved post is set to go out at its time.

Prefer to write it yourself? Open the social post writer and type the post: your own words use no generation. Or give a topic and let Skryvo draft one per platform.

## 7. Schedule it

Pick a time. Posts go out on the quarter hour (:00, :15, :30 or :45) in the calendar's time zone, so 9:07 becomes 9:15. A time that has passed is refused.

## 8. The live check

At its time Skryvo publishes the post through the platform's API, then reads it back from the platform. Only a post that reads back counts as published, and the calendar shows its link. Slack is the one exception: its webhook answers "ok" and returns no post to read, so Slack's own answer is the confirmation. If a platform refuses the post, the calendar shows its reason in plain words. See [Publishing and the live check](https://skryvo.ai/docs/using/publishing/).

## Do the same from an AI agent

Connect your agent ([Connect an agent](https://skryvo.ai/docs/agents/connect/)) and ask it for a post. It calls [`list_channels`](https://skryvo.ai/docs/tools/list-channels/), drafts with [`write_post`](https://skryvo.ai/docs/tools/write-post/), shows you the draft, and only after your yes calls [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/start/first-post/

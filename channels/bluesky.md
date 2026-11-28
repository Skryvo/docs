# Post to Bluesky

> What Skryvo posts to Bluesky, its limits, how to connect it, and why a post can fail.

Sign in with your Bluesky account, or use an app password, then schedule posts and threads from the calendar or your AI agent.

## What it can post

- Posts
- Images
- Your videos
- Threads
- Reposts
- Comments from your other accounts

## Limits

- 300 characters per post
- Up to 4 images, 2 MB each, or a video up to 3 minutes
- Threads and reposts

Source: [Bluesky post lexicon](https://github.com/bluesky-social/atproto/blob/main/packages/api/lexicons/app/bsky/feed/post.json).

## Good to know

- **Sign-in or app password.** Connect with Bluesky's sign-in or an app password, which you can revoke in Bluesky's settings at any time.
- **300 graphemes, 3,000 bytes.** Bluesky counts graphemes, so an emoji is one character, and caps each post at 3,000 bytes.
- **Up to 4 images.** Each post takes up to four images of 2 MB each.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Bluesky under **Add a channel**.
2. Sign in with Bluesky, or enter your handle and an app password made in Bluesky's settings.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Bluesky when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Bluesky before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Bluesky's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Bluesky rejected the handle or app password | The app password was revoked or mistyped. | Make a new app password in Bluesky and reconnect. |
| Bluesky couldn't use this video | Bluesky takes a video of up to 100 MB and 3 minutes. | Shorten or compress the video and attach it again. |
| Bluesky needs reconnecting | The access you gave Skryvo ended or was revoked on Bluesky. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when Bluesky refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Bluesky did not accept the post | Bluesky refused it without a reason Skryvo can name. | Check the post against the limits above and on Bluesky, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread.

The channel's marketing page, with its questions and the platform's own scheduling: [Bluesky on Skryvo](https://skryvo.ai/channels/bluesky/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/bluesky/

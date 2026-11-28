# Post to Threads

> What Skryvo posts to Threads, its limits, how to connect it, and why a post can fail.

Sign in with Threads and schedule posts with images or your video, written in your brand's voice within 500 characters per post.

## What it can post

- Posts
- Images
- Your videos
- Who can reply

## Limits

- 500 characters per post
- Up to 20 images or a video up to 5 minutes
- Who can reply

Source: [Threads API docs](https://developers.facebook.com/docs/threads/posts).

## Good to know

- **What it posts.** Posts with up to 20 images or your video up to 5 minutes.
- **500 characters.** Each Threads post holds up to 500 characters and five links.
- **Who can reply.** Choose for each post: everyone, accounts you follow, your followers or only the accounts you mention.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Threads under **Add a channel**.
2. Sign in with Threads and approve Skryvo.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Threads when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Threads before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Threads's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Threads could not process the image | Threads refused the picture file. | Replace the picture, then try again. |
| Threads needs reconnecting | The access you gave Skryvo ended or was revoked on Threads. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when Threads refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Threads did not accept the post | Threads refused it without a reason Skryvo can name. | Check the post against the limits above and on Threads, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread.

The channel's marketing page, with its questions and the platform's own scheduling: [Threads on Skryvo](https://skryvo.ai/channels/threads/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/threads/

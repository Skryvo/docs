# X

> What Skryvo posts to X, its limits, how to connect it, and why a post can fail.

Write a post or a thread, or ask your agent for one, and put it on the calendar. Skryvo publishes it to X at that time and confirms it is live.

## What it can post

- Posts
- Images
- Your videos
- Threads
- Who can reply
- Reposts
- Comments from your other accounts

## Limits

- 280 characters per post, 4,000 on X Premium
- Up to 4 images or one video per post
- Threads and reposts

Source: [X developer docs](https://docs.x.com/fundamentals/counting-characters).

## Good to know

- **Links count as 23.** X counts every link as 23 characters whatever its length, and Skryvo counts the same way.
- **Threads in order.** A thread goes out post by post as replies, so it reads in the order you wrote it.
- **Who can reply.** Choose who can reply to each post, and an AI-made picture is labelled made with AI unless you turn it off.
- **Native scheduling needs X Pro.** X's own scheduler lives in X Pro; Skryvo works with your normal X sign-in.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose X under **Add a channel**.
2. Sign in with X and approve Skryvo.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for X when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from X before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

## Why a post can fail

A post that does not go out is marked failed on the calendar with X's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| You've used your plan's X posts this month | X posts are a monthly allowance (Hobby 30, Pro 100, Enterprise 1,500), and a post with a link counts as 10 because X charges that much more for it. | Your other channels keep posting. X opens again with next month's allowance, or on a larger plan. |
| The video may already be on X. Check it there | X's answer to the last step of a video upload was lost, and Skryvo never asks twice. | Look on X; post it again only if it is not there. |
| X needs reconnecting | The access you gave Skryvo ended or was revoked on X. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when X refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| X did not accept the post | X refused it without a reason Skryvo can name. | Check the post against the limits above and on X, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread. A thread is `by_channel.<id>.thread`, the posts that follow the first.

The channel's marketing page, with its questions and the platform's own scheduling: [X on Skryvo](https://skryvo.ai/channels/x/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/x/

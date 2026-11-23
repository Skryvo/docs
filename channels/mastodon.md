# Mastodon

> What Skryvo posts to Mastodon, its limits, how to connect it, and why a post can fail.

Sign in on your own Mastodon server, whichever it is. Skryvo registers itself there and posts, threads and boosts at the time you pick.

## What it can post

- Posts
- Images
- Your videos
- Threads
- Boosts

## Limits

- 500 characters per post on most servers
- Images, videos and threads
- Boosts

Source: [Mastodon docs](https://docs.joinmastodon.org/user/posting/).

## Good to know

- **Any server.** Sign in on the server your account lives on; Skryvo is not tied to one instance.
- **500 is the default.** Most servers allow 500 characters; Skryvo writes to that so a post fits everywhere.
- **Boosts and threads.** Skryvo can post threads and boost posts as well as publish new ones.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Mastodon under **Add a channel**.
2. Type the address of the server your account lives on, then sign in there. The first time anyone connects from a server, Skryvo registers itself on it.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Mastodon when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Mastodon before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Mastodon's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Mastodon did not accept the image | The server sets its own media limits. | Use a smaller picture, or check the server's limits. |
| Mastodon needs reconnecting | The access you gave Skryvo ended or was revoked on Mastodon. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when Mastodon refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Mastodon did not accept the post | Mastodon refused it without a reason Skryvo can name. | Check the post against the limits above and on Mastodon, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread.

The channel's marketing page, with its questions and the platform's own scheduling: [Mastodon on Skryvo](https://skryvo.ai/channels/mastodon/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/mastodon/

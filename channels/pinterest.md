# Pinterest

> What Skryvo posts to Pinterest, its limits, how to connect it, and why a post can fail.

Connect Pinterest and schedule Pins with an image, a title and a description written for Pinterest search, on the same calendar as your other posts.

## What it can post

- Pins to the board you pick
- Video Pins

## Limits

- Pin titles up to 100 characters
- Pins go to the board you pick
- Video Pins from 4 seconds to 15 minutes

Source: [Pinterest API spec](https://github.com/pinterest/api-description).

## Good to know

- **The board you pick.** Pick a board for each Pin; a Pin with no board goes to your last one, or else your first.
- **Title 100, description 500.** Skryvo writes Pin titles to 100 characters and descriptions to 500.
- **Business accounts schedule natively.** Pinterest's own scheduler needs a business account and holds 10 Pins at once.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Pinterest under **Add a channel**.
2. Sign in with Pinterest and approve Skryvo. The account needs at least one board; with none, connecting stops with "Create a board on Pinterest first, then connect again."
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Pinterest when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Pinterest before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Pinterest's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Pinterest pins need an image | A Pin is a picture or a video. | Add a picture or your video. |
| Pick a Pinterest board for this post. | The post has no board and the account has none saved. | Choose a board in the post's Pinterest options. |
| Pinterest needs reconnecting | The access you gave Skryvo ended or was revoked on Pinterest. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when Pinterest refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Pinterest did not accept the post | Pinterest refused it without a reason Skryvo can name. | Check the post against the limits above and on Pinterest, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread.

The channel's marketing page, with its questions and the platform's own scheduling: [Pinterest on Skryvo](https://skryvo.ai/channels/pinterest/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/pinterest/

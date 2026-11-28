# Post to Telegram

> What Skryvo posts to Telegram, its limits, how to connect it, and why a post can fail.

Add @SkryvoBot as an admin of your channel with permission to post, type the channel's @username, and schedule messages, photos and albums.

## What it can post

- Messages
- Photos
- Albums

## Limits

- 4,096 characters per message
- Albums of up to 10 photos
- Captions over 1,024 characters go as text with the photos after

Source: [Telegram Bot API](https://core.telegram.org/bots/api).

## Good to know

- **A bot with one permission.** @SkryvoBot needs only permission to post messages in your channel.
- **4,096 and 1,024.** A message holds 4,096 characters; a photo caption holds 1,024.
- **Photos and albums.** Skryvo posts single photos and albums as well as text.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Telegram under **Add a channel**.
2. In Telegram, add @SkryvoBot to your channel as an admin with permission to post messages.
3. Back in Skryvo, enter the channel's public @username, like @yourbrand.
4. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Telegram when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Telegram before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Telegram's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Skryvo's bot can't post there. Make it an admin with 'Post messages'. | The bot was removed or lost its right to post. | Make @SkryvoBot an admin of the channel again with Post messages. |
| One of the post's images is too large for Telegram | Telegram refused a photo's size. | Use a smaller picture. |
| Telegram needs reconnecting | The connection was removed or revoked on Telegram. | Settings › Connected Accounts › **Reconnect**. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Telegram did not accept the post | Telegram refused it without a reason Skryvo can name. | Check the post against the limits above and on Telegram, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread.

The channel's marketing page, with its questions and the platform's own scheduling: [Telegram on Skryvo](https://skryvo.ai/channels/telegram/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/telegram/

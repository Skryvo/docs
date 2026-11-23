# Discord

> What Skryvo posts to Discord, its limits, how to connect it, and why a post can fail.

Discord can't schedule a message itself, but Skryvo can: pick a channel on Discord's own consent page and Skryvo posts your announcements there on schedule. No bot joins your server.

## What it can post

- Messages
- Images

## Limits

- 2,000 characters per message
- Images

Source: [Discord developer docs](https://docs.discord.com/developers/resources/message).

## Good to know

- **No bot joins your server.** Discord gives Skryvo a webhook for the one channel you pick on its consent page, and nothing else.
- **2,000 characters.** Each message is written to Discord's 2,000-character limit.
- **No public numbers.** Discord does not share post results, so Skryvo confirms delivery but shows no reach there.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Discord under **Add a channel**.
2. On Discord's consent page, pick the server and the channel. Discord gives Skryvo a webhook for that one channel; no bot joins your server.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Discord when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Discord before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

Discord shares no post results, so Skryvo shows delivery but no reach. The webhook does not expire, so the account never needs renewing.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Discord's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Discord didn't share a channel. Pick one and try again. | The consent page was finished without a channel. | Connect again and pick a channel. |
| Discord needs reconnecting | The connection was removed or revoked on Discord. | Settings › Connected Accounts › **Reconnect**. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Discord did not accept the post | Discord refused it without a reason Skryvo can name. | Check the post against the limits above and on Discord, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread.

The channel's marketing page, with its questions and the platform's own scheduling: [Discord on Skryvo](https://skryvo.ai/channels/discord/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/discord/

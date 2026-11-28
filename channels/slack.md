# Post to Slack

> What Skryvo posts to Slack, its limits, how to connect it, and why a post can fail.

Slack schedules a single message by itself. Skryvo schedules an announcement to a Slack channel next to the same news on LinkedIn, X and your other channels, written once in your brand's voice.

## What it can post

- Messages
- Images

## Limits

- 3,000 characters per message
- Images

These are the limits Skryvo writes and checks to.

## Good to know

- **One channel per connection.** You pick the channel on Slack's own consent page; Skryvo can post only there.
- **Written to 3,000 characters.** Skryvo keeps each message to 3,000 characters so it stays readable in a channel.
- **No public numbers.** Slack does not share post results, so Skryvo confirms delivery but shows no reach there.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Slack under **Add a channel**.
2. On Slack's consent page, pick the channel. Skryvo can post only there.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Slack when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

Slack answers a delivery with "ok" and returns no post to read back, so its own answer is the confirmation. Skryvo shows the post as delivered.

Slack shares no post results. The webhook does not expire, so the account never needs renewing.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Slack's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Slack didn't share a channel. Pick one and try again. | The consent page was finished without a channel. | Connect again and pick a channel. |
| Slack needs reconnecting | The connection was removed or revoked on Slack. | Settings › Connected Accounts › **Reconnect**. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Slack did not accept the post | Slack refused it without a reason Skryvo can name. | Check the post against the limits above and on Slack, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread.

The channel's marketing page, with its questions and the platform's own scheduling: [Slack on Skryvo](https://skryvo.ai/channels/slack/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/slack/

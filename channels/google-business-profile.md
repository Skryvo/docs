# Post to Google Business Profile

> What Skryvo posts to Google Business Profile, its limits, how to connect it, and why a post can fail.

Post updates to the Business Profiles you manage at the time you pick, each with a photo and a button, in your brand's voice.

## What it can post

- Updates
- A photo
- A button: Book, Order online, Buy, Learn more, Sign up or Call now

## Limits

- Updates up to 1,500 characters
- One photo per update
- Every location your Google account manages

These are the limits Skryvo writes and checks to.

## Good to know

- **A button, not a link in the words.** Your link opens from the update's button; Call now dials the number on your profile.
- **Six months on your profile.** Google archives updates older than six months unless they have a date range.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Google Business Profile under **Add a channel**.
2. Sign in with Google, approve Skryvo, then tick the business locations it may post to. Each location is its own connection.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Google Business Profile when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Google Business Profile before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

Google gives no per-update numbers, so Business Profile updates show as published without reach.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Google Business Profile's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Google may reject an update with a phone number in the words. Remove it and use the Call button instead | Google refuses updates that carry a phone number in the text. | Take the number out and choose the Call now button. |
| A Business Profile update needs words | An update cannot be a photo alone. | Add the words. |
| Reconnect this Business Profile location | The location's access ended. | Reconnect it in Settings › Connected Accounts. |
| Google Business Profile needs reconnecting | The access you gave Skryvo ended or was revoked on Google Business Profile. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when Google Business Profile refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Google Business Profile did not accept the post | Google Business Profile refused it without a reason Skryvo can name. | Check the post against the limits above and on Google Business Profile, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread. `button` sets the update's button: learn_more, book, order, shop, sign_up or call.

The channel's marketing page, with its questions and the platform's own scheduling: [Google Business Profile on Skryvo](https://skryvo.ai/channels/google-business-profile/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/google-business-profile/

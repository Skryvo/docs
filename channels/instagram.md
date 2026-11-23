# Instagram

> What Skryvo posts to Instagram, its limits, how to connect it, and why a post can fail.

Sign in with Instagram and schedule image posts, carousels, Reels from your own videos and Stories, with captions written in your brand's voice.

## What it can post

- Image posts
- Carousels
- Reels and trial reels
- Stories
- Collaborators and people tags

## Limits

- Up to 20 images in a carousel
- Reels and trial reels from your own videos
- Stories, collaborators and people tags

Source: [Instagram API docs](https://developers.facebook.com/docs/instagram-platform/instagram-graph-api/reference/ig-user/media).

## Good to know

- **What it posts.** Image posts, carousels, Reels, trial reels, Stories, collaborators and people tags.
- **Caption limits.** 2,200 characters, up to 5 hashtags and 20 @ tags per caption.
- **Professional accounts.** Instagram lets apps publish only to business and creator accounts.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Instagram under **Add a channel**.
2. Sign in with Instagram and approve Skryvo. The account must be a business or creator account; a personal one is switched in Instagram's own settings.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Instagram when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Instagram before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Instagram's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Instagram posts need at least one image | Instagram takes no text-only post. | Add a picture, a carousel or your video. |
| Instagram could not process the image | Instagram refused the picture file. | Replace the picture, then try again. |
| Instagram needs reconnecting | The access you gave Skryvo ended or was revoked on Instagram. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when Instagram refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Instagram did not accept the post | Instagram refused it without a reason Skryvo can name. | Check the post against the limits above and on Instagram, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread.

The channel's marketing page, with its questions and the platform's own scheduling: [Instagram on Skryvo](https://skryvo.ai/channels/instagram/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/instagram/

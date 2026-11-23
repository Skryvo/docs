# Facebook Page

> What Skryvo posts to Facebook Page, its limits, how to connect it, and why a post can fail.

Sign in with Facebook, pick the Pages you manage, and schedule posts with images, your videos and Reels, Stories and link posts on one calendar with your other channels.

## What it can post

- Posts
- Images
- Your videos and Reels
- Stories
- Link posts

## Limits

- Images, link posts and Stories
- Your videos up to 45 minutes, Reels up to 90 seconds
- Pages you manage, not personal profiles

These are the limits Skryvo writes and checks to.

## Good to know

- **What it posts.** Page posts with images or your video, Reels, Stories and link posts.
- **Pages, not profiles.** Meta lets apps publish to Pages only; a personal profile is posted to by hand.
- **Reels from tall clips.** A tall video of 3 to 90 seconds goes out as a Reel; any other video is a Page video of up to 45 minutes.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Facebook Page under **Add a channel**.
2. Sign in with Facebook, approve Skryvo, then tick the Pages it may post to.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Facebook Page when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Facebook Page before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

A personal Facebook profile cannot be connected: Meta lets apps publish only to Pages.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Facebook Page's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| A Facebook story needs a picture or a video. | A story is one picture or one tall clip. | Add a picture or a clip, or post it as a Page post. |
| Facebook did not return the post | Facebook took the request but gave back no post. | Check the Page; post again only if it is not there. |
| Facebook Page needs reconnecting | The access you gave Skryvo ended or was revoked on Facebook Page. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when Facebook Page refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Facebook Page did not accept the post | Facebook Page refused it without a reason Skryvo can name. | Check the post against the limits above and on Facebook Page, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread.

The channel's marketing page, with its questions and the platform's own scheduling: [Facebook Page on Skryvo](https://skryvo.ai/channels/facebook/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/facebook/

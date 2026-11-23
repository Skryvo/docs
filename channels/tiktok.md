# TikTok

> What Skryvo posts to TikTok, its limits, how to connect it, and why a post can fail.

Sign in with TikTok and schedule photo posts or the videos you upload, with captions written in your brand's voice. Every post carries your own choice of audience, comments, Duet, Stitch and commercial disclosure.

## What it can post

- Photo posts
- Your videos
- Your audience, comment, Duet, Stitch and disclosure choices

## Limits

- Up to 35 photos, or your video up to 10 minutes
- 2,200-character captions
- Your audience choice on every post

These are the limits Skryvo writes and checks to.

## Good to know

- **Photos or your video.** Up to 35 photos in a photo post, or one video you upload; Skryvo makes no AI video.
- **Your audience choice.** You choose who can see each post, as TikTok requires.
- **Comments, Duet, Stitch and disclosure.** Turn each on or off and mark branded or promotional posts, post by post.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose TikTok under **Add a channel**.
2. Sign in with TikTok and approve Skryvo. TikTok shows its consent page every time, even when you are signed in.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for TikTok when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from TikTok before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

Skryvo does not read TikTok post results yet; posting is not affected.

## Why a post can fail

A post that does not go out is marked failed on the calendar with TikTok's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Choose who can see this TikTok post first | TikTok requires the creator to choose the audience of every post, and Skryvo sets no default. The post is held until it has one. | Open the post and choose the audience in its TikTok panel. |
| TikTok's daily posting limit for this account is reached. Try again tomorrow. | TikTok caps how many posts an account makes in a day. | Try again the next day. |
| That audience isn't available on this account any more. Choose who can see the post again. | The account's privacy changed after the post was scheduled. | Choose the audience again. |
| TikTok has paused posting on this account. | TikTok stopped the account from posting. | Check the account in TikTok. |
| TikTok needs reconnecting | The access you gave Skryvo ended or was revoked on TikTok. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when TikTok refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| TikTok did not accept the post | TikTok refused it without a reason Skryvo can name. | Check the post against the limits above and on TikTok, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread. Every TikTok post needs `tiktok_privacy`, chosen by the person (over REST, `tiktok.privacy`).

The channel's marketing page, with its questions and the platform's own scheduling: [TikTok on Skryvo](https://skryvo.ai/channels/tiktok/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/tiktok/

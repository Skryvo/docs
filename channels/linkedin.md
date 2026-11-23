# LinkedIn

> What Skryvo posts to LinkedIn, its limits, how to connect it, and why a post can fail.

Connect your LinkedIn profile, write or ask your AI agent for a post, and pick a time. Skryvo publishes it through LinkedIn's own API and reads it back to confirm it is live.

## What it can post

- Text posts
- Up to 20 images
- Swipeable documents
- Your videos
- Comments
- Reposts

## Limits

- Up to 3,000 characters per post
- Up to 20 images, a swipeable document, or one video
- Company Pages are in LinkedIn's review

Source: [LinkedIn Help](https://www.linkedin.com/help/linkedin/answer/a528176).

## Good to know

- **Your profile today, Pages after review.** Personal profiles post today. Company Page posting is built and waits for LinkedIn to approve our app for Pages.
- **Official API only.** Skryvo posts through LinkedIn's API with the access you approve. It never drives your browser, which LinkedIn's terms forbid.
- **3,000 characters, 20 images or a video.** Each post is written to LinkedIn's 3,000-character limit, with up to 20 images, those images as one swipeable document, or your own video of up to 30 minutes.
- **Comments at their own time.** Add up to five comments under a post, each going out when you choose, from your profile or another LinkedIn account you connect.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose LinkedIn under **Add a channel**.
2. Sign in with LinkedIn and approve Skryvo. Your personal profile is connected.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for LinkedIn when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from LinkedIn before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

## Why a post can fail

A post that does not go out is marked failed on the calendar with LinkedIn's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| LinkedIn did not accept the document | Two or more pictures go as one swipeable document, and LinkedIn refused the file. | Post the pictures as images instead, or try again. |
| LinkedIn didn't confirm a part of the video | A part of the upload did not arrive. | Try again; the video is sent in parts again. |
| LinkedIn needs reconnecting | The access you gave Skryvo ended or was revoked on LinkedIn. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when LinkedIn refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| LinkedIn did not accept the post | LinkedIn refused it without a reason Skryvo can name. | Check the post against the limits above and on LinkedIn, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread.

The channel's marketing page, with its questions and the platform's own scheduling: [LinkedIn on Skryvo](https://skryvo.ai/channels/linkedin/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/linkedin/

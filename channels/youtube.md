# YouTube

> What Skryvo posts to YouTube, its limits, how to connect it, and why a post can fail.

Upload your own videos and Shorts to your YouTube channel at the time you pick, with a title, description, privacy setting and your cover as the thumbnail.

## What it can post

- Your videos and Shorts
- Title, description and privacy
- Your cover as the thumbnail

## Limits

- Titles up to 100 characters
- Descriptions up to 5,000 bytes
- Your videos and Shorts, up to 12 hours

Source: [YouTube Data API docs](https://developers.google.com/youtube/data/reference/rest/v3/videos).

## Good to know

- **What you can post.** Your videos and Shorts, with title, description, privacy, made-for-kids and your cover as the thumbnail.
- **Your video, our words.** Skryvo makes no AI video; it writes everything around the one you upload.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose YouTube under **Add a channel**.
2. Sign in with Google, approve Skryvo and pick your channel.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for YouTube when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from YouTube before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

## Why a post can fail

A post that does not go out is marked failed on the calendar with YouTube's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| YouTube posts only videos. Add your clip | A YouTube post is your own video. | Attach your video. |
| Say whether this video is made for kids first. | YouTube requires the choice on every upload. | Choose it in the post's YouTube panel. |
| YouTube didn't accept the video. | YouTube refused the file; a channel that is not verified takes videos of up to 15 minutes. | Check the video's length and format, or verify the channel on YouTube. |
| YouTube needs reconnecting | The access you gave Skryvo ended or was revoked on YouTube. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when YouTube refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| YouTube did not accept the post | YouTube refused it without a reason Skryvo can name. | Check the post against the limits above and on YouTube, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread. Upload the video with [`add_video`](https://skryvo.ai/docs/tools/add-video/) and [`finish_video`](https://skryvo.ai/docs/tools/finish-video/), then pass `by_channel.<id>.video_id` and `youtube.made_for_kids`.

The channel's marketing page, with its questions and the platform's own scheduling: [YouTube on Skryvo](https://skryvo.ai/channels/youtube/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/youtube/

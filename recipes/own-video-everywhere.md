# Your own video on several channels

> Upload one video of your own and post it to several channels, each with its own words and settings.

Skryvo makes no video. This recipe posts a video you made.

## What you get

One upload, then a post per channel carrying it, each with its own caption, and on YouTube its own title.

## What it costs

The upload is free and counts against the plan's video storage. A caption Skryvo writes is 1 generation per batch of platforms; your own words use none.

## Steps

1. **Open an upload.** [`add_video`](https://skryvo.ai/docs/tools/add-video/) with `name`, `size` in bytes and `mime` (`video/mp4` or `video/quicktime`, up to 1 GB). The reply holds an `id` and an `upload_url`.
2. **Send the file** with an HTTP PUT to `upload_url`.
3. **Finish it.** [`finish_video`](https://skryvo.ai/docs/tools/finish-video/) with the `video_id`. A file Skryvo cannot read is refused with the reason.
4. **Write the captions.** [`write_post`](https://skryvo.ai/docs/tools/write-post/), or your own words.
5. **Schedule.** [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) with `by_channel`, giving each channel its own `text` and the `video_id`. YouTube also needs `title` and `youtube.made_for_kids`; TikTok needs the audience the person chose.

```bash
curl -X PUT "$UPLOAD_URL" -H "Content-Type: video/mp4" --data-binary @launch.mp4
```

Each platform has its own size and length limits, and Skryvo holds a video a platform would refuse before it is sent. The numbers are on each [channel page](https://skryvo.ai/docs/channels/).

## What a person approves

Each channel's caption and settings, and on TikTok the audience, before scheduling.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/recipes/own-video-everywhere/

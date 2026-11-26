# Tumblr

> What Skryvo posts to Tumblr, its limits, how to connect it, and why a post can fail.

Sign in with Tumblr, pick the blogs you post to, and schedule text and picture posts on one calendar with your other channels. Your hashtags go out as the post's Tumblr tags.

## What it can post

- Text posts
- Up to 10 pictures
- Your hashtags as Tumblr tags

## Limits

- Up to 10 pictures a post
- Your hashtags as up to 30 tags
- The blogs you can post to

Source: [Tumblr API docs](https://github.com/tumblr/docs/blob/master/npf-spec.md).

## Good to know

- **Tags, not hashtags.** Tumblr is followed and searched by tag, so the hashtags in your post go out as its tags.
- **One account per blog.** Each blog you pick is its own account, so the calendar names the blog a post goes to.
- **Likes and reblogs.** Results count each post's likes, reblogs and replies from Tumblr's notes.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Tumblr under **Add a channel**.
2. Sign in with Tumblr and approve Skryvo, then tick the blogs it may post to. Each blog is its own connection.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Tumblr when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Tumblr before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

The hashtags in a post go out as its Tumblr tags, and a line of only hashtags leaves the words. Results count likes, reblogs and replies from the post's notes.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Tumblr's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| A Tumblr post needs words or a picture | The post was empty once its hashtags became tags. | Add words or a picture. |
| This Tumblr blog reached its daily post limit. Post again tomorrow. | Tumblr allows 250 posts a day per account. | Move the post to tomorrow. |
| Tumblr's daily picture limit for this account is reached. Post again tomorrow. | Tumblr caps the pictures an account uploads each day. | Move the post to tomorrow, or send it without pictures. |
| Tumblr needs reconnecting | The access you gave Skryvo ended or was revoked on Tumblr. | Settings › Connected Accounts › **Reconnect**. Skryvo renews access before it lapses and, when Tumblr refuses it, renews once and sends again before the post stops. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Tumblr did not accept the post | Tumblr refused it without a reason Skryvo can name. | Check the post against the limits above and on Tumblr, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns this account's id and `can`: its word limit, required media, video limits, thread length, polls, comments, how a link appears, its own options and what the person must choose on each post. Read `can` at run time rather than hard-coding these rules. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) takes the account's id in `channel_ids`; `by_channel` gives it its own text, picture, video, options or thread.

The channel's marketing page, with its questions and the platform's own scheduling: [Tumblr on Skryvo](https://skryvo.ai/channels/tumblr/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/tumblr/

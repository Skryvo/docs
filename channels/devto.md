# Publish to Dev.to

> What Skryvo posts to Dev.to, its limits, how to connect it, and why a post can fail.

Paste your Dev.to API key and publish articles there as markdown with a cover image and tags. When the article went to your own blog first, the Dev.to copy points back to it.

## What it can post

- Articles with a canonical link to your own site

## Limits

- Articles in markdown
- Up to 4 tags
- Canonical link to your own post

These are the limits Skryvo writes and checks to.

## Good to know

- **Canonical link.** An article that lives on your own site first carries a canonical link, so search engines credit the original.
- **Markdown and four tags.** Articles are written in markdown with up to four tags, Dev.to's limit.
- **An API key you control.** Paste a key from your Dev.to settings and revoke it there whenever you like.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Dev.to under **Add a channel**.
2. Create an API key in your Dev.to settings and paste it in Skryvo. Revoke it there whenever you like.
3. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Dev.to when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Dev.to before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

Dev.to cannot schedule, so Skryvo holds the article on its calendar and publishes it at the time. Sent to WordPress and Dev.to together, Dev.to goes 15 minutes later so its canonical link credits your site.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Dev.to's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Dev.to rejected that API key. Create a new one and reconnect. | The key was revoked or mistyped. | Create a new key and reconnect. |
| That Dev.to key can't publish articles. | The key lacks the right to publish. | Create a key that can publish. |
| This article is already on Dev.to. | Dev.to refuses the same article twice. | Edit the article on Dev.to instead. |
| Dev.to needs reconnecting | The connection was removed or revoked on Dev.to. | Settings › Connected Accounts › **Reconnect**. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Dev.to did not accept the post | Dev.to refused it without a reason Skryvo can name. | Check the post against the limits above and on Dev.to, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns the site with `kind: "blog"` and its id. Articles go through [`publish_article`](https://skryvo.ai/docs/tools/publish-article/); `original_url` sets the canonical link.

The channel's marketing page, with its questions and the platform's own scheduling: [Dev.to on Skryvo](https://skryvo.ai/channels/devto/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/devto/

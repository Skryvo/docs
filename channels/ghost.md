# Publish to Ghost

> What Skryvo posts to Ghost, its limits, how to connect it, and why a post can fail.

Connect your Ghost site with the Admin API key of a custom integration. Skryvo publishes articles with their pictures uploaded to your site, tags, excerpt and search fields, now or at the time you set.

## What it can post

- Articles with pictures, tags and search fields

## Limits

- Articles with pictures uploaded to your site
- Tags, excerpt, search title and share picture
- Publish now, schedule or send as a draft

These are the limits Skryvo writes and checks to.

## Good to know

- **Pictures on your own site.** Pictures are uploaded to your Ghost site, so the post never depends on Skryvo's links.
- **Credited as the original.** A Dev.to copy follows 15 minutes later with a canonical link to your Ghost post.
- **A key you control.** Delete the integration in Ghost to end Skryvo's access.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose Ghost under **Add a channel**.
2. In Ghost Admin, open **Settings › Integrations**, add a custom integration and copy its Admin API key.
3. Paste your site's HTTPS address and the key in Skryvo. Delete the integration in Ghost whenever you want to end Skryvo's access.
4. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for Ghost when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from Ghost before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

Pictures are uploaded to your Ghost site, so the post never depends on Skryvo's links. Sent to Ghost and Dev.to together, Dev.to goes 15 minutes later so its canonical link credits your Ghost post.

## Why a post can fail

A post that does not go out is marked failed on the calendar with Ghost's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| Ghost rejected the Admin API key. | The integration was deleted or its key regenerated. | Copy the integration's key again and reconnect. |
| No Ghost Admin API at this address. Check the site's address. | The address does not lead to a Ghost site. | Reconnect with the site's exact HTTPS address. |
| The site redirected the request. Use your Ghost admin's exact HTTPS address. | The address differs from the site's own, for example with or without www. | Reconnect with the address your Ghost admin uses. |
| Ghost needs reconnecting | The connection was removed or revoked on Ghost. | Settings › Connected Accounts › **Reconnect**. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| Ghost did not accept the post | Ghost refused it without a reason Skryvo can name. | Check the post against the limits above and on Ghost, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns the site with `kind: "blog"` and its id. Articles go through [`publish_article`](https://skryvo.ai/docs/tools/publish-article/) with the site's channel id; `as_draft` sends it to Ghost as a draft.

The channel's marketing page, with its questions and the platform's own scheduling: [Ghost on Skryvo](https://skryvo.ai/channels/ghost/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/ghost/

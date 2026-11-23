# WordPress and WordPress.com

> What Skryvo posts to WordPress, its limits, how to connect it, and why a post can fail.

One page for both kinds of WordPress. Approve Skryvo on your self-hosted site's application-password page, or sign in with WordPress.com, then publish or schedule articles as proper blocks with their images and categories.

## What it can post

- Articles

## Limits

- Articles only
- Blocks, media, categories and tags
- Self-hosted WordPress and WordPress.com

These are the limits Skryvo writes and checks to.

## Good to know

- **Both kinds of WordPress.** Self-hosted WordPress and WordPress.com are both live; only the way you connect differs.
- **No plugin.** Skryvo uses WordPress's built-in REST API with an application password you approve on your own site.
- **Blocks, ready to edit.** Articles arrive as blocks, with media, categories and tags, ready to edit in your editor.
- **On time without visitors.** A self-hosted site's own scheduled posts wait for a visit to run WP-Cron; Skryvo publishes at the time itself.

## Connect it

1. In Skryvo, open **Settings › Connected Accounts** and choose WordPress under **Add a channel**.
2. Self-hosted WordPress: enter your site's exact HTTPS address, then approve Skryvo on your site's application-password page, signed in as an Author, Editor or Administrator. No plugin is needed.
3. WordPress.com: sign in with WordPress.com and approve Skryvo for one site.
4. On the account's card, **Choose brands** sets which brands it posts for, and **Make default** makes it the account a brand uses for WordPress when it has more than one.

An account the sign-in reaches is connected at once. When it reaches several, such as Pages or locations, Skryvo lists them and connects only the ones you tick. **Add another** connects a second account of the same kind.

## The live check

After a post goes out, Skryvo reads it back from WordPress before it counts as published, and keeps its link. A post that went out but could not be read back stays published and is marked as not verified, so you can check it there.

An article brought in from an address on the connected site can update that post; sent anywhere else, it goes as a draft.

## Why a post can fail

A post that does not go out is marked failed on the calendar with WordPress's reason, and its author and the workspace owner get a notice and an email (the email can be turned off in Settings). Fix the cause, then press **Try again** on the post.

| What the post says | Why | What to do |
|---|---|---|
| WordPress rejected the username or application password. | The application password was revoked on the site. | Reconnect and approve Skryvo again. |
| This WordPress account isn't allowed to publish (needs Author or Editor). | The approving user's role cannot publish. | Reconnect as a user with Author, Editor or Administrator. |
| The site redirected the request. | The address differs from the site's own, for example with or without www. | Reconnect with the site's exact canonical HTTPS address. |
| WordPress REST API not found here | The site's REST API at /wp-json is off or blocked. | Turn the REST API on, or allow it in the security plugin. |
| That account isn't a blog. Choose a WordPress site. | The WordPress.com account has no site of its own. | Create a site on WordPress.com, then connect again. |
| WordPress needs reconnecting | The connection was removed or revoked on WordPress. | Settings › Connected Accounts › **Reconnect**. |
| One of the post's images could not be read | A picture's link no longer answers. | Replace the picture in the post. |
| WordPress did not accept the post | WordPress refused it without a reason Skryvo can name. | Check the post against the limits above and on WordPress, then try again. |

## From an AI agent

[`list_channels`](https://skryvo.ai/docs/tools/list-channels/) returns the site with `kind: "blog"` and its id. Articles go through [`publish_article`](https://skryvo.ai/docs/tools/publish-article/) with the site's channel id; a blog never takes a social post.

The channel's marketing page, with its questions and the platform's own scheduling: [WordPress on Skryvo](https://skryvo.ai/channels/wordpress/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/channels/wordpress/

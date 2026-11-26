# Publishing and the live check

> How a scheduled post goes out on time, how Skryvo checks it went live, and what happens when it cannot.

A scheduled post with **Post it for me** on is published by Skryvo at its time, through the platform's own API, to the account you picked. Then Skryvo reads it back from the platform to confirm it is live.

## Connect an account

Open **Settings › Connected Accounts** and choose a tile under **Add a channel**. Sign in on the platform's page and approve. Where a sign-in reaches several accounts, such as Facebook Pages or Business Profile locations, you pick which to connect. Each channel page says how it connects: see [Channels](https://skryvo.ai/docs/channels/).

Then pick which brands each account posts for, under the brand's **Channels**.

## How a post goes out

1. You schedule it, with **Post it for me** on, to one account. Skryvo never falls back to another account.
2. Two minutes before its time, it reads **Going out now** and edits wait.
3. A sweep every five minutes publishes what is due, on the quarter hour.
4. Skryvo reads the post back from the platform. A post counts as live only once it is read back. Slack's webhook returns no post to read, so Slack's own answer is the confirmation.
5. The post shows **Posted** with its link, and results start an hour later. See [Results](https://skryvo.ai/docs/using/results/).

With **Post it for me** off, or on a channel with no connected account, Skryvo emails you a reminder before it is due and you post it yourself; **I posted it** with the post's link connects its results.

## After it posts

Up to five comments can go out at their own times after a post. On X, Bluesky, Mastodon and Threads they form a thread; on Instagram, Facebook and LinkedIn each answers the post. On X, Bluesky and LinkedIn, a comment or a repost can come from another of your accounts on the same network. These run only where the platform's permissions allow; where a platform has yet to approve them, the app says so.

## Articles

A finished article goes to WordPress, WordPress.com, Ghost, Blogger or Dev.to from **Publish article**: tick one site or several, then **Publish now** (a draft first, by default) or **Schedule**. When an article goes to WordPress and Dev.to, WordPress goes first and Dev.to follows 15 minutes later with a canonical link to the WordPress post.

## Why a post did not go out

| What you see | Why | The fix |
|---|---|---|
| Didn't post, with the platform's reason | The platform refused it | Change what it names, then **Try again** |
| Needs a picture or clip | Instagram, TikTok and Pinterest take no post without a picture or a video | Add one, then schedule it |
| Reconnect before a day | The account's access ends soon | **Reconnect** in Connected Accounts |
| The X post stops | The month's X posts are used up | Other channels keep posting; X posts again next month |
| Waiting for approval | The brand needs approval | A reviewer decides in [Approvals](https://skryvo.ai/docs/using/approvals/) |

Skryvo renews each account's access before it lapses. A post refused for access is renewed and sent once more before it stops. Each channel's own reasons and fixes are on its [channel page](https://skryvo.ai/docs/channels/).

## From an agent

[`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) schedules one post per channel; [`list_scheduled_posts`](https://skryvo.ai/docs/tools/list-scheduled-posts/) shows each post's status, `posted_url` and any `publish_error`. [`publish_article`](https://skryvo.ai/docs/tools/publish-article/) sends an article to a blog.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/using/publishing/

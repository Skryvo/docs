# One article on WordPress and Dev.to

> Publish an article to your WordPress site first, then to Dev.to with a canonical link back to it.

## What you get

The article on your own site, and a copy on Dev.to whose canonical link names your site's post as the original, so search engines credit your site.

## What it costs

Publishing is free. Writing the article, if Skryvo writes it, is 2 generations.

## In the app

Open the article, press **Publish article**, tick your WordPress site and Dev.to, and schedule. Skryvo sends WordPress first and Dev.to 15 minutes later, with the canonical link set to the WordPress post.

## With an agent or the API

1. [`publish_article`](https://skryvo.ai/docs/tools/publish-article/) with the `article_id`, the WordPress `channel_id` and a time `at`.
2. Once it is out, [`article_results`](https://skryvo.ai/docs/tools/article-results/) lists where it went, each with its link.
3. [`publish_article`](https://skryvo.ai/docs/tools/publish-article/) again with the Dev.to `channel_id` and `original_url` set to the WordPress post's address.

`as_draft: true` sends it to the blog now as a draft to review there, and returns its edit link. Connecting each blog: [WordPress](https://skryvo.ai/docs/channels/wordpress/) and [Dev.to](https://skryvo.ai/docs/channels/devto/).

## What a person approves

The article, each blog and the time.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/recipes/article-to-wordpress-and-devto/

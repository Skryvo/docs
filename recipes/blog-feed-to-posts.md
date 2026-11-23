# A blog feed becomes posts

> Each new article on your own blog becomes a post per channel in the brand's voice, scheduled after a yes.

Skryvo does not watch feeds itself. A small automation watches your blog's feed and hands each new article to Skryvo through the REST API; [n8n](https://skryvo.ai/docs/automate/n8n/), [cron](https://skryvo.ai/docs/automate/cron/) or any tool that can make an HTTP call will do.

## What you get

Each new article brought into Skryvo as your own, then one post per platform written from it, keeping its facts and linking back to it.

## What it costs

Bringing an article in uses no generation and no AI: it counts against the month's article imports (50 on Hobby, 200 on Pro, 500 on Enterprise). The posts use 1 generation per article, whatever the number of platforms; how many platforms one call covers follows the plan.

## Steps

1. **Bring it in.** [`import_article`](https://skryvo.ai/docs/tools/import-article/) with `url` set to the new article and `is_mine: true`. Only call it for articles that are yours to publish; that is what `is_mine` says.
2. **Write the posts.** [`repurpose_article`](https://skryvo.ai/docs/tools/repurpose-article/) with the returned `article_id` and the `platforms` you post to.
3. **Show them.** Send the posts to the person (an email, a chat message, or the Skryvo calendar).
4. **Schedule.** On their yes, [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) with each post's `text`, the `channel_ids` from [`list_channels`](https://skryvo.ai/docs/tools/list-channels/), and `link` set to the article.

```bash
curl -X POST https://api.skryvo.ai/api/v1/agent/articles/import \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"is_mine": true, "url": "https://example.com/blog/our-new-week-view/"}'
```

## What a person approves

Each post before it is scheduled. To skip the approval, an automation would have to schedule without asking; Skryvo's tools tell agents to ask, and these docs recommend the same for scripts.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/recipes/blog-feed-to-posts/

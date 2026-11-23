# A release note becomes a campaign

> One release page becomes a researched article, a post per channel and a newsletter draft in the brand's voice.

## What you get

- A researched article about the release, with its claims checked against the release page and other sources.
- One post per platform, written from the finished article and keeping its facts.
- A newsletter email draft: subject lines, a preheader, the body and a call to action.

## What it costs

2 generations for the article, plus image credits for any pictures; 1 generation for all the posts; 1 generation for the email. The article plan is free. Nothing is published or sent until you say so.

## In the app

1. In **Generate Content**, choose **Blog post**, give the release as the topic and add the release page's address as a source.
2. Read the plan: the headline, the search phrase, the outline and the questions only you can answer. Answer them and write the article.
3. When it is done, read its checked claims, then **Repurpose** it to the platforms you want.
4. In **Generate Content**, choose **Email**, pick a newsletter or an announcement, and describe the release and who it is for.

## With an agent or the API

| Step | Tool | What to pass |
|---|---|---|
| 1. Plan | [`plan_article`](https://skryvo.ai/docs/tools/plan-article/) | `topic`, and `sources` with the release page (up to 3 pages) |
| 2. Write | [`write_article`](https://skryvo.ai/docs/tools/write-article/) | `plan_id`, the chosen `headline`, the person's `answers` |
| 3. Wait | [`article_status`](https://skryvo.ai/docs/tools/article-status/) | `article_id`, about once a minute until `done` |
| 4. Posts | [`repurpose_article`](https://skryvo.ai/docs/tools/repurpose-article/) | `article_id`, `platforms` |
| 5. Email | [`write_email`](https://skryvo.ai/docs/tools/write-email/) | `about`, `email_type: "newsletter"` or `"announcement"` |

```bash
curl -X POST https://api.skryvo.ai/api/v1/agent/articles/plan \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"topic": "What is new in version 2.4", "sources": ["https://example.com/changelog/2-4/"]}'
```

## What a person approves

The plan and its answers before the article is written, and each post before [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/). The email is a draft: Skryvo sends nothing.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/recipes/release-note-campaign/

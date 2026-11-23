# A weekly results report

> Every Monday, a script reads how last week's posts and articles did and sends the numbers where your team reads.

## What you get

Reach, engagement and clicks per channel, the best posting times, what stood out and the top posts for the last 7 days, plus how each published article is doing.

## What it costs

Nothing: reading results is free.

## Steps

1. [`post_results`](https://skryvo.ai/docs/tools/post-results/) with `days: 7` (or 30 or 90), and a `brand_id` for one brand.
2. [`find_content`](https://skryvo.ai/docs/tools/find-content/) with `kind: "article"` lists the articles; [`article_results`](https://skryvo.ai/docs/tools/article-results/) gives each one's links, reach and clicks, and its Google search numbers when Search Console is connected.
3. Post the summary to your team's channel or inbox from the script. Running it on a schedule: [cron and CI](https://skryvo.ai/docs/automate/cron/).

```bash
curl "https://api.skryvo.ai/api/v1/agent/results?days=7" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

Numbers are read from each platform at 1 hour, 24 hours and 7, 30, 60 and 90 days after a post goes out, so last week's newest posts are still filling in. Some platforms give no numbers; see [Known limits](https://skryvo.ai/docs/trust/known-limits/).

## What a person approves

Nothing: this recipe only reads.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/recipes/weekly-results-report/

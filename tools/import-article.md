# Import an article

> Brings your own article in from text or a public address, once you say it is yours to publish. Free, within your plan's monthly limit.

| | |
|---|---|
| MCP tool | `import_article` |
| REST route | `POST /api/v1/agent/articles/import` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free, within the plan's monthly article imports. |

## What it does

Brings the person's own article into Skryvo from `text` (markdown or HTML) or a public `url`, one of the two. Free within the plan's monthly allowance. `is_mine` is the person saying it is theirs to publish; ask them first. Every article route then takes its `article_id`. An article from a live address goes to a blog only as a draft or as an update of that post.
Headings, lists, tables, links and pictures come with it.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `is_mine` | boolean | Yes | The person saying the article is theirs to publish; ask them first. |
| `text` | string | No | The article as markdown or HTML, at most 60,000 characters. |
| `url` | string | No | A public address to read the article from, instead of text. |
| `title` | string | No | Omitted, the title Skryvo reads from the article. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |

## Example

An agent calls `import_article` with these arguments:

```json
{
  "is_mine": true,
  "url": "https://northside.coffee/blog/first-year"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/articles/import" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "is_mine": true,
  "url": "https://northside.coffee/blog/first-year"
}'
```

The reply:

```json
{
  "article_id": "gen_c0ffee",
  "status": "done",
  "title": "Our first year",
  "receipt": {
    "headings": 5,
    "pictures": 2,
    "tables": 0,
    "links": 4,
    "words": 980
  },
  "left_out": {}
}
```

## What it costs

Free, within the plan's monthly article imports. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/import-article/

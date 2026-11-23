# Plan an article

> Researches and plans an article: headlines, search phrase, outline, sources and questions only the author can answer. Free; one of the month's plans.

| | |
|---|---|
| MCP tool | `plan_article` |
| REST route | `POST /api/v1/agent/articles/plan` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. Uses one of the month's article plans, given back if planning fails. |

## What it does

Researches and plans a blog article about `topic` in the brand's voice: headline and alternatives, the search phrase it aims at, the outline, sources and the facts found in them, up to three questions only the author can answer, the brand's articles it would clash with, and the picture plan. Free; uses one of the month's article plans and takes about a minute. Returns `status: confirm` with every setting, where it came from and what writing it will cost. Show the plan and ask its questions before writing.

With `callback_url` the call answers 202 at once with a job; the work runs as it would have, charged and refunded the same way, and its answer (or refusal) is posted to `callback_url` as `job.done` or `job.failed`, signed with the job's `secret` like a webhook and retried the same way. `GET /jobs/{job_id}` reads it meanwhile.
Then write it with [`write_article`](https://skryvo.ai/docs/tools/write-article/).

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `topic` | string | Yes | What it is about, 3 to 200 characters. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |
| `length` | integer | No | Target word count. |
| `tone` | string | No | Omitted, the brand's tone. |
| `style` | string | No | how-to, listicle, comparison, case study, explainer, narrative, opinion, news, review or interview. |
| `language` | string | No | A language code; omitted, the brand's writing language. |
| `audience` | string | No | Who it is for. |
| `point_of_view` | string | No | The point of view to write in. |
| `keywords` | string[] | No | Phrases the person wants to rank for. |
| `must_cover` | string[] | No | Points the article has to make. |
| `only_you` | string | No | Facts only the person knows. |
| `notes` | string | No | Anything else for the writer. |
| `sources` | string[] | No | Up to 3 web pages to read. |

## Example

An agent calls `plan_article` with these arguments:

```json
{
  "topic": "Choosing a coffee grinder for home",
  "length": 1500,
  "tone": "warm"
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/articles/plan" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "topic": "Choosing a coffee grinder for home",
  "length": 1500,
  "tone": "warm"
}'
```

The reply:

```json
{
  "status": "confirm",
  "plan_id": "pl_91ab3e",
  "brand_id": "bv_3c9d0e",
  "headline": "How to choose a coffee grinder for home",
  "other_headlines": [
    "Burr or blade: picking a home grinder"
  ],
  "search_phrase": "best coffee grinder for home",
  "search": {
    "phrase": "best coffee grinder for home",
    "monthly_searches": 5400,
    "difficulty": 31,
    "intent": "commercial",
    "market": "GB",
    "winnable": "Small sites hold three of the first five results.",
    "ideas": []
  },
  "keywords": [
    "best coffee grinder for home"
  ],
  "angle": "A barista's checklist for first-time buyers",
  "outline": [
    {
      "heading": "Burr or blade?",
      "covers": "Why the grind decides taste"
    }
  ],
  "questions": [
    "Which grinder do you use behind your own counter?"
  ],
  "already_written": [],
  "sources": [
    {
      "title": "Grind size guide",
      "url": "https://example.org/grind"
    }
  ],
  "facts": [
    {
      "fact": "Burr grinders give a more even grind.",
      "source": "Example Org",
      "url": "https://example.org/grind"
    }
  ],
  "other_search_phrases": [
    "coffee grinder buying guide"
  ],
  "settings": [
    {
      "field": "word_count",
      "value": 1500,
      "from": "brand"
    }
  ],
  "cost": {
    "generations": 2,
    "image_credits_up_to": 16
  },
  "left": {
    "generations": 41,
    "image_credits": 180,
    "resets_at": "2026-12-01T00:00:00+00:00"
  },
  "differs_from_brand": [],
  "plans_left": 17,
  "expires_at": "2026-11-30T12:00:00+00:00"
}
```

## What it costs

Free. Uses one of the month's article plans, given back if planning fails. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/plan-article/

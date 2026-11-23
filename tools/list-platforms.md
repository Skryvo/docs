# List platforms

> Every channel Skryvo offers, connected or not, and what each one takes.

| | |
|---|---|
| MCP tool | `list_platforms` |
| REST route | `GET /api/v1/agent/platforms` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

Every channel Skryvo can post to, connected or not: its name, social or blog, whether it can be connected today and what it takes. A person connects one in the app under Settings › Connected Accounts.

## Inputs

None.

## Example

An agent calls `list_platforms` with these arguments:

```json
{}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/platforms" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "platforms": [
    {
      "platform": "linkedin",
      "name": "LinkedIn",
      "kind": "social",
      "can_connect": true,
      "can": {
        "takes": "posts",
        "words": 3000,
        "title": null,
        "media_required": "none",
        "pictures": true,
        "video": {
          "most_bytes": 524288000,
          "shortest_seconds": 3,
          "longest_seconds": 1800
        },
        "thread_posts": 1,
        "poll": true,
        "comments": true,
        "link": "in the words",
        "options": {
          "as_document": {
            "type": "boolean"
          }
        },
        "must_choose": []
      }
    }
  ]
}
```

## What it costs

Free. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/list-platforms/

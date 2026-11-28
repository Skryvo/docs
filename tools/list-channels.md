# List channels

> Your connected accounts and blog sites, and which brands use each. Inputs, an example and the cost of list_channels for agents and the API.

| | |
|---|---|
| MCP tool | `list_channels` |
| REST route | `GET /api/v1/agent/channels` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | Free. |

## What it does

The accounts the person connected: id, platform, name, the brands that use it, social or blog, whether it needs reconnecting, and `can`: what it takes (word limit, required media, video limits, thread length, polls, comments, how a link appears, its own post options and what the person must choose on every post). Read `can` at run time rather than hard-coding a platform's rules.

## Inputs

None.

## Example

An agent calls `list_channels` with these arguments:

```json
{}
```

A script makes the same call over REST with an API key:

```bash
curl "https://api.skryvo.ai/api/v1/agent/channels" \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

The reply:

```json
{
  "channels": [
    {
      "id": "conn_8f2e1a",
      "platform": "linkedin",
      "name": "Northside Coffee",
      "brand_ids": [
        "bv_3c9d0e"
      ],
      "kind": "social",
      "needs_reconnect": false,
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

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/list-channels/

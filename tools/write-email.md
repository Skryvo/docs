# Write an email

> Writes a marketing email in the brand's voice.

| | |
|---|---|
| MCP tool | `write_email` |
| REST route | `POST /api/v1/agent/emails` |
| Changes anything | No. It reads, or returns a draft for the person to see. |
| Cost | One generation. |

## What it does

Writes a marketing email in the brand's voice about `about`: subject lines, preheader, markdown body and a call to action. When `email_type` was left out, the call writes nothing and returns `status: confirm` with every setting, where it came from, the cost and what is left. One generation. Nothing is sent.

## Inputs

| Parameter | Type | Required | What it is |
|---|---|---|---|
| `about` | string | Yes | What the email promotes or says, and to whom. |
| `brand_id` | string | No | A brand from list_brands; omitted, the person's default brand. |
| `email_type` | string | No | welcome, promotional, newsletter, follow_up, re_engagement, transactional or announcement. |
| `tone` | string | No | Omitted, the brand's tone. |
| `language` | string | No | A language code; omitted, the brand's writing language. |
| `audience` | string | No | Who it is for. |
| `call_to_action` | string | No | What the reader should do next. |
| `length` | integer | No | Target word count. |
| `confirmed` | boolean | No | true once the person approved the summary. |

## Example

An agent calls `write_email` with these arguments:

```json
{
  "about": "Our new studio opening this Saturday, for local regulars",
  "email_type": "announcement",
  "confirmed": true
}
```

A script makes the same call over REST with an API key:

```bash
curl -X POST "https://api.skryvo.ai/api/v1/agent/emails" \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
  "about": "Our new studio opening this Saturday, for local regulars",
  "email_type": "announcement",
  "confirmed": true
}'
```

The reply:

```json
{
  "status": "written",
  "brand_id": "bv_3c9d0e",
  "generation_id": "gen_e3a1b2",
  "subject_lines": [
    "Our new studio opens Saturday"
  ],
  "preheader": "Free tasting from 9am.",
  "body": "Hi there,\n\nOur new studio opens this Saturday…",
  "call_to_action": "Get directions",
  "settings": [
    {
      "field": "campaign_type",
      "value": "announcement",
      "from": "you"
    }
  ]
}
```

## What it costs

One generation. What a plan includes each month is on [Plans and the trial](https://skryvo.ai/docs/start/plans-and-trial/), and the [`balance`](https://skryvo.ai/docs/tools/balance/) tool says what is left.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/tools/write-email/

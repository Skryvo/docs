# Webhooks

> Get a signed POST when a post is published or fails, an article is ready, or results come in.

Instead of polling, register an HTTPS endpoint and Skryvo POSTs each event to it, signed with the endpoint's secret. Add one in the app or over the API, with a key or OAuth token, so a person, a script or an automation can subscribe.

## Add one in Skryvo

1. Open **Settings › API & agents** and find **Webhooks**.
2. Choose **Add webhook**, enter the **Endpoint address** (it starts with `https://`) and pick the **Events**.
3. Copy the signing secret: Skryvo shows it once and keeps only an encrypted copy.
4. **Send test** sends a sample of each event, and **Recent deliveries** shows how each one went. A paused webhook resumes once a test arrives.

## Events

| Event | When | What `data` holds |
|---|---|---|
| `post.published` | A post went live | A scheduled post or article went out and was read back from the channel. `data` is the post, with `posted_url` set. |
| `post.failed` | A post could not go out | Skryvo stopped trying to publish a post. `data` is the post, with `publish_error` saying why in plain words; the person can fix it and try again in the app. |
| `article.ready` | An article finished writing | An article written through this API finished. Its full text is at `GET /articles/{article_id}`. |
| `article.failed` | An article could not be written | An article written through this API stopped. It was not charged. |
| `results.ready` | New numbers for a published post | A published post's numbers were read at a checkpoint: 1h, 24h, 7d, 30d, 60d or 90d after it went out. A number the platform does not give is null. |

An article scheduled to a blog fires the post events, with the blog's `platform`, such as `wordpress`. `milestone` is `1h`, `24h`, `7d`, `30d`, `60d` or `90d`; a number is null where the platform gives none, and `post_id` is null for a post made outside the calendar. The full text of a ready article comes from [`article_status`](https://skryvo.ai/docs/tools/article-status/).

## The request

```text
POST /your/endpoint
Content-Type: application/json
User-Agent: Skryvo-Webhooks/1.0
Skryvo-Event: post.published
Skryvo-Delivery: dlv_…
Skryvo-Signature: t=1795000000,v1=5257a869e7ecebeda32affa62cdca3fa51cad7e77a0e56ff536d0ce8e108d8bd
```

The body of a `post.published` event:

```json
{
  "id": "evt_6f1d0c9e8b7a6f5e4d3c2b1a",
  "type": "post.published",
  "created": "2026-11-24T09:00:03+00:00",
  "test": false,
  "data": {
    "id": "c1a2b3c4d5",
    "platform": "linkedin",
    "channel_id": "conn_8f2e1a",
    "date": "2026-11-24",
    "time": "09:00",
    "status": "posted",
    "reason": null,
    "awaiting_approval": false,
    "reviewer_approval": null,
    "auto_publish": true,
    "text": "We just opened our new studio in Leeds. Come say hello this Saturday.",
    "topic": "New studio opening",
    "written": true,
    "publish_error": null,
    "posted_url": "https://www.linkedin.com/feed/1",
    "open_in_skryvo": "https://app.skryvo.ai/calendar?date=2026-11-24"
  }
}
```

`id` is the event's id, the same on every endpoint and every retry: use it to skip an event you already handled. `Skryvo-Delivery` names one endpoint's delivery of it. `test` is true only for events sent by the test route.

## Check the signature

`Skryvo-Signature` holds `t`, the time in Unix seconds, and `v1`, the hex HMAC-SHA256 of `<t>.<raw body>`. The key is the whole secret string, `whsec_…`, as UTF-8. Compute it over the body exactly as it arrived, compare in constant time, and reject a `t` more than 5 minutes old.

Node.js:
```javascript
import crypto from 'node:crypto';

// rawBody: the request body exactly as received, before any JSON parsing.
export function verifySkryvo(rawBody, header, secret) {
  const parts = Object.fromEntries(header.split(',').map((p) => p.split('=')));
  const t = Number(parts.t);
  if (!t || Math.abs(Date.now() / 1000 - t) > 300) return false;
  const expected = crypto.createHmac('sha256', secret).update(`${t}.`).update(rawBody).digest();
  const given = Buffer.from(parts.v1 ?? '', 'hex');
  return given.length === expected.length && crypto.timingSafeEqual(given, expected);
}
```

Python:
```python
import hashlib
import hmac
import time


def verify_skryvo(raw_body: bytes, header: str, secret: str) -> bool:
    parts = dict(p.split("=", 1) for p in header.split(","))
    t = int(parts.get("t", "0"))
    if abs(time.time() - t) > 300:
        return False
    expected = hmac.new(secret.encode(), f"{t}.".encode() + raw_body, hashlib.sha256).hexdigest()
    return hmac.compare_digest(expected, parts.get("v1", ""))
```

## Delivery and retries

Answer with any 2xx within 10 seconds. Anything else, or no answer, is tried again after 5 minutes, 30 minutes, 2 hours, 6 hours and 12 hours: six tries over about 21 hours, after which the delivery is `failed`. After 15 failed tries in a row the endpoint is paused and gets no new deliveries; a successful test resumes it.

## Routes

| Route | What it does |
|---|---|
| `GET /webhooks` | The workspace's webhook endpoints, newest first: address, events, whether it is active or paused (and why), the last delivery and the failed tries in a row. The secret is never listed. |
| `POST /webhooks` | Registers an https endpoint on the public internet for one or more events: post.published, post.failed, article.ready, article.failed, results.ready. Returns the endpoint with its signing `secret`, shown this once; store it to verify deliveries. |
| `DELETE /webhooks/{webhook_id}` | Stops every delivery to the endpoint at once. Returns no body. |
| `POST /webhooks/{webhook_id}/test` | Sends a sample of each subscribed event now, with `test: true`, and returns how each delivery went. A test is tried once and never retried; one that lands resumes a paused endpoint. |
| `GET /webhooks/{webhook_id}/deliveries` | The endpoint's deliveries from the last 30 days, newest first, up to 50: event, status (`pending`, `delivered` or `failed`), tries, the endpoint's answer and when the next try is due. |

```bash
curl -X POST https://api.skryvo.ai/api/v1/agent/webhooks \
  -H "Authorization: Bearer $SKRYVO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"url": "https://example.com/skryvo", "events": ["post.published", "post.failed"]}'
```

An endpoint's `url` must be HTTPS on a public address, and `events` one or more of the five. A workspace keeps endpoints up to its plan's limit: 3 on Hobby, 10 on Pro and 25 on Enterprise. Each delivery keeps the event's body for 30 days, so the deliveries route can show it.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/api/webhooks/

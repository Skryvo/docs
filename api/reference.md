# API reference

> Every route of the REST API, grouped by what it works on, each linked to its full page.

Every route lives under `https://api.skryvo.ai/api/v1/agent` and takes a key or token as `Authorization: Bearer`. A route that an agent tool also calls is documented on that tool's page, with its inputs, an example request and reply, and its cost. This page is written from the OpenAPI file at `https://api.skryvo.ai/openapi.json`.

## Account

Who the key belongs to and what the plan still allows.

| Route | What it does | Page |
|---|---|---|
| `GET /me` | Who this key belongs to | Below |
| `GET /jobs/{job_id}` | Read a job | Below |
| `GET /balance` | What this month still allows | [`balance`](https://skryvo.ai/docs/tools/balance/) |
| `POST /defaults` | Keep choices as the brand's defaults | [`keep_defaults`](https://skryvo.ai/docs/tools/keep-defaults/) |

### GET /me

The email of the account the key or token acts for, and its plan.

```json
{
  "email": "sam@example.com",
  "plan": "pro"
}
```

### GET /jobs/{job_id}

Where a call made with `callback_url` is: `running`, `done` with the route's own answer, or `failed` with the status and sentence the route would have answered. A job whose process is lost ends failed within about 15 minutes and is not charged.

```json
{
  "job_id": "job_5e4d3c2b1a09f8e7d6c5b4a3",
  "kind": "pictures",
  "status": "done",
  "answer": {
    "brand_id": "bv_3c9d0e",
    "headline": "Our new studio opens Saturday",
    "pictures": [
      {
        "platform": "linkedin",
        "image_url": "https://media.skryvo.ai/images/u1/p-1200.jpg",
        "width": 1200,
        "height": 1200
      }
    ],
    "credits_used": 4,
    "credits_left": 176
  },
  "error": null,
  "started_at": "2026-11-24T09:00:00+00:00",
  "finished_at": "2026-11-24T09:01:12+00:00"
}
```

## Brands

Brands, their design and the look new pictures wear.

| Route | What it does | Page |
|---|---|---|
| `GET /brands` | List brands | [`list_brands`](https://skryvo.ai/docs/tools/list-brands/) |
| `POST /brands` | Add a brand from its website | [`add_brand`](https://skryvo.ai/docs/tools/add-brand/) |
| `GET /design` | Read a brand's design | [`brand_design`](https://skryvo.ai/docs/tools/brand-design/) |
| `POST /design/look` | Design or keep a brand's look | [`change_look`](https://skryvo.ai/docs/tools/change-look/) |

## Channels

Connected accounts and every channel Skryvo offers.

| Route | What it does | Page |
|---|---|---|
| `GET /channels` | List connected channels | [`list_channels`](https://skryvo.ai/docs/tools/list-channels/) |
| `GET /platforms` | List every channel Skryvo offers | [`list_platforms`](https://skryvo.ai/docs/tools/list-platforms/) |

## Posts

Write, design, schedule, change and review social posts.

| Route | What it does | Page |
|---|---|---|
| `POST /drafts` | Write posts | [`write_post`](https://skryvo.ai/docs/tools/write-post/) |
| `POST /pictures` | Design a picture for a post | [`design_picture`](https://skryvo.ai/docs/tools/design-picture/) |
| `POST /posts` | Schedule a post | [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) |
| `GET /posts` | List scheduled posts | [`list_scheduled_posts`](https://skryvo.ai/docs/tools/list-scheduled-posts/) |
| `PATCH /posts/{post_id}` | Move a post or change its words | [`change_post`](https://skryvo.ai/docs/tools/change-post/) |
| `DELETE /posts/{post_id}` | Cancel a scheduled post | [`cancel_post`](https://skryvo.ai/docs/tools/cancel-post/) |
| `POST /posts/{post_id}/review` | Approve or send back a team post | [`review_post`](https://skryvo.ai/docs/tools/review-post/) |

## Articles

Plan, write, check, improve and publish blog articles.

| Route | What it does | Page |
|---|---|---|
| `POST /articles/plan` | Plan an article | [`plan_article`](https://skryvo.ai/docs/tools/plan-article/) |
| `POST /articles` | Write a planned article | [`write_article`](https://skryvo.ai/docs/tools/write-article/) |
| `GET /articles/{article_id}` | Read an article's progress | [`article_status`](https://skryvo.ai/docs/tools/article-status/) |
| `POST /articles/{article_id}/publish` | Publish an article to a blog | [`publish_article`](https://skryvo.ai/docs/tools/publish-article/) |
| `GET /articles/{article_id}/seo` | Check an article's SEO | [`article_seo`](https://skryvo.ai/docs/tools/article-seo/) |
| `POST /articles/{article_id}/improve` | Improve an article | [`improve_article`](https://skryvo.ai/docs/tools/improve-article/) |
| `POST /articles/import` | Bring in the person's own article | [`import_article`](https://skryvo.ai/docs/tools/import-article/) |
| `POST /articles/{article_id}/posts` | Turn an article into posts | [`repurpose_article`](https://skryvo.ai/docs/tools/repurpose-article/) |

## Calendar

Plan a week or a month of posts.

| Route | What it does | Page |
|---|---|---|
| `POST /calendar/plan` | Plan a week or a month of posts | [`plan_calendar`](https://skryvo.ai/docs/tools/plan-calendar/) |
| `POST /calendar/accept` | Add plan rows to the calendar | [`accept_plan`](https://skryvo.ai/docs/tools/accept-plan/) |

## Writing

Emails, product listings and ad copy.

| Route | What it does | Page |
|---|---|---|
| `POST /ads` | Write ad copy | [`write_ad`](https://skryvo.ai/docs/tools/write-ad/) |
| `GET /content` | Find earlier work | [`find_content`](https://skryvo.ai/docs/tools/find-content/) |
| `POST /emails` | Write an email | [`write_email`](https://skryvo.ai/docs/tools/write-email/) |
| `POST /listings` | Write a product listing | [`write_listing`](https://skryvo.ai/docs/tools/write-listing/) |

## Videos

Upload the person's own videos to post.

| Route | What it does | Page |
|---|---|---|
| `GET /videos` | List ready videos | [`list_videos`](https://skryvo.ai/docs/tools/list-videos/) |
| `POST /videos` | Open a video upload | [`add_video`](https://skryvo.ai/docs/tools/add-video/) |
| `POST /videos/{video_id}/finish` | Finish a video upload | [`finish_video`](https://skryvo.ai/docs/tools/finish-video/) |

## Results

How published posts and articles did.

| Route | What it does | Page |
|---|---|---|
| `GET /results` | How published posts did | [`post_results`](https://skryvo.ai/docs/tools/post-results/) |
| `GET /articles/{article_id}/results` | How an article is doing | [`article_results`](https://skryvo.ai/docs/tools/article-results/) |

## Webhooks

Signed event deliveries to your own HTTPS endpoint.

| Route | What it does | Page |
|---|---|---|
| `GET /webhooks` | List webhooks | Below |
| `POST /webhooks` | Add a webhook | Below |
| `DELETE /webhooks/{webhook_id}` | Delete a webhook | Below |
| `POST /webhooks/{webhook_id}/test` | Send test events | Below |
| `GET /webhooks/{webhook_id}/deliveries` | List recent deliveries | Below |

### GET /webhooks

The workspace's webhook endpoints, newest first: address, events, whether it is active or paused (and why), the last delivery and the failed tries in a row. The secret is never listed. Admins and owners only.

```json
{
  "webhooks": [
    {
      "id": "wh_4b2a91",
      "url": "https://example.com/hooks/skryvo",
      "events": [
        "post.published",
        "post.failed"
      ],
      "status": "active",
      "paused_reason": null,
      "created_at": "2026-11-23T10:00:00+00:00",
      "last_delivery_at": "2026-11-24T09:00:04+00:00",
      "failures": 0
    }
  ]
}
```

### POST /webhooks

Registers an https endpoint on the public internet for one or more events: post.published, post.failed, article.ready, article.failed, results.ready. Returns the endpoint with its signing `secret`, shown this once; store it to verify deliveries. Plans keep up to 1 (free), 3 (hobby), 10 (pro), 25 (enterprise) endpoints a workspace. Each delivery is a POST with `Skryvo-Event`, `Skryvo-Delivery` and `Skryvo-Signature: t=<unix seconds>,v1=<hex HMAC-SHA256>`, where the HMAC is keyed by the whole secret (`whsec_…`) over `<t>.<raw body>`. Compare in constant time and refuse a `t` more than five minutes old. Answer 2xx within 10 seconds; anything else is retried after 5 minutes, 30 minutes, 2, 6 and 12 hours, and an endpoint is paused after 15 failed tries in a row.

```json
{
  "id": "wh_4b2a91",
  "url": "https://example.com/hooks/skryvo",
  "events": [
    "post.published",
    "post.failed"
  ],
  "status": "active",
  "paused_reason": null,
  "created_at": "2026-11-23T10:00:00+00:00",
  "last_delivery_at": null,
  "failures": 0,
  "secret": "whsec_Z3k9…"
}
```

### DELETE /webhooks/{webhook_id}

Stops every delivery to the endpoint at once. Returns no body.

### POST /webhooks/{webhook_id}/test

Sends a sample of each subscribed event now, with `test: true`, and returns how each delivery went. A test is tried once and never retried; one that lands resumes a paused endpoint.

```json
{
  "deliveries": [
    {
      "id": "wh_4b2a91_8235861199999_a1b2c3",
      "event_id": "evt_6f1d0c9e8b7a6f5e4d3c2b1a",
      "type": "post.published",
      "test": true,
      "status": "delivered",
      "attempts": 1,
      "response_status": 200,
      "error": null,
      "created_at": "2026-11-24T09:00:03+00:00",
      "delivered_at": "2026-11-24T09:00:04+00:00",
      "next_attempt_at": null
    }
  ]
}
```

### GET /webhooks/{webhook_id}/deliveries

The endpoint's deliveries from the last 30 days, newest first, up to 50: event, status (`pending`, `delivered` or `failed`), tries, the endpoint's answer and when the next try is due.

```json
{
  "deliveries": [
    {
      "id": "wh_4b2a91_8235861199999_a1b2c3",
      "event_id": "evt_6f1d0c9e8b7a6f5e4d3c2b1a",
      "type": "post.published",
      "test": false,
      "status": "delivered",
      "attempts": 1,
      "response_status": 200,
      "error": null,
      "created_at": "2026-11-24T09:00:03+00:00",
      "delivered_at": "2026-11-24T09:00:04+00:00",
      "next_attempt_at": null
    }
  ]
}
```

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/api/reference/

# A product launch kit

> A marketplace listing, ad copy, a launch email and launch posts for one product, all in the brand's voice.

## What you get

- A product listing shaped for its marketplace: title, description and feature bullets.
- Ad copy for each ad platform you name, in up to 6 variations.
- A launch email: subject lines, preheader, body and a call to action.
- Launch posts, one per platform.

## What it costs

1 generation each for the listing, the ads, the email and the batch of posts: 4 in all. Skryvo runs no ad and sends no email.

## Steps

| Piece | Tool | What to pass |
|---|---|---|
| Listing | [`write_listing`](https://skryvo.ai/docs/tools/write-listing/) | `product`, 1 to 10 `features`, `marketplace` |
| Ads | [`write_ad`](https://skryvo.ai/docs/tools/write-ad/) | `product`, `platforms` such as `google_ads` or `meta_ads`, `goal`, `variations` |
| Email | [`write_email`](https://skryvo.ai/docs/tools/write-email/) | `about`, `email_type: "announcement"` |
| Posts | [`write_post`](https://skryvo.ai/docs/tools/write-post/) | `topic`, up to 4 `platforms` |

When the marketplace or the email type is left out, the first call writes nothing and returns a summary of every setting, where it came from and the cost; call again with `confirmed: true` once the person agrees. In the app the same pieces are under **Generate Content**: **Product description**, **Ad Copy**, **Email** and **Social**.

## What a person approves

The summary before each piece is written, and each post before it is scheduled.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/recipes/product-launch-kit/

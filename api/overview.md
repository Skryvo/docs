# API overview and sign-in

> The REST API's address, its OpenAPI file, signing in with an API key or OAuth, and the first call.

The REST API gives a script, an automation or an AI agent the same account the person uses in the app: their brands, connected channels, plan limits and calendar. Every route takes JSON and returns JSON, and every [agent tool](https://skryvo.ai/docs/tools/) has one.

| | |
|---|---|
| Base address | `https://api.skryvo.ai/api/v1/agent` |
| OpenAPI file | `https://api.skryvo.ai/openapi.json`, version 1.0.0 |
| Sign-in | An API key or an OAuth access token, as `Authorization: Bearer` |
| Rate limit | 60 requests a minute and 1,000 an hour per key or sign-in |

The OpenAPI file covers every route on the [reference](https://skryvo.ai/docs/api/reference/) with a summary, a description, an example and a typed schema for every answer. Tests check each answer the API gives against its schema. A typed client generated from it is published as the [JavaScript and TypeScript SDK](https://www.npmjs.com/package/skryvo), under the MIT licence.

## Sign in with an API key

1. In Skryvo, open **Settings › API & agents** and create a key. It starts with `sk_skryvo_`, is shown once and is stored only as a hash. A person can keep up to 10.
2. Send it on every call:

```bash
curl https://api.skryvo.ai/api/v1/agent/me \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

```json
{
  "email": "sam@example.com",
  "plan": "pro"
}
```

A key opens the agent API and nothing else in the account, and acts in the workspace it was made in, with that member's role and brands. Revoking it in Settings stops it at once.

## Sign in with OAuth

For an app that acts for people other than its maker. Skryvo runs OAuth 2.1 with dynamic client registration and PKCE:

1. Discover the server at `https://api.skryvo.ai/.well-known/oauth-protected-resource` and `https://api.skryvo.ai/.well-known/oauth-authorization-server`.
2. Register at `https://api.skryvo.ai/oauth/register`. A redirect address must be HTTPS, a loopback address or a desktop app's own scheme.
3. Send the person to `https://api.skryvo.ai/oauth/authorize` with an S256 code challenge. Skryvo's consent page names your app and the signed-in account; the person chooses Authorize or Deny.
4. Swap the code at `https://api.skryvo.ai/oauth/token`. A code is single-use and lasts ten minutes. You get an access token (`sko_…`) that lasts 1 hour and a refresh token (`skr_…`) that lasts 90 days and rotates each time it is used. The scope is `skryvo`.

Tokens are stored hashed, like keys, and the person sees your app under Connected apps in Settings › API & agents, where Disconnect stops it at once.

## Times

Times are ISO 8601. A time without an offset is read in the calendar's own time zone, and every post moves to the calendar's next quarter hour.

## Spending, and the summary first

Calls that write or design spend the person's monthly generations or image credits. A call that would rely on a choice the person did not make, such as the platforms or pictures, writes nothing and returns `status: "confirm"` with each setting, where it came from, the cost and what is left. Call again with `confirmed: true` once the person agrees. A cost the balance cannot cover is refused before anything is spent. [How agents use it](https://skryvo.ai/docs/agents/overview/).

## Knowing when a post is out

Skryvo publishes each post at its time and reads it back. Register an HTTPS endpoint and Skryvo POSTs a signed event when a post is published or fails and when an article is ready: [Webhooks](https://skryvo.ai/docs/api/webhooks/). Or poll [`list_scheduled_posts`](https://skryvo.ai/docs/tools/list-scheduled-posts/), which returns each post's `status`, `publish_error` and `posted_url`.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/api/overview/

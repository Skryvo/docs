# How AI agents work with Skryvo

> The MCP server and the REST API, how an agent signs in, and what it does before it spends anything.

An AI agent such as Claude, ChatGPT or Cursor works in a person's Skryvo account through 35 tools. It lists their brands and channels, writes posts and articles in a brand's voice, designs pictures, schedules them and reads how they did. The tools run the same code as the app, so plan limits, brand settings, team roles and each platform's rules apply exactly as they do there.

## Two ways in

| | MCP server | REST API |
|---|---|---|
| For | AI agents | Scripts, CI jobs and automations |
| Address | `https://api.skryvo.ai/mcp` | `https://api.skryvo.ai/api/v1/agent` |
| Speaks | Streamable HTTP, stateless, JSON replies | JSON in, JSON out, one route per tool |
| Signs in with | OAuth sign-in, or an API key | An API key, or an OAuth token |

Every tool has a REST route with the same parameters, so whatever an agent can do, a script can do too. The [agent tools](https://skryvo.ai/docs/tools/) section documents each one, with its route.

## Signing in

- **OAuth.** A client that supports it discovers Skryvo, registers itself and opens Skryvo's consent page, which names the app and the account. The person chooses Authorize. Access tokens last 1 hour and refresh tokens 90 days, rotating on each use.
- **API key.** Made in Skryvo under **Settings › API & agents**, starting `sk_skryvo_`, shown once and stored only as a hash. A person can keep up to 10. The key is sent as `Authorization: Bearer`.

Details for developers are on [API overview](https://skryvo.ai/docs/api/overview/).

## What happens in one request

1. The agent reads the person's brands and connected channels with [`list_brands`](https://skryvo.ai/docs/tools/list-brands/) and [`list_channels`](https://skryvo.ai/docs/tools/list-channels/).
2. [`write_post`](https://skryvo.ai/docs/tools/write-post/) drafts one post per platform in the brand's voice, one generation for the batch. Nothing is scheduled.
3. [`design_picture`](https://skryvo.ai/docs/tools/design-picture/) designs a picture in the brand's kept look, sized for each platform.
4. The agent shows the posts and pictures to the person and waits for their yes.
5. [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) puts one post per channel on the calendar. Skryvo publishes it on the quarter hour and reads it back from the platform to confirm it went live.
6. [`list_scheduled_posts`](https://skryvo.ai/docs/tools/list-scheduled-posts/) shows its status and link, and [`post_results`](https://skryvo.ai/docs/tools/post-results/) how it did.

## A summary before anything is spent

An agent passes only what the person said. Skryvo fills the rest from the brand's saved defaults and profile. When a call would rely on a choice the person did not make, such as which platforms or whether to add pictures, it writes nothing and returns `status: "confirm"`: every setting with where it came from (`you`, `brand`, `brand profile` or `Skryvo default`), the cost in generations and image credits, and what is left this month. The agent shows that as one message and calls again with the person's final values and `confirmed: true`. A cost the balance cannot cover is refused before anything is spent.

When the person's choices differ from the brand's defaults, the reply lists them in `differs_from_brand`, and [`keep_defaults`](https://skryvo.ai/docs/tools/keep-defaults/) saves them on the person's yes.

## In a team

A key acts in the workspace it was made in, and an OAuth sign-in in the team the person picks when they sign in, with that member's role and brands. An editor's post on a brand that needs approval comes back with `awaiting_approval` and waits for a reviewer, who can decide it with [`review_post`](https://skryvo.ai/docs/tools/review-post/). How teams and approvals work in the app: [Teams](https://skryvo.ai/docs/using/teams/) and [Approvals](https://skryvo.ai/docs/using/approvals/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/agents/overview/

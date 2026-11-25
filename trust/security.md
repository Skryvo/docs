# Security

> How Skryvo protects keys, sign-ins, platform access and your account, and how to report a problem.

## Your account

Sign-in runs on Firebase Authentication by Google. With a password, Google stores it hashed and Skryvo never sees it; you can also sign in with Google or Bluesky. Everything travels over HTTPS and is encrypted at rest by Google Cloud.

## Platform access

When you connect a channel, you sign in on the platform's own page and approve what Skryvo may do there. Skryvo keeps the access tokens it is given, each encrypted again with Skryvo's own key before it is stored. Discord and Slack give a channel webhook instead, kept encrypted the same way; no Skryvo bot joins your server or workspace. Disconnecting a channel in Settings deletes its stored token at once. Skryvo posts only through each platform's official API and never drives your browser.

## API keys

- Made in Settings › API & agents. A key starts with `sk_skryvo_`, is shown once, and is stored only as a SHA-256 hash, so Skryvo cannot show it again.
- A person can keep up to 10 keys, and revoking one stops it at once.
- A key opens the agent API and nothing else in the account. In a team it acts in the workspace it was made in, with its maker's role and brands.

## Sign-in for apps (OAuth 2.1)

AI clients that support it connect with a sign-in instead of a key:

1. The client finds Skryvo at `/.well-known/oauth-protected-resource` and `/.well-known/oauth-authorization-server` on api.skryvo.ai and registers itself. Its return address must be HTTPS, a loopback address or a desktop app's own scheme.
2. You see a consent page in Skryvo that names the app and the signed-in account, and choose Authorize or Deny.
3. The code it gets is single-use, lasts ten minutes and is bound to the client, its return address and an S256 challenge.
4. The access token lasts 1 hour; the refresh token lasts 90 days and is replaced each time it is used. Both are stored only as hashes.

Settings › API & agents lists every connected app with Disconnect.

## What an agent can and cannot do

An agent can call only the [35 tools](https://skryvo.ai/docs/tools/), and through them only what your plan, your role and your brand's rules allow. It cannot change your plan, billing, password or connected accounts. Skryvo receives the tool calls, never the rest of your conversation with the agent. The server sets who is calling from the key or token and ignores any identity a caller sends. More on [agent safety](https://skryvo.ai/docs/agents/safety/).

## Limits that protect the service

Each key or sign-in may make 60 requests a minute and 1,000 an hour ([Limits](https://skryvo.ai/docs/api/limits/)). The free tools on skryvo.ai pass Cloudflare Turnstile, the check that tells people from bots, and count each visitor's uses.

## Who can reach production

Only Skryvo's founder can reach production systems. Google Cloud, Render and Stripe, which run Skryvo's database, API and payments, are independently audited for security, including SOC 2. Card details stay with Stripe; Skryvo never sees or stores them.

## Report a problem

Email support@skryvo.ai with what you found and how to reproduce it. If a breach puts your data at risk, Skryvo tells you and the authorities the law requires, without delay. The full policy is the [Privacy Policy](https://skryvo.ai/privacy/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/trust/security/

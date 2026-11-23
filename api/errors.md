# API errors

> What each HTTP error from the API means, with the body it carries and what to do about it.

Every refusal carries a sentence a person can act on, so a script or an agent can show it as it is.

| Status | Meaning |
|---|---|
| 401 | The key or token is missing, revoked or expired. |
| 403 | The person's role in this team workspace does not allow the call. |
| 422 | Refused with a reason to show the person, or a field failed validation. |
| 429 | Sent more than 60 requests a minute or 1000 an hour with one key or token. |

A request that fails validation is also a 422, with `details` for each field.

## 401

The key or token is missing, revoked or expired.

```json
{
  "detail": "Send a live Skryvo API key as 'Authorization: Bearer sk_skryvo_…'."
}
```

## 403

The person's role in this team workspace does not allow the call.

```json
{
  "detail": "Only an admin or the owner can change a brand's look."
}
```

## 422

Refused with a reason to show the person, or a field failed validation.

```json
{
  "detail": "That time has passed. Pick a time in the future."
}
```

## 429

Sent more than 60 requests a minute or 1000 an hour with one key or token.

```json
{
  "error": "rate_limit_exceeded",
  "message": "Too many requests. Try again in 20 seconds.",
  "retry_after": 20
}
```

## What to do

- **401:** the key was revoked or the token expired. Make a new key, or refresh the OAuth token.
- **403:** the member's role in the team does not allow the call. Ask an admin or the owner.
- **422:** show `detail` to the person. It names the cause, such as a time in the past, an unknown channel or a month's allowance spent.
- **429:** wait the seconds in `Retry-After`, then send the call again. [Limits](https://skryvo.ai/docs/api/limits/).

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/api/errors/

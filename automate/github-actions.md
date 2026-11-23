# Skryvo in GitHub Actions

> A workflow that turns each published release into posts, then schedules them after a reviewer approves.

Each published release becomes a post per platform in the brand's voice. The drafts appear in the run's summary, and they are scheduled only after a reviewer approves the run's second job.

## Before you start

1. In Skryvo, open **Settings › API & agents** and create an API key. Store it as a secret in the tool, never in the workflow's text.
2. Find the ids of the channels to post to:

```bash
curl https://api.skryvo.ai/api/v1/agent/channels \
  -H "Authorization: Bearer $SKRYVO_API_KEY"
```

Each channel's `id` goes in `channel_ids`, and its `can` says what it takes.

## Set up the repository

1. Add the key as a repository secret named `SKRYVO_API_KEY`.
2. Add the channel ids as repository variables, `SKRYVO_LINKEDIN` and `SKRYVO_BLUESKY`.
3. Create an environment named `social` with required reviewers. GitHub then holds the second job until one of them approves.

## The workflow

Save as `.github/workflows/release-posts.yml`:
```yaml
name: Release posts
on:
  release:
    types: [published]

jobs:
  draft:
    runs-on: ubuntu-latest
    steps:
      - name: Write the posts
        env:
          SKRYVO_API_KEY: ${{ secrets.SKRYVO_API_KEY }}
          TOPIC: "${{ github.event.release.name }} is out: ${{ github.event.release.html_url }}"
        run: |
          jq -n --arg topic "${TOPIC:0:200}" \
            '{topic: $topic, platforms: ["linkedin", "bluesky"], pictures: false}' \
            | curl -sf -X POST https://api.skryvo.ai/api/v1/agent/drafts \
                -H "Authorization: Bearer $SKRYVO_API_KEY" \
                -H "Content-Type: application/json" -d @- > drafts.json
          jq -r '.posts[] | "### \(.platform)\n\n\(.text)\n"' drafts.json >> "$GITHUB_STEP_SUMMARY"
      - uses: actions/upload-artifact@v4
        with:
          name: drafts
          path: drafts.json

  schedule:
    needs: draft
    runs-on: ubuntu-latest
    environment: social
    steps:
      - uses: actions/download-artifact@v4
        with:
          name: drafts
      - name: Schedule each post
        env:
          SKRYVO_API_KEY: ${{ secrets.SKRYVO_API_KEY }}
          CHANNELS: "linkedin=${{ vars.SKRYVO_LINKEDIN }} bluesky=${{ vars.SKRYVO_BLUESKY }}"
        run: |
          for pair in $CHANNELS; do
            platform="${pair%%=*}"; channel="${pair#*=}"
            jq --arg p "$platform" --arg c "$channel" \
              '{text: (.posts[] | select(.platform == $p) | .text), channel_ids: [$c]}' drafts.json \
              | curl -sf -X POST https://api.skryvo.ai/api/v1/agent/posts \
                  -H "Authorization: Bearer $SKRYVO_API_KEY" \
                  -H "Content-Type: application/json" -d @-
          done
```

The first job spends one generation for both posts and schedules nothing. With no `at`, each post goes out about five minutes after the reviewer approves; add `at` to pick a time. To also write an article from the release, pass the release's address as one of [`plan_article`](https://skryvo.ai/docs/tools/plan-article/)'s `sources`.

## Keep a person in the loop

`write_post` returns drafts and schedules nothing, so the workflow decides when a person sees them. Three ways that work today:

- **Send the drafts for a yes.** Email or message the drafts to the person, and schedule only the ones they approve.
- **Let the team's approval hold them.** A key made by an editor on a brand that needs approval puts each scheduled post in the reviewer's queue: `schedule_post` answers with `awaiting_approval: true`, and nothing goes out until a reviewer approves it in Skryvo. [Approvals](https://skryvo.ai/docs/using/approvals/).
- **Plan topics instead of posts.** [`plan_calendar`](https://skryvo.ai/docs/tools/plan-calendar/) and [`accept_plan`](https://skryvo.ai/docs/tools/accept-plan/) add planned topics: Skryvo writes each one before its time and sets none to publish, so the person checks them in the calendar and schedules the ones they keep.

Any scheduled post can be moved, changed or cancelled in the calendar before it goes out.

## Know when a post is out

Register a [webhook](https://skryvo.ai/docs/api/webhooks/) for `post.published` and `post.failed`, and the workflow starts the moment a post goes out or fails. Without one, poll `GET https://api.skryvo.ai/api/v1/agent/posts?days=1` a few minutes after the post's time. A post with `posted_url` set is live and was read back from the platform; one with `publish_error` set did not go out, and the error says why in plain words.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/automate/github-actions/

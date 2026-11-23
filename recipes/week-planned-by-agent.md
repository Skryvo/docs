# A week planned by an agent

> An agent plans a week of posts for a brand, keeps the rows you choose, and schedules what you approve.

## What you get

A week (or a month) of social posts for one brand: each row has a date, a time, a platform, a topic and why it is there.

## What it costs

The plan is 1 generation and one of the month's calendar plans. Each post written from it is 1 generation per batch of platforms. Scheduling is free.

## Steps

1. **Plan.** [`plan_calendar`](https://skryvo.ai/docs/tools/plan-calendar/) with `start_date`, `period: "week"`, and the `platforms` and `topics` the person named. Nothing is added to the calendar yet.
2. **Keep the rows.** Show the plan. For the rows the person keeps, [`accept_plan`](https://skryvo.ai/docs/tools/accept-plan/) with those rows as `items`. They land on the calendar as planned topics, not set to publish.
3. **Write each post.** Either draft and approve the planned topics on the Desk in the app, or have the agent call [`write_post`](https://skryvo.ai/docs/tools/write-post/) for a row's topic and platform.
4. **Schedule.** On the person's yes, [`schedule_post`](https://skryvo.ai/docs/tools/schedule-post/) with the text, the channel and the row's time (`at`, ISO 8601, moved to the next quarter hour).

A prompt that does all of it:

```text
Plan next week's LinkedIn and Instagram posts for my brand. Show me the plan, add the rows I keep,
then write each one and wait for my yes before you schedule it.
```

## What a person approves

The rows to keep, and each post before it is scheduled.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/recipes/week-planned-by-agent/

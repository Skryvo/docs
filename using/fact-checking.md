# How a claim is checked

> How Skryvo checks the claims in an article against their sources, and what each verdict on the Fact Check card means.

Every article Skryvo writes in the app is checked before you read it. The **Fact Check** card on the article lists every claim once, cited ones first, each with its verdict, a one-line reason and its source.

## What happens to each claim

1. **Figures are grounded.** A figure a source states gets that source's link. A figure no source states, or a cited sentence whose numbers its source does not state, is removed. Two kinds of number stay: a worked example built on your own assumption ("Say the home costs $400,000"), and plain arithmetic on numbers already in the passage.
2. **The gaps are mended.** When a sentence is removed, the section is rewritten so nothing points at the missing text. The rewrite keeps every link and adds no number, or the original stays.
3. **Cited sentences meet their sources.** Each sentence with a link is compared with the fact from that page it restates best: its numbers must match, and its wording must stay close to the source's own.
4. **Uncited claims meet the web.** Up to ten claims without a citation are checked. Those still open get up to three searches; the top two result pages are read, and the verdict comes from those pages alone, citing their addresses.

## What each verdict means

| Verdict | What it means |
|---|---|
| Verified | The cited source states it, in close wording, with the same numbers. |
| Likely true | The cited source supports the point; its wording differs. |
| Disputed | Another source reports a different number for the same thing. |
| Contradicted | The web check found a source that says the opposite. |
| Unverified | The sentence states a number its source does not, or the web check found nothing on it. |

Unverified, disputed and contradicted claims stay in the draft, marked, so you decide. They lower the article's evidence score. Nothing the check could not confirm is shown as verified.

## Fixing a flagged claim

The fix on the Fact Check card rewrites only the flagged sentences from the evidence already gathered: each is corrected, softened or left as it was. Every other sentence stays word for word. A claim only you can back belongs in your answers to the plan's questions: your answers go in your own words, and nothing goes in quotation marks that your notes do not contain.

## Where the check runs

| Where | What runs |
|---|---|
| Articles in the app | Research, the fact list, unsourced-figure removal, the cited-sentence check and the web check of uncited claims |
| Articles from an agent | The same, without the web check of uncited claims |
| Your own article | **Check my facts**, free, from the editor's strip |
| Social posts, emails, ads, listings | A claim check against the brief and the brand's facts; claims none of them back are removed or flagged |

## What it does not do

The check covers figures, sources and product features. It does not judge opinions or general advice. There is no measured accuracy rate for the check itself yet, so none is published. The full method, with a real article's results, is on [Fact-checking at Skryvo](https://skryvo.ai/fact-checking/).

## From an agent

[`article_status`](https://skryvo.ai/docs/tools/article-status/) returns every claim with its verdict, its reason and its source links. [`improve_article`](https://skryvo.ai/docs/tools/improve-article/) with `goal: "accuracy"` rewrites only the disputed sentences.

---

Skryvo docs, checked against the product on 23 November 2026: https://skryvo.ai/docs/using/fact-checking/

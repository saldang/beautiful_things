# Equality algorithm and its conflict of interest

`Type:` grilling
`Status:` open
`Blocked by:` 04

## Question

What mechanically makes discovery "ethical and equal", how is fairness measured, and how does the mechanism survive a funding model that pays for attention?

To decide:

- What fairness means here, in one testable sentence. Candidates: guaranteed impression share for small/new orgs; exploration quota (N of M slots go to orgs you don't follow); locality weighting; strict rotation decoupled from popularity. Popularity-following is the failure mode, so what replaces it?
- The metric: if fairness can't be measured it can't be defended. Concrete candidate — Gini or top-10% share of impressions across verified orgs, published alongside the cost tracker.
- **The conflict of interest**: Platform Contributions depend on user attention, and an equality algorithm deliberately sends attention to small orgs. Is the ranking therefore structurally protected from the funding concern (e.g. fixed quotas, no A/B optimisation toward engagement), and how is that stated in the spec so a future contributor can't quietly "improve engagement"?
- Filters (cause, distance, …): does a filter narrow a fair-sampled pool, or does it re-rank by relevance and thereby reintroduce popularity?
- Does the same fairness rule govern the follow-based feed, or only discovery?

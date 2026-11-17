# Cost transparency data contract

`Type:` grilling
`Status:` open
`Blocked by:` —
`Blocks:` —

## Question

The live cost tracker is the feature that makes the no-profit claim checkable. What exactly is a cost line, where does the number come from, and what does "live" mean?

To decide:

- Sources of truth: fiscal-host API (contributions, balance, published expenses), plus hosting/provider billing. Which parts are pulled, which are manually entered, and who is allowed to enter one.
- Granularity and vocabulary: what counts as a cost — hosting, domain, provider fees, email, geocoding, research time? Is there a per-category breakdown or one number?
- Refresh cadence and staleness display: "live" is a promise; a lagging number must be shown *as* lagging rather than hidden.
- Currency, and what happens when costs and contributions are in different currencies.
- Relationship to the fairness metric (ticket 05): if both are published, are they published on the same page/schedule so the "we are funded by attention" story is legible?
- What the platform does *not* report (e.g. volunteer labour hours) — being explicit protects the claim.
- Failure behaviour: fiscal host API down or collective closed — what the page shows instead of a stale green number.

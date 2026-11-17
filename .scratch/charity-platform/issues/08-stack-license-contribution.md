# Stack, hosting realism, license and contribution model

`Type:` grilling
`Status:` open
`Blocked by:` —
`Blocks:` —

## Question

What is the spec's wrapper: the stack, the realistic monthly cost of running it, the license, and how strangers contribute?

To decide:

- Stack: one that the operator can carry alone *and* that contributors arrive already knowing. Constraint: the hosting cost feeds ticket 07's tracker, so an expensive default (managed everything, serverless with per-request pricing) is a product decision, not a technical one.
- Hosting shape: single small VPS + managed Postgres vs platform-as-a-service. What the spec promises a self-hoster, and what it demands of them.
- Media storage for update images: this is the cost line that grows with success — bundled object storage with a hard quota, or left to the deployer?
- License: AGPL-3.0 (a fork of the charity platform stays open, protects donors from a closed clone) vs MIT (maximum uptake). Recommend one and state why in the spec, because contributors ask first.
- Contribution process: ADRs for decisions, CONTRIBUTING, CI expectations, whether there is a CLA or DCO, and how a contributor's change to the ranking algorithm (ticket 05) is gated so the fairness promise can't be quietly reverted.
- Versioning and upgrade story for a self-hosted instance.

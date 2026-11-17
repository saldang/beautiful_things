# Charity platform — wayfinder map

`wayfinder:map` · effort `charity-platform` · tracker: local markdown (`.scratch/charity-platform/`)

## Destination

A **decision-complete spec** for an open-source, self-hostable charity network: charities register and publish updates like a social network; people follow favourites and discover others by filters (cause, distance, …); **Charity Donations move straight into each charity's own payment-provider account and never into the platform's balance**; platform running costs are published live against **Platform Contributions** received through a fiscal host.

The author builds the single real instance; strangers contribute. So the spec must let a contributor run an instance without reverse-engineering it, and must be honest about which parts only the operator can do (provider approval, entity, fiscal host).

Destination reached = no core decision left open, spec written, hand-off to build.

## Notes

- Skills per session: `/grilling` + `/domain-modeling` for decision tickets, `/research` for AFK tickets, `/to-spec` for the hand-off.
- Standing preferences: no profit, open source and open contribution, ranking that is explicitly ethical (no rich-get-richer), running costs and donations visible to users.
- Vocabulary lives in `CONTEXT.md` at the repo root. Read it before designing; add terms the moment they crystallise.
- No git repo exists in this directory yet. Research assets are plain files under `research/`, not `research/<name>` branches, until `git init` happens (then they can be moved to branches).
- Accepted cost of the money model: the operator is not a payment *intermediary* (never holds charity funds) but is still a payment *platform* — legal entity, provider application, restricted-business approval, ongoing compliance. Ticket 02 has now measured that cost; read it before designing anything that touches money.
- **Charitable fundraising on the provider is limited to AU, CA, UK and US.** Treat it as a given constraint of this spec, not a problem to solve.

## Decisions so far

- [Donation trust boundary and money model](issues/01-donation-trust-boundary.md) — charity donations go direct to each charity's own **Stripe** account via direct charges (Express/Custom rejected: they put funds in the platform balance); platform contributions via a **fiscal-hosted collective** with a public ledger; donation destinations are **allowlisted, re-verified on change, publicly versioned**; verification is **manual now, registry-import later**, and unverified orgs are listed nowhere and render no destination.
- [Payment-provider eligibility](issues/02-payment-provider-eligibility.md) — viable, but charitable fundraising is a *restricted* business supported only in **AU, CA, UK, US** and approved at Stripe's discretion; direct charges keep funds off the platform; liability is configured (`losses_collector = stripe`); live totals need per-account queries, not a platform-wide listing; "Standard account" is legacy language for an Accounts v2 *merchant configuration*.

## Not yet specified

<!-- in scope, but not sharp enough to ticket yet — graduates as the frontier advances -->

- **Second provider as fallback** (PayPal or similar) for charities outside AU/CA/UK/US, or for donors whose preferred method isn't on the first provider. Unresearched — worth a ticket only if ticket 03 chooses a degraded presence for those countries instead of excluding them.
- **Abuse and reporting**: how a user reports a fake update or a suspected swapped destination; what suspension looks like from the outside; appeal path.
- **Appeals / campaigns**: is a Donation Destination per org, or per campaign ("winter appeal")? Per-campaign multiplies the destination-verification problem; per-org may be too coarse for real charities.
- **Donor identity**: anonymous giving, receipts (provider-side?), what a donor sees afterwards, whether donors get accounts at all — and if they don't, whether "follow" needs an account.
- **Multi-instance**: does a second self-hosted instance share charity records with yours (federation), or is each instance its own world? Interaction with manual verification is the hard part.
- **Data model and API shape**: depends on the publishing model ticket and on what Stripe direct charges demand at checkout.
- **Content moderation** of org updates (misinformation, party-political campaigning vs charitable purpose) — policy, not just tooling.
- **Multi-currency and cross-border** giving; statement/payout quirks.
- **i18n, accessibility, mobile**: responsive web only? PWA?
- **How the spec itself is published** so strangers can contribute: CONTRIBUTING, ADRs, dependency/license policy.

## Out of scope

- Holding, pooling or forwarding charity money in a platform balance (Stripe Express/Custom accounts) — the middleman model is ruled out; returns only if the destination is redrawn.
- Building payment, refund, chargeback or receipt handling: the provider and the fiscal host own it.
- Paid maintainers, or any revenue beyond cost recovery.
- Fundraising for individuals, non-charitable causes, or political campaigns.

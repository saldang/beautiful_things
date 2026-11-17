# Donation trust boundary and money model

`Type:` grilling
`Status:` resolved
`Blocked by:` —
`Blocks:` 02

## Question

Where does a donation's money physically go? Who is allowed to receive it, what does the platform have to verify to be sure a destination belongs to the charity it claims, and how does the platform itself get funded without becoming a payment intermediary?

*Decided during the charting grilling rather than as a separate session; recorded here so the reasoning lives in one place.*

## Answer

**Two money flows, two names — never one word.**

- **Charity Donation** — donor → charity's own payment account. The platform never holds it, never forwards it, never sees a balance.
- **Platform Contribution** — anyone → the project, for running costs. The platform holds this *for itself*, which is not money transmission.

**Charity Donation plumbing: Stripe Connect, Standard accounts, direct charges.** The charity connects an existing Stripe account via OAuth; the charge is created on *their* account, so funds never enter the platform balance, and the destination is provably theirs because Stripe verified that human. Rejected: Express/Custom accounts, which onboard the charity *onto the platform* — funds land in the platform balance and the platform carries payout liability. That is the middleman model, and it is out of scope.

**Platform Contribution plumbing: a fiscal-hosted collective** (Open Collective or equivalent). The host supplies the legal entity, receives the money, publishes every expense and the balance, and exposes it over an API. The "live cost tracker" therefore becomes a *read of someone else's audited ledger* rather than a system the platform builds and self-reports — the difference between transparency a stranger can audit and transparency they must trust. Accepted limit: the host's country and currency decide who can contribute at all.

**Verification: manual review now, designed for registry import later.** The author reviews each org against its official public registry entry (A). A national-registry importer (B) can replace it later without a rewrite, which is why verification is modelled as state plus source.

- States: `unverified → verified → suspended`, with a `source` field (`manual` today, `registry:<country>` later).
- An org may exist at `unverified` to prepare its profile, but is **not listed or discoverable, and renders no Donation Destination, until `verified`**.
- Self-declaration with a visible "unverified" badge (C) is rejected: rendering donation destinations for unvetted orgs turns the platform into a phishing kit.

**Donation Destination rules** — the destination is the only place money moves, so it is the one boundary not economised on:

- Allowlisted domains only: recognised donation platforms, plus the charity's own registered domain. Blocks wallet substitution.
- Changing the destination requires **re-verification**.
- Every change is written to an **append-only public destination history**, so a donor's complaint can be answered with "this is what was live on this date".

**Consequences accepted by the operator:**

- The platform is not a payment intermediary but *is* a payment-provider platform: legal entity contracted with the provider, application, approval for charitable fundraising as a restricted business, ongoing compliance. Survivability of that gate is ticket 02, not an assumption.
- Totals per charity are observable from checkout events on the destination account, so "live donation updates per charity" survives — but the platform attests only what the provider told it, never a cross-app cash total it cannot see.

# Payment-provider eligibility for a charity-fundraising platform

`Type:` research
`Status:` resolved
`Blocked by:` —
`Blocks:` 03

## Question

Can a small open-source, no-profit platform operated by an individual (or hosted by a fiscal host) actually be approved to run Stripe Connect with **Standard accounts and direct charges** for charity fundraising — and if not, what is the closest legal shape that still keeps charity money out of the platform balance?

Facts needed, with sources and dates:

1. Stripe Connect platform eligibility: can an individual sign up as a Connect platform, or is a registered business/nonprofit entity required? What does the platform agreement make the platform liable for?
2. Charitable fundraising as a restricted business: does it need pre-approval, what does the review ask for, and does the answer differ for *direct charges on the charity's own Standard account* versus platform-held funds?
3. Country coverage: which countries can charities connect a Standard account from, and which can the operator's platform be registered in? (Determines who can even appear on the platform.)
4. Direct charges mechanics: are platform fees optional/zero, who absorbs the Stripe fee, and can the platform read per-account charge events (for live totals) without holding funds? Any restriction on a platform reading another account's payment data?
5. PayPal as an alternative: does the equivalent (charity receives directly, platform verifies the destination) exist, and what does it require?
6. Does the answer change if the fiscal host, rather than the individual, is the Connect platform of record? Is that even permitted?

## Answer

**Conditionally viable — with a country cap that reshapes the destination.** Findings with quotes and source links: [payment-provider-eligibility.md](../research/payment-provider-eligibility.md).

1. **Charitable fundraising is a *restricted* business on Stripe** — discretionary approval, revocable at any time, and the approval is per service offer.
2. **Only four countries.** "Organisations fundraising for a charitable purpose (Note: Supported in Australia, Canada, the United Kingdom and the United States. Prohibited in all other countries.)" A charity in Germany, Italy, France, Spain, Brazil… cannot be supported on this path. This is a scope fact, not a legal footnote: it belongs in the spec's first page.
3. **The money model survives intact.** Direct charges settle in the connected account's country, chargebacks hit the connected account's balance, and liability is a configuration choice — set `defaults.responsibilities.losses_collector = stripe` so the platform is not on the hook for a charity's chargebacks. The application fee must be explicitly **zero**: an application fee is the mechanism by which a platform skims, and the spec says the platform does not.
4. **Live totals are possible but fan out per account.** Platform-level visibility of direct charges is limited; you query per connected account (or per-account webhooks). One extra query per charity, not one query for all.
5. **"Stripe Standard accounts" is a legacy label.** New platforms use Accounts v2 with configurations. Keep the intent — merchant configuration, full Dashboard, Stripe does KYC, OAuth to connect — and name the configuration in the spec, not the legacy word "Standard".
6. **Open gaps, deliberately not assumed:** whether an individual (no entity) can be a Connect platform; whether the fiscal host can be the Connect platform of record; PayPal's charity requirements (unresearched); whether platform approval is separate from the per-charity 4-country list. These go to ticket 03, where the operator's shape is decided.

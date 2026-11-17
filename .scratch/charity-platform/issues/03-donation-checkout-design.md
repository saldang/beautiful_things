# Donation checkout design

`Type:` grilling
`Status:` open
`Blocked by:` 02

## Question

Given the provider constraints confirmed in ticket 02, what is the actual donor flow from "I want to give" to "the charity's account has it", and what does the platform record?

To decide:

- **The country cap, first.** Stripe supports charitable-purpose fundraising only in AU, CA, UK, US (ticket 02). So: is the platform those four countries only, with the limitation stated on the front page — or does a charity outside them get a degraded "link out, no checkout, no live totals" presence? The second answer is a *different product* for most of the world, and it needs to be chosen, not drifted into.
- **Who is the platform of record with the provider**: the author as an individual (if permitted at all), a new entity, or the fiscal host? Unverified in ticket 02 and it blocks going live, so it may need a direct question to Stripe rather than a design session.
- Checkout mechanism: provider-hosted Checkout Session created on the connected account (direct charge) vs a Payment Link per charity. Which one keeps the destination verifiable and the code smallest?
- Who absorbs the provider fee — the charity (fee debited from the connected account) or the platform (fee debited from the platform balance, and therefore a visible cost line in ticket 07)? Confirm the application fee is **zero**, since a non-zero one quietly makes the platform a beneficiary of charity donations.
- Per org or per campaign/appeal as the unit of giving (feeds the fog item on appeals).
- What the platform stores after a successful charge — event id, amount, currency, timestamp, donor identity or none? This is the data behind "live donation updates" and it is also a privacy decision.
- Live-total refresh: per-connected-account queries or webhooks (platform-level listing is not available for direct charges), and what the page shows while a charity's account is restricted or the provider is down.

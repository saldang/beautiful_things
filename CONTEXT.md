# Context

Ubiquitous language for this project. One term per concept; if a word is overloaded, the overload is the bug.

## Money

- **Charity Donation** — a donor's money given to a charity. It travels from donor to the charity's own payment-provider account. The platform never holds it, forwards it, or sees a balance.
- **Platform Contribution** — money given to the project itself to cover running costs. Held by the fiscal host on the project's behalf; it is not money transmission because the platform is the beneficiary.
- **Donation Destination** — where a charity's Charity Donations land: the charity's own Stripe Standard account, referenced by an allowlisted URL or provider account id. It is verified, it changes only through re-verification, and its history is public.
- **Platform Cost** — a real expense of running the instance. Published against Platform Contributions. Not a donation, not a fee.
- **Fiscal host** — the legal entity that receives Platform Contributions and publishes the ledger.

## Charities

- **Charity** — an organisation recognised by an official public charity registry, whose entry the operator has matched. Not a cause, not an individual, not a campaign.
- **Org record** — the platform's representation of a Charity. Its verification is a state plus a source, never a boolean.
- **Verification state** — `unverified` (may prepare a profile; not listed; renders no Donation Destination) → `verified` (listed, discoverable, may receive) → `suspended` (delisted; destination history retained).
- **Verification source** — `manual` today; `registry:<country>` when registry import lands.
- **Update** — the social artefact a verified Charity publishes. (Definition pending ticket 04.)

## People

- **Donor** — a person giving a Charity Donation. (Whether a Donor is an account holder is pending.)
- **Follower** — a person who follows a Charity.
- **Operator** — the person running an instance. Performs verification. In this project, also the author.

## Discovery

- **Discovery** — surfacing Charities to someone who does not follow them yet.
- **Fairness rule** — the mechanism that stops discovery from becoming popularity-ranked. (Pending ticket 05.)

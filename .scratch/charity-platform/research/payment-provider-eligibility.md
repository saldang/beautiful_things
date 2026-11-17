# Payment-provider eligibility — findings

Research asset for ticket `02-payment-provider-eligibility`. Fetched 2026-11-16 from the sources listed per finding. Quotes are verbatim from the pages; paraphrases are marked.

## Headline

**Stripe supports charitable-purpose fundraising only in Australia, Canada, the United Kingdom and the United States.** Everything the money model needs is technically available (direct charges, charity keeps its own account, platform never holds funds), but the platform's charity coverage is capped at four countries, and approval is discretionary.

## 1. Charitable fundraising is a restricted business, not an ordinary one

Source: <https://stripe.com/legal/restricted-businesses>

The restricted-business section says businesses listed require additional due diligence — "you will be asked to provide additional information (such as proof of relevant licences or more details about your business model)" — and "Stripe might not be able to grant approval for your business to use our products. If we do provide approval, note that the approval is specific to each service offer and it may be modified or revoked by Stripe at any time".

Two entries matter here, both under **restricted**:

- "Fundraising conducted by non-profits, charities, political organisations and businesses offering a reward in return for donation"
- "Organisations fundraising for a charitable purpose (Note: Supported in Australia, Canada, the United Kingdom and the United States. **Prohibited in all other countries**.)"

Adjacent entry, for completeness: "Charity sweepstakes and raffles for the explicit purpose of fundraising (Note: Supported in Australia, Brazil, Canada, Hong Kong, Ireland, Mexico, the United Kingdom and the United States. Prohibited in all other countries.)" — wider list, and it is a different activity from ordinary donation.

## 2. Direct charges do what the money model needs

Sources: <https://docs.stripe.com/connect/direct-charges>, <https://docs.stripe.com/connect/charges>

- You "create a charge directly on a connected account". "The charge amount—less the application fee—is deposited into the connected account."
- "Funds always settle in the country of the connected account."
- "Refunds and chargebacks reduce the connected account's balance" — the platform's balance is untouched.
- Application fee is optional and is what transfers to the platform; the spec must state it is **zero/none** for charity donations, otherwise the platform skims.
- Fee billing is a configuration choice: "You can choose whether to have Stripe debit fees directly from connected accounts or from your platform account." Choosing the connected account makes the charity pay Stripe's fee as merchant.

## 3. Live donation totals are possible but constrained

Source: <https://docs.stripe.com/connect/direct-charges>

"Direct charges have limited visibility at the platform level. When you create direct charges … To access direct charge data, you must query the Stripe API **using the connected account**." This "affects data synchronization services like Fivetran, as well as other third-party integrations that rely on platform-level API queries."

Consequence for the design: per-charity totals come from per-connected-account queries or per-account webhooks, not one platform-wide listing. That is a fan-out cost per charity, which matters once there are hundreds.

## 4. Account model: "Standard" is now the legacy name

Sources: <https://docs.stripe.com/connect/accounts>, <https://docs.stripe.com/connect/accounts-v2>

- Standard, Express and Custom are described as **legacy** account types: "The information on this page applies only to platforms that already use legacy connected account types." New platforms should use **Accounts v2** with configurations.
- A Standard connected account "is a conventional Stripe account where the connected account has a direct relationship with Stripe, is able to log in to the Dashboard", and "Stripe handles the onboarding and identity verification processes". Stripe contacts the account directly.
- Platforms "building on Connect must use OAuth to connect to Standard connected accounts."
- "After you create a Standard connected account, you can't change its country" and it can't change type afterwards.
- The v2 equivalent is a connected account carrying a **merchant** configuration plus dashboard access — same shape, new API. The spec should name the *configuration* (merchant, full dashboard, Stripe as losses collector) rather than the legacy label "Standard".

## 5. Liability lands where it should

Source: <https://docs.stripe.com/connect/risk-management>

- "Direct charges occur on a connected account, so negative transactions for direct charges affect the connected account's balance."
- Responsibility for connected-account negative balances is a configuration: `defaults.responsibilities.losses_collector` is either `stripe` or `platform`. With `stripe`, "Stripe risk teams manage all payments-related connected account risk", Stripe collects KYC, the account gets the full Dashboard, and "if you pay the listed prices for other Stripe fees, we don't charge additional fees for negative balance liability".
- The platform "is always responsible for its own negative balances."

So: choose `losses_collector = stripe`. The platform then is not on the hook for a charity's chargebacks — which is the whole reason the money model was chosen.

## 6. Still unresolved (do not assume)

- **Can an individual be a Connect platform?** Not stated in the pages read. The platform agreement is a business relationship, so assume a registered entity *or* the fiscal host is required — needs confirmation from Stripe, not from docs.
- **Can the fiscal host be the Connect platform of record** while the author operates the app? Plausible, unverified.
- **PayPal**: not researched. `developer.paypal.com` returned no usable text. Their nonprofit/charity requirements (confirmed charity status, country coverage) need their own research if PayPal is wanted as a second path.
- **Merchant of record / platform approval per country** for the *platform itself* (as opposed to the charity), versus per connected account: unclear which approval covers the 4-country list.

## Verdict recorded on the ticket

Conditionally viable, with the country cap and discretionary approval treated as **given constraints** in the spec, not obstacles to design around.

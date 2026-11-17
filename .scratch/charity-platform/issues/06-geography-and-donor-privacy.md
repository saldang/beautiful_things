# Geography, distance and donor privacy

`Type:` grilling
`Status:` open
`Blocked by:` —
`Blocks:` —

## Question

The distance filter needs to know where a charity is and where a user is. How precise, computed where, stored how long, and on what legal basis?

To decide:

- Charity location granularity: exact address (needed to verify against a registry) vs published centroid/city vs service area. What is shown publicly, and does a small charity's address become a safety problem?
- Donor/user location: browser geolocation on demand, a typed postcode/city, or IP-derived? Does the server ever store a user's coordinates, and if so for how long?
- Distance computed client-side (server never learns the user's location) or server-side (simpler, needs a lawful basis and retention rule)?
- Does "distance" mean anything for a charity that operates nationally, or does it need a service-area model instead of a point?
- Which lawful basis and consent flow applies for EU/UK users, and what the spec must say so a self-hoster in another jurisdiction can adapt it.
- Whether this applies to Platform Contribution donors too, or only to charity discovery.

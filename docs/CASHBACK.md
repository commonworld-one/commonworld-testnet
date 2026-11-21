# CWN cashback and rewards — proposal

**This is a design direction, not a launched program.** No cashback rate, CWN value, redemption promise, named partner, launch date, or funding commitment is announced here.

## Product goal

The product goal is embedded CWN rewards in ordinary apps, games, subscriptions and purchases, without requiring the user to install or operate a separate wallet such as MetaMask.

One intended use case is purchase-linked cashback: a person buys a service through a Commonworld partner or affiliate flow and receives a reward in CWN, potentially alongside perks or discounts.

The same purchase-linked reward model is intended to cover the agent economy: agents that buy services through partner or affiliate flows can receive CWN rewards too. Together, these flows are meant to form a partner network in which Commonworld earns revenue from partners. This document does not set reward rates, revenue shares or a settlement design.

The campaign, contract and claim mechanisms below are possible implementation components, not a replacement for that product goal. The user-facing experience should remain inside the application or purchase flow. The custody model, account design and payment routing remain open design questions. This is a proposed experience, not a claim that it is available today.

## Why explore it

A game, app, agent service or community campaign could reward a verifiable eligible action with CWN. On the current testnet, gas is configured at zero, so cashback would be a loyalty/reward mechanic—not a gas rebate.

## Testnet: prove accounting mechanics

Use valueless tCWN or clearly labelled points. Test eligibility, event evidence, calculation, claim, duplicate prevention, expiry, pause and reconciliation. Begin with a capped test budget and synthetic or consenting participants. Publish the contract, tests and replayable results. Test faucets, FO/tINST tokens, CWNX credits and escrow flows are separate experiments; none is the CWN cashback program.

## Betanet: bounded pilots

Before any pilot, define participant consent, campaign owner, funding source, total cap, per-user cap, duration, eligible actions, exclusions, correction/refund rules, monitoring and an emergency pause. Reconcile application events against on-chain claims and treasury outflows. Use named participants only where scope is agreed.

## Mainnet: launch gates

A public program would require an approved issuance and treasury policy, funded budget, audited contracts, multisig controls, incident response, clear terms, partner authorization and independent review. Explain transferability and redemption precisely; never imply cash equivalence or guaranteed returns without an approved, real arrangement.

## Possible contract boundaries

A first design could use a campaign registry, signed event attestations, capped reward vault, claim contract, role separation, expiry, pause and replay protection. Different actions (purchase, game milestone, agent work, referral) need different evidence and fraud rules. Some evidence may be verified off-chain; state clearly what the chain does and does not validate.

## Measures to publish for a pilot

Eligible events, claims, duplicate/rejected attempts, payout correctness, budget committed/paid/expired, support burden, abuse indicators, and completion/return rates. Report units, time window and source. Do not report token price as product success.

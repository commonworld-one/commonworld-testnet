# Testnet ecosystem catalogue

This catalogue separates current network infrastructure, experiments and ideas. “Live” means a dated observation exists; it is not a security or production-readiness claim.

## Network services and tooling

| Area | State supported by records | Evidence boundary |
|---|---|---|
| Besu QBFT network | Observed on Testnet; four validators and a separate RPC node in the dated topology snapshot. | Confirm current operation before reuse; topology does not establish decentralization. |
| Public JSON-RPC gateway | Observed, with bounded methods, body sizes, concurrency and request rates in dated configuration reports. | Limits may change; historical write failures and rate limits were observed. |
| Explorer | Public Blocks, Nodes and transaction pages observed. | Transient block-list errors occurred; no verified complete address/contract/transaction analytics totals. |
| Monitoring | Probe and database-size measurements recorded in operations reports. | No claim of external alerting unless explicitly connected. |
| RPC backup | One RPC database archive restored and checked at a snapshot height. | Not a full network, validator or key recovery drill. |
| Load testing | Controlled HTTP ramps and receipt/nonce reconciliation performed. | TPS depends on route, senders, socket budget and whether measuring attempts, RPC acceptance or block inclusion. |

## Agent demonstrations and candidate components

| Area | Current label | What to say |
|---|---|---|
| Faucets and test tokens | Agent-run experiments | FO and tINST claims were reported and in specific cases exercised by other agents. Not CWN reward programs. |
| AMMs and swaps | Bounded testnet experiments | Outside agents operated selected V2 flows. V4 and other paths need separate evidence. No audit or durable liquidity claim. |
| Paid service and escrow | Bounded experiments | Some receipt, idempotency, delivery-hash, refund and retry paths have report-level and partial independent evidence. Each contract/invariant must be linked separately. |
| Agent identity/authorization | Prototypes | Wallet-key authorization and scoped signatures were discussed/tested; this is not verified human identity or Sybil resistance. |
| Oracle | Mock feed | A mock feed was tested; a public consumer-compatible live price feed is not established. No Chainlink integration or partnership is claimed. |
| Indexing and analytics | Prototype / operator report | CWN Scout, by Muse, was described as a local SQLite indexer. Do not represent it as a durable, public, network-wide analytics service without deployment and coverage proof. |
| Cross-chain bridge | Author-reported experiment | A Base Sepolia bridge was described by its author; not independently reproduced or security reviewed. Do not imply Circle endorsement, native USDC issuance, or production safety. |
| Smart accounts and standards | Research / partial experiments | ERC-4337, ERC-1271, ERC-2771, ERC-7579, EIP-7702 and related ideas require separate implementation and conformance evidence. Mention only a named tested deployment, not a blanket network feature. |
| Chainlist / Safe / Chainlink / Circle / Hyperlane | Candidate or external process | Listing requests, compatibility research and design references are not partnerships, integrations or endorsements. |

## Evidence upgrades

Move an item to a stronger status only with dated, public proof:

- **Observed:** timestamped endpoint or chain check.
- **Independently exercised:** an operator other than the author completed the named flow, with transaction and result.
- **Integrated:** maintained product actually uses the component, with owner and scope.
- **Partner confirmed:** both parties authorize the public relationship claim.
- **Audited:** named independent security review with scope and report.

Every entry should record chain ID, environment, source post/report, contract address, deployment transaction, test transaction(s), operator, date and known limitations where applicable.

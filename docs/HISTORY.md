# Network history

The public Commonworld Testnet is the fourth chain in this project. Dates and chain IDs below come from operator records; independent corroboration is noted where it exists.

**1. Lab v1, local, 10-11 November 2026 (chain ID 2026111001).** The first standalone local Besu QBFT zero-gas stand on a Mac: validators, zero-fee transactions from accounts without native balance, contracts, tokens and agent scenarios, then MetaMask and an Explorer. It was followed by Lab v2 as a separate chain, not a continuation.

**2. Lab v2, local, 13 November 2026 (chain ID 2026111302).** A separate local chain with its own genesis, keys and data directories (operator records), adding QBFT with Prague from genesis, zero gas price, a wallet filter and an Explorer. On 14-16 November, local load ramps and integration probes ran against these local stands. Local-chain results describe local behavior only and are not evidence about the current public chain.

**3. Server capacity profile (V8), OVH, 16 November 2026.** A separate experimental server chain with a 100M block gas limit, used for capacity work. Its chain ID is reported as 2026111604 in a single operator record and is not independently corroborated here. Operator records describe its containers as stopped (not deleted) when the Commonworld Testnet launched. It is neither Lab v2 nor the Commonworld Testnet.

**4. Commonworld Testnet, OVH, chain ID 11111327.** Launched on the server on 18 November 2026 with a new genesis and fresh data (operator records; launch report dated 20261118T191226Z, RPC restart recorded 19:48:54 UTC). Block production, zero-gas contract operations and 200 test transfers were recorded the same day. On 18-19 November, public HTTPS RPC and Explorer access were added to the running chain through a filtered gateway (public RPC checks recorded 18 November, 23:04 UTC). Per operator records, public access is limited to this filtered gateway. The public testnet is public access to this server chain, not a newer chain after it.

The genesis block hash (0x7e47d2c1bfe09cba38a0315aa8ee6fa6ccb26338371035abf6f2768144aa0756) was verified against live block 0 on 21 November 2026. Other launch-time details above rest on dated operator records, not continuous observation.

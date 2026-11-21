# Commonworld Testnet network guide

**Snapshot date:** 20 November 2026 (operational passport and public checks described in the project records). This date covers the operational checks; linked posts and comments include records published on 21 November 2026 (UTC). These are dated observations, not a live uptime guarantee. Check the public RPC before depending on the network.

## Identity

| Property | Observed value |
|---|---|
| Chain name | Commonworld Testnet |
| Chain ID | `11111327` / `0xa98b9f` |
| Client / consensus | Hyperledger Besu `v26.11.0` / QBFT |
| Native currency | tCWN, 18 decimals |
| Gas price | Zero in the recorded testnet configuration |
| Public JSON-RPC | [https://rpc-testnet.commonworld.one](https://rpc-testnet.commonworld.one) |
| Explorer | [https://explorer-testnet.commonworld.one](https://explorer-testnet.commonworld.one) |

The recorded topology had four validators and a separate RPC node. This is a topology snapshot, not a claim of decentralization or production-grade fault tolerance.

## Execution specification

Values below come from the operator's genesis and deployment records (dated 18 and 19 November 2026) and were cross-checked against the public RPC with read-only calls on 21 November 2026 (UTC), around head block 39,400. The genesis and compose files themselves are not published in this repository; where the RPC cannot expose a value, it is marked as operator-reported.

### Chain and forks

| Parameter | Value |
|---|---|
| Chain ID / network ID | `11111327` (`0xa98b9f`) |
| Genesis block hash | `0x7e47d2c1bfe09cba38a0315aa8ee6fa6ccb26338371035abf6f2768144aa0756` |
| Genesis timestamp | `0` |
| Fork activations | `londonBlock: 0`, `shanghaiTime: 0`, `cancunTime: 0`, `pragueTime: 0`: London, Shanghai, Cancun and Prague rules are active from genesis |
| Later forks | No activation after Prague is configured in the recorded genesis |
| `zeroBaseFee` | `true` (base fee fixed at 0) |
| Genesis allocation | A single entry: dev treasury `0x16e2790be88a2ce5d5e982a32ab0427574659df9` with 10,000,000,000 tCWN (10^28 wei). No faucet contract is included |

The running chain matches these records: block 0 read over the public RPC has the same hash and `extraData` as the recorded genesis, and headers from block 0 onward carry `withdrawalsRoot` (Shanghai), `blobGasUsed`, `excessBlobGas` and `parentBeaconBlockRoot` (Cancun), and `requestsHash` (EIP-7685, Prague). The fork claims rest on these header fields, not on the client version string.

### Consensus

| Parameter | Value |
|---|---|
| Algorithm | QBFT; the header `mixHash` carries the QBFT vanity bytes |
| Validators at genesis | 4: `0x98eadc3caee5c150e2d495ece408152789e5b264`, `0xda390cac0780abbda751d8144bf03b20e5525d52`, `0x5f326f33a129e958440855e7f34a3fc8bbdee7df`, `0x6b8cc771381d52e8d3281f77fddb7666a209455d` |
| `blockperiodseconds` | 2 |
| `emptyblockperiodseconds` | 5 (the observed average block time of about 4.9 s reflects mostly empty blocks) |
| `requesttimeoutseconds` | 4 |
| `epochlength` | 30,000 blocks |
| `blockreward` | 0 |

The validator list is decoded from genesis `extraData`; live blocks show rotating proposers from this set. A separate, non-validating RPC node serves the public gateway. Peer counts from `net_peerCount` or the Explorer are not the validator set.

### Gas and transaction limits

| Parameter | Value | Confirmation |
|---|---|---|
| Block gas limit | 100,000,000 | genesis `gasLimit`; constant across sampled headers from block 0 to head |
| Per-transaction gas limit | 16,777,216 | genesis QBFT `pertxgaslimit` |
| RPC call gas cap | 16,777,216 | operator-reported (`--rpc-gas-cap`) |
| Base fee | 0 | `zeroBaseFee: true`; `baseFeePerGas` is 0 in every sampled block |
| Minimum gas price | 0 | operator-reported (`--min-gas-price=0`); `eth_gasPrice` and `eth_maxPriorityFeePerGas` return 0 |
| Blob base fee | 0 | `eth_feeHistory` returns `baseFeePerBlobGas: 0` |
| Pool balance check | disabled | operator-reported (`--tx-pool-enable-balance-check=false`); zero-balance accounts can submit zero-fee transactions |

### Client, storage and sync

| Parameter | Value |
|---|---|
| Client version | Hyperledger Besu `v26.11.0` ([release notes](https://github.com/besu-eth/besu/releases/tag/26.11.0), 2 November 2026) |
| Deployed image | `hyperledger/besu@sha256:3d6ac0368d449c13c4ba075acac90d6b96afa5b3113295385d88c4d5122c8808` (pinned, `linux/amd64`; the digest matches the upstream `hyperledger/besu:26.11.0` manifest on Docker Hub, verified 21 November 2026) |
| Runtime | OpenJDK 25, Linux x86-64 (from `web3_clientVersion`) |
| State storage | Bonsai (operator-reported `--data-storage-format=BONSAI`) |
| Chain pruning | BAL (operator-reported `--Xchain-pruning-enabled=BAL`). Per the upstream change that introduced the BAL mode ([besu-eth/besu#9637](https://github.com/besu-eth/besu/pull/9637)), BAL pruning keeps all blocks and prunes only Block Access Lists. That documents the pruning policy, not a guarantee of full historical retention: sampled receipt and event reads succeeded (see Limits and availability), but retention from genesis was not verified exhaustively |
| Sync mode | Not overridden; the documented Besu default for a private network started from a genesis file is FULL ([CLI reference](https://docs.besu-eth.org/public-networks/reference/cli/options)) |
| Historical state window | No override is recorded; the documented default for `--bonsai-historical-block-limit` is 512 blocks ([CLI reference](https://docs.besu-eth.org/public-networks/reference/cli/options)). Observed reads are consistent with that default: on 21 November 2026 a state read 388 blocks behind head succeeded while reads 644 or more blocks behind returned null. The effective value was not measured exactly |

The deployment records state that all four validators and the RPC node run the same pinned image. `web3_clientVersion` on the public RPC and the proposer vanity written into recent block `extraData` both report `besu 26.11.0`; each is evidence about the node that produced it, not independent proof of every validator's binary.

### Not published

The genesis file, node compose files, the Explorer build version and the edge gateway build are not published in this repository. This document quotes the operator's dated records for those values and marks them operator-reported.

## Connect

Use the public HTTPS JSON-RPC URL above. A read-only identity check can be made with:

```json
{"jsonrpc":"2.0","method":"eth_chainId","params":[],"id":1}
```

Expected chain ID at the snapshot date: `0xa98b9f`.

For a wallet, add a custom EVM network with the RPC URL and Chain ID above. The native currency symbol is tCWN. Obtain test tokens only from a faucet or distribution explicitly documented by its operator; this repository does not publish private keys or promise a faucet.

## Limits and availability

The public RPC is protected by a gateway with bounded request/response sizes, batch size, method concurrency, HTTP concurrency and rate limits. Operator records dated 19 November 2026 list a 1 MiB request body, 2 MiB response, batch size 20, an `eth_getLogs` range of 500 blocks, an `eth_feeHistory` range of 512 blocks, at most 20 in-flight method units with 2 concurrent HTTP requests, and rate limits of 12 requests/second per source (burst 24) and 60/second globally (burst 120). These settings were not re-verified under load for this document; check again before publishing client-facing integration instructions.

The public gateway allowlists wallet reads, fee and gas estimation, historical queries and signed `eth_sendRawTransaction`; `eth_sendTransaction`, `admin`, `debug`, `txpool` and QBFT mutation methods are not available on the public gateway (operator records, applied 19 November 2026).

The write path has experienced HTTP errors under load in historical checks. Reading success does not establish transaction-submission success. Use modest request rates, exponential backoff on 429/5xx, and reconcile transaction receipts instead of blindly resubmitting an unknown result.

Historical state availability was limited in observed checks. On 21 November 2026 (head around block 39,300), `eth_getBalance` at historical heights 36,710 and 38,656 returned null while the same call at height 38,912 succeeded, and `eth_call` at block 36,711 returned an internal error. Historical transaction receipts and event logs remained retrievable. The node's storage configuration is recorded in the operator's deployment records as Bonsai storage with `--Xchain-pruning-enabled=BAL` and no overridden historical-block limit; the records reviewed do not show the runtime command lines, so additional runtime overrides cannot be excluded. Under the documented client behaviour, Bonsai reconstructs historical state only within `--bonsai-historical-block-limit` blocks behind the head (default 512), and BAL pruning is documented to keep all blocks. Historical receipts and event logs were retrievable in the sampled checks above, but retention from genesis was not verified exhaustively. The observed boundary above is consistent with the 512-block default, but it does not prove it: the effective value was not measured exactly, and the limit is configurable. Do not assume historical contract state is available at an arbitrary past block.

Zero gas price is a testnet configuration, not an unlimited-capacity promise. RPC bandwidth, CPU, storage, indexing and operator resources remain finite.

## WebSocket

A saved server configuration showed an internal Besu WebSocket listener, but the public records reviewed for this repository do not establish a working public WebSocket endpoint or successful external `newHeads` subscription. Do not advertise WS until it is tested from outside and documented here.

## Explorer and indexing

The Explorer provides public pages for blocks, nodes and transactions. Historical checks showed that HTTP 200 for the page itself did not guarantee that the block-list API succeeded; transient 500/502 responses and RPC path failures were observed. Treat the Explorer as a useful testnet interface, not a complete indexed analytics service. No verified network-wide totals for all transactions, addresses and contracts are published here.

## Recovery evidence

One manual RPC database backup was restored on a separate OCI2 host. At the snapshot height, chain ID, genesis, block hash, a historical successful receipt, and a contract read matched the working RPC. This proves one RPC database restore test only; it does not establish full validator/key recovery.

## Safe usage

- Use only testnet assets; they have no promised monetary value.
- Never send a mainnet secret or seed phrase to a faucet or testnet app.
- Do not expose validator keys or private RPC routes in public issues.
- Report the exact timestamp, endpoint, method, response status and transaction hash when describing a failure.

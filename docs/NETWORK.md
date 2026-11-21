# Commonworld Testnet network guide

**Snapshot date:** 20 November 2026 (operational passport and public checks described in the project records). These are dated observations, not a live uptime guarantee. Check the public RPC before depending on the network.

## Identity

| Property | Observed value |
|---|---|
| Chain name | Commonworld Testnet |
| Chain ID | `11111327` / `0xa98b9f` |
| Client / consensus | Hyperledger Besu / QBFT |
| Native currency | tCWN, 18 decimals |
| Gas price | Zero in the recorded testnet configuration |
| Public JSON-RPC | [https://rpc-testnet.commonworld.one](https://rpc-testnet.commonworld.one) |
| Explorer | [https://explorer-testnet.commonworld.one](https://explorer-testnet.commonworld.one) |

The recorded topology had four validators and a separate RPC node. This is a topology snapshot, not a claim of decentralization or production-grade fault tolerance.

## Connect

Use the public HTTPS JSON-RPC URL above. A read-only identity check can be made with:

```json
{"jsonrpc":"2.0","method":"eth_chainId","params":[],"id":1}
```

Expected chain ID at the snapshot date: `0xa98b9f`.

For a wallet, add a custom EVM network with the RPC URL and Chain ID above. The native currency symbol is tCWN. Obtain test tokens only from a faucet or distribution explicitly documented by its operator; this repository does not publish private keys or promise a faucet.

## Limits and availability

The public RPC is protected by a gateway with bounded request/response sizes, batch size, method concurrency, HTTP concurrency and rate limits. Historical operational records list 1 MiB request, 2 MiB response, batch size 20, `eth_getLogs` range 500, `eth_feeHistory` range 512, and rate limits of 12 requests/second per source (burst 24) and 60/second globally (burst 120). These are historical settings, not a guarantee they remain current; check again before publishing client-facing integration instructions.

The write path has experienced HTTP errors under load in historical checks. Reading success does not establish transaction-submission success. Use modest request rates, exponential backoff on 429/5xx, and reconcile transaction receipts instead of blindly resubmitting an unknown result.

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

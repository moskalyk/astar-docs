---
sidebar_position: 6
---

# Transaction Manager

The Astar Transaction Manager offers a simple interface for dispatching transactions on Ethereum-compatible networks - specifically astar-zkevm and astar-zkyoto - to service your game or app and scale to millions of users that brings an enormous amount of benefits.

## Benefits
- Gas abstraction -- whereby users can pay for network gas in a variety of tokens (ie. USDC, DAI, etc.)
- Sponsored gas -- projects may sponsor the gas of specific contracts to allow free gas for their users
- Batched transactions -- group a bunch of independent transactions and allow them to be mined as a single transaction
- Parallel transactions -- parallelize the dispatch of transactions in some cases
- Fire + forget model -- easily send transactions to the transactions api which will automatically manage nonces, bump gas, and other features which will ensure fast delivery
- Optimal gas pricing for transactions -- will be attempted once and if not included from the mempool within 3 blocks, the transaction will be resubmitted

The only difference with respect to deployed EVM contracts: transactions with a Transaction Manager will have the `msg.sender` as one of the Sequence Relayer addresses, which can be seen in any one of the status pages: for example [on Astar zkEVM](https://astar-zkevm-relayer.sequence.app/status) with the `senders` array.

## [Try a Quickstart Today](https://docs.sequence.xyz/solutions/transaction-manager/overview)

:::info
Get started quickly with the source code of the [boilerplate](https://github.com/0xsequence-demos/tx-manager) using the Transactions API.
:::
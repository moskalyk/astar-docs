---
sidebar_position: 1
---

# Indexer

Astar Studio equips game builders with an indexer that collects data from the following networks: Astar zkEVM and Astar zKyoto.

## Features
- Super-fast API to query all token balances, history, metadata and NFTs with multi-chain support
- Real-time indexing of ERC20, ERC721 and ERC1155 transactions across EVM-compatible chains
- Automatically detects all tokens on the chain, without the need for a contract registry
- Resilient to node failures and chain re-organizations
- Easily listen for specific events and transactions on-chain accurately with a simple API
- Built-in token / nft metadata support to easily render tokens in your apps / games
- High uptime and availability

## What data can I query for my game?

Studio takes the stress out of gathering on-chain data for your game. Simply select the data you want from the indexer, and it generates the necessary code in snippets.

Sequence Indexer Documentation & Examples
- `getTokenBalances`: [Fetch lists of ERC20, ERC721, and ERC1155 Tokens](https://docs.sequence.xyz/api/indexer/examples/fetch-tokens/)
- `getTransactionHistory`: [Fetch the transaction history for any wallet address](https://docs.sequence.xyz/api/indexer/examples/transaction-history/) or [contract address](https://docs.sequence.xyz/api/indexer/examples/transation-history-token-contract/)
- `getTokenSupplies`: [Fetch all unique tokens in a particular ERC20/721/1155 contract, including total supplies](https://docs.sequence.xyz/api/indexer/examples/unique-tokens/)
- `getEtherBalance`: [Native Network Balance](https://docs.sequence.xyz/api/indexer/examples/native-network-balance/)
- `subscribeEvents`: [Subscribe to Blockchain Events](https://docs.sequence.xyz/api/indexer/examples/subscriptions/)

## How much code will I have to write to query?

Powered by the Sequence Indexer, the Astar Studio offers several features that level-up your on-chain data capabilities without writing a line of code by providing helpful code snippets of the most common use cases. It boasts a user-friendly interface that you can use to fetch important data, like the tokens owned by a specific wallet under a specific contract, for instance.
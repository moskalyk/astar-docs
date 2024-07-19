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

Fetch different kinds of data from the indexer:

- [Fetch all tokens & NFTS in any wallet including all metadata](./examples/fetch_tokens.md)
- [Fetch the transaction history for any wallet address](./examples/transaction_history.md)
- [Fetch all unique tokens in a particular ERC20/721/1155 contract, including total supplies](./examples/unique_tokens.md)
- [What is the total token supply of an ERC20 token? What is the total token supply of
  all the ERC1155 tokens in a particular contract?](./examples/unique_tokens.md)
- [Fetch the transaction history for any token contract address](./examples/transaction_history_token_contract.md)
- [Listen to transactions for particular tokens/contracts/addresses via webhooks](./examples/programmatic_webhooks.md)

## How much code will I have to write to query?

Powered by the Sequence Indexer, the Astar Studio offers several features that level-up your on-chain data capabilities without writing a line of code by providing helpful code snippets of the most common use cases. It boasts a user-friendly interface that you can use to fetch important data, like the tokens owned by a specific wallet under a specific contract, for instance.
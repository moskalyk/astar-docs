---
sidebar_position: 2
---

# Indexer Installation

:::warning[Introducing the Astar Studio - https://studio.astar.network]
The Sequence **Indexer** service is managed through **[Astar Studio](https://studio.astar.network)**. Sign up to grab your API access key.

[Get started with the **Astar Studio** Free Plan today!](https://studio.astar.network)
:::

Sequence Indexer is a simple API to query any blockchain token and NFT data. Below are instructions
on how to integrate the Sequence Indexer API into your Webapps, Games, and backends. In case you missed
it, please also see the [Indexer Overview](./index.md).

## Installation

The Sequence Indexer is built as an HTTP API with RPC endpoints that you may call directly
from your Webapp, Game or server backend. Below you'll find information on the RPC endpoint
schema with sample curl commands, along with examples in both Javascript/Typescript and Go.

Sequence provide SDKs for [Web / node.js](https://github.com/0xsequence/sequence.js) and [Go](https://github.com/0xsequence/go-sequence).
Or if you'd like to integrate the Indexer with another language target, simply follow the API reference below
to implement the HTTP requests. Additionally, read the Typescript client source code as [reference
implementation of the Indexer API client](https://github.com/0xsequence/sequence.js/blob/master/packages/indexer/src/indexer.gen.ts) as well.

<br />

### Web / node.js Installation

```sh
npm install 0xsequence ethers
```

or

```sh
pnpm install 0xsequence ethers
```

or

```sh
yarn add 0xsequence ethers
```

:::info
This code requires an API Access Key from [Astar Studio](https://studio.astar.network).
:::

```ts
import { SequenceIndexer } from '@0xsequence/indexer'

// indexer hosts for the chain you'd like to query
const indexer = new SequenceIndexer('https://astar-zkyoto-indexer.sequence.app', 'AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY')

// try any contract and account address you'd like :)
const contractAddress = '0x21a0055a7bc2c6c3000822aa06f81de88306f453'
const accountAddress = '0xe6eB28398CCBe46aA505b62b96822c2Ce8DAABf4'

// query Sequence Indexer for all nft balances of the account on Polygon
const nftBalances = await indexer.getTokenBalances({
	contractAddress: contractAddress,
	accountAddress: accountAddress,
	includeMetadata: true
})
 
console.log('collection of items:', nftBalances)
```

**NOTE:** if you're using `@0xsequence/indexer` from node.js, Sequence recommends using node v18.x or newer.

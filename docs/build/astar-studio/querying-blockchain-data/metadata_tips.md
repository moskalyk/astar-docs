---
sidebar_position: 4
---

# Metadata Tips & Notes on Spam

The Sequence Indexer and Sequence Metadata services will pick up everything and anything
that is published on a blockchain. The service is designed to provide data in real-time
as blocks are mined, and adhere to all popular ERC20, ERC721 and ERC1155 metadata
standards so things *just work*.

This is very helpful for your applications to be able to have access to the complete set of data
on-chain, but it also means it will include spam tokens when querying with default settings.

To combat spam, Sequence introduced `metadataOptions` arguments which can be passed to Indexer RPC
calls to control the results returned.

The Sequence Metadata service keeps track of contracts which are "verified" by checking popular
sources like Coingecko, OpenSea, Sequence Builder (https://sequence.build) and the Sequence Token
Directory (https://github.com/0xsequence/token-directory). By calling the Indexer RPC methods with
`"metadataOptions": { "verifiedOnly": true }`, any contract address which has not been verified, will
be omitted from the results. Sequence recommend using this option all the time, but, the downside is
if your project's contracts are unverified, then they will also be omitted from the results. To help
with this, your options are to get verified with one of the sources above, or in your RPC calls to pass
`"metadataOptions": { "verifiedOnly": true, "includeContracts": ["0x21a0055a7bc2c6c3000822aa06f81de88306f453"] }`
as an example.

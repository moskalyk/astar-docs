# Webhooks

Webhooks are a feature that allows systems to be called upon across the internet based on the emission of a blockchain event that meets some criteria. 

You can listen to transactions via webhooks using the Sequence Indexer by registering an endpoint or removing it after it's no longer required.

:::warning
	If you prefer a no-code way to add webhooks that uses the Astar Studio, check out [this walkthrough](/../no_code_webhooks)
:::

To begin, direct yourself to the [Astar Studio](https://studio.astar.network) and follow [this walkthrough for Public API Access Key](../../quickstart#5-claim-an-api-access-key) and [this walkthrough for a Secret API Access Key](../../quickstart/#6-optional-for-development-create-a-service-account), both required for using the Sequence Indexer Webhooks. 

Function
1. [Register a Webhook Listener](./programmatic_webhooks.md#1-register-a-webhook-listener)
2. [Remove a Webhook Listener](./programmatic_webhooks.md#2-remove-a-webhook-listener)

Service response
1. [Webhook Listener Response](./programmatic_webhooks.md#webhook-listener-response)

Examples
1. [Listen to All Mints of a Contract](./programmatic_webhooks.md#1-listen-to-all-mints-of-a-collectible-contract)
2. [Listen to Mints of a Specific Token ID](./programmatic_webhooks.md#2-listen-to-a-specific-token-id-for-an-erc1155)
3. [Listen to Event Topic Hashes for a Contract](./programmatic_webhooks.md#3-listen-to-topic-events-for-a-contract-address)
4. [Listen to Marketplace Request Creation](./programmatic_webhooks.md#4-listen-to-marketplace-request-creation)

:::info
	If you require a server for development, you can use one of the following:

	[Template Nodejs Webhook Server](https://github.com/0xsequence-demos/template-nodejs-webhook-server/blob/master/README.md) combined with [ngrok](https://ngrok.com) a secure tunnel to your computer running the local server

	[Template Cloudflare Webhook Worker](https://github.com/0xsequence-demos/template-cloudflare-worker-webhook)
:::

## 1. Register a Webhook Listener

Our filters allow you to listen to events with a particular contract address and/or account address, specific token ids, events, or topic hashes.

:::info
	If you require a webhook endpoint to call you can use [webhook.site](https://webhook.site/) for testing purposes to specify in the `url`
:::

*Sequence Indexer `AddWebhookListener` Method:*

* Request: POST /rpc/Indexer/AddWebhookListener
* Content-Type: application/json
* Body (in JSON):
    * `url` (string) -- the URL to send the webhook to
    * `filters` (object) -- an array of filters
        * `contractAddresses` ([]string) -- a ERC20 / ERC721 / ERC1155 contract address
        * `accounts` ([]string) -- wallet addresses
        * `events` ([]string) -- the string of the event (e.g. "Transfer(address,address,uint256)")
        * `topicHashes` ([]string) -- a hash of the of the event (e.g. ethers.utils.id("Transfer(address,address,uint256)"))
        * `tokenIDs` ([]int) *optional* -- an array of token ids

<br />

One of `contractAddresses` or `accounts` must be provided in the filter.

**Example: `AddWebhookListener`**

:::code-group

```bash [cURL]
curl -X POST -H "Content-Type: application/json" -H "X-Access-Key: <project_access_key>" -H "Authorization: BEARER <secret_API_key>" -d '{"filters": {"contractAddresses":["0x21a0055a7bc2c6c3000822aa06f81de88306f453"]}}' https://astar-zkyoto-indexer.sequence.app/rpc/Indexer/AddWebhookListener
```

```typescript [TypeScript]
// Works in both a Webapp (browser) or Node.js:
import { SequenceIndexer } from '@0xsequence/indexer'

const indexer = new SequenceIndexer('https://astar-zkyoto-indexer.sequence.app', '<project_access_key>', '<secret_API_key>')

const req = {
    url: 'https://webhook.site/27c266b7-ee69-4046-8319-75ce91ec2bcf',
    filters: {
		accounts: ['0x21a0055a7bc2c6c3000822aa06f81de88306f453']
	}
}


const ok = await indexer.addWebhookListener({
	Url: req.url,
    Filters: req.filters
})
	
console.log('ok', ok)
```

```go [Go]
import (
	"context"
	"fmt"
	"log"
	"net/http"

	"github.com/0xsequence/go-sequence/indexer"
)

func GetTransactionHistory(accountAddress string) {
	seqIndexer := indexer.NewIndexer("https://astar-zkyoto-indexer.sequence.app", '<project_access_key>', '<secret_API_key>')

	ok, err := seqIndexer.AddWebhookListener(context.Background(),
		&proto.WebhookListener{
			Url: "https://webhook.site/27c266b7-ee69-4046-8319-75ce91ec2bcf",
			Filters: &proto.WebhookEventFilter{
				Accounts: []prototyp.Hash{prototyp.HashFromString("0x57886924721C33F798E2b6F898CA91e8584AE79f")},
                // ContractAddresses: []prototyp.Hash{prototyp.HashFromString("0xC852bf35CB7B54a33844B181e6fD163387D85868")},
				// TokenIDs:          []prototyp.BigInt{prototyp.NewBigInt(1)},
			},
		},
	)
	fmt.Println(ok, err)
}
```
:::
Now you can listen to events on the blockchain with your webhook.

## 2. Remove a Webhook Listener
If you need to clean up your webhook listeners, you can submit requests to remove the listener based on listener `id` and `projectId` 

*Sequence Indexer `RemoveWebhookListener` Method:*

* Request: POST /rpc/Indexer/RemoveWebhookListener
* Content-Type: application/json
* Body (in JSON):
    * `id` (string) -- the id of the listener returned when registering the `response.listener.id`
    * `projectId` (string) -- the project id the JWT token was obtained from

<br />

**Example: `RemoveWebhookListener`**

In the following examples you'll need to update the `id` of the webhook listener, returned in the [`AddWebhookListener`](./programmatic_webhooks.md#1-register-a-webhook-listener)

:::code-group

```bash [cURL]
curl -X POST -H "Content-Type: application/json" -H "X-Access-Key: <project_access_key>" -H "Authorization: BEARER <secret_API_key>" -d '{ "id": <listener_id>, "projectId": 25906}' https://astar-zkyoto-indexer.sequence.app/rpc/Indexer/RemoveWebhookListener
```

```typescript [TypeScript]
// Works in both a Webapp (browser) or Node.js:
import { SequenceIndexer } from '@0xsequence/indexer'

const indexer = new SequenceIndexer('https://astar-zkyoto-indexer.sequence.app', '<project_access_key>', '<secret_API_key>')

const ok = await indexer.removeWebhookListener({
	id: <listener_id>,
    projectId: <project_id>
})
	
console.log('ok', ok)
```

```go [Go]
import (
	"context"
	"fmt"
	"log"
	"net/http"

	"github.com/0xsequence/go-sequence/indexer"
)

func RemoveWebhook(accountAddress string) {
	seqIndexer := indexer.NewIndexer("https://astar-zkyoto-indexer.sequence.app", '<project_access_key>', <secret_API_key>)

	ok, err := seqIndexer.RemoveWebhookListener(context.Background(),
		&proto.WebhookListener{
			id: <listener_id>,
			projectId: <project_id>,
		},
	)
	fmt.Println(ok, err)
}
```
:::

## Webhook Listener Response

Upon webhook listener response, an object is returned in the following structure

- Response (in JSON):
	- `id` (i32) -- the id of the response
	- `type` (string), -- the type of event (i.e. `BLOCK_ADDED`)
	- `blockNumber` (i32) -- the block number from the blockchain for when the event occured
	- `blockHash` (string) -- the hash of the block for the transaction
	- `parentBlockHash` (i32) -- the hash of the parent block
	- `contractAddress` (string) -- the contract address from where the event came from
	- `contractType` (string) -- the type of contract (e.g. `ERC20`, `ERC721`, `ERC1155`, etc.)
	- `txnHash` (string) -- the transaction hash of the event
	- `txnIndex` (i32) -- the index of the transaction in the blockchain block
	- `txnData` (object) -- the transaction data of who sent to who
		- `value` (string) -- the value of the transaction 
		- `from` (string) -- the originator of the transaction, if there is a value
		- `to` (string) -- the destination address of the transaction, if there is a value
	- `txnLogIndex` (string) -- the log index in the transaction
	- `logDataType` (string) -- the type of log event (e.g. `TOKEN_TRANSFER`)
	- `Log` (object) -- the emitted event data
		- `raw` ([Log](/api/indexer/examples/webhook-listener#log-object)) -- the raw transaction object
		- `contractType` (string) -- the type of contract (e.g. `ERC20`, `ERC721`, `ERC1155`, etc.)
		- `transferEvent` ([TransferEvent](./programmatic_webhooks.md#transferevent-object))
		- `OrderCreated` ([OrderbookRequestCreated](./programmatic_webhooks.md#orderbookrequestcreated-object))
		- `OrderAccepted` ([OrderbookRequestAccepted](./programmatic_webhooks.md#orderbookrequestaccepted-object))
		- `OrderCancelled` ([OrderbookRequestCancelled](./programmatic_webhooks.md#orderbookrequestcancelled-object))

## Examples

Provided are a few additional TypeScript examples:

### 1. Listen to All Mints of a Collectible Contract

If you want to get all mints and transfers of a contract

:::code-group

```bash [cURL]
curl -X POST -H "Content-Type: application/json" -H "X-Access-Key: <project_access_key>" -H "Authorization: BEARER <secret_API_key>" -d '{"filters": {"contractAddresses":["0x21a0055a7bc2c6c3000822aa06f81de88306f453"]}}' https://astar-zkyoto-indexer.sequence.app/rpc/Indexer/AddWebhookListener
```

```typescript [TypeScript]
// Works in both a Webapp (browser) or Node.js:
import { SequenceIndexer } from '@0xsequence/indexer'

const indexer = new SequenceIndexer(
    'https://astar-zkyoto-indexer.sequence.app', 
    '<project_access_key>',
    '<secret_API_key'
);

const req = {
	url: 'https://webhook-testing.ngrok.dev/webhook/5f5fe8ea-aa7e-4cf5-9d70-8f46c39a6117',
	filters:{   
		contractAddresses: ['0x21a0055a7bc2c6c3000822aa06f81de88306f453'],
	}
}

const ok = await indexer.addWebhookListener({
	url: req.url,
    filters: req.filters
})
	
console.log('ok', ok)
```
:::

### 2. Listen to a Specific Token ID for an ERC1155

If you want to get all mints of a specific token ID for an ERC1155

:::code-group

```bash [cURL]
curl -X POST -H "Content-Type: application/json" -H "X-Access-Key: <project_access_key>" -H "Authorization: BEARER <secret_API_key>" -d '{"filters": {"contractAddresses":["0x21a0055a7bc2c6c3000822aa06f81de88306f453"], "tokenIDs": ["1237"]}}' https://astar-zkyoto-indexer.sequence.app/rpc/Indexer/AddWebhookListener

```

```typescript [TypeScript]
// Works in both a Webapp (browser) or Node.js:
import { SequenceIndexer } from '@0xsequence/indexer'

const indexer = new SequenceIndexer(
    'https://astar-zkyoto-indexer.sequence.app', 
    '<project_access_key>',
    '<secret_API_key'
);

const req = {
	url: 'https://webhook-testing.ngrok.dev/webhook/5f5fe8ea-aa7e-4cf5-9d70-8f46c39a6117',
	filters:{   
		contractAddresses: ['0x21a0055a7bc2c6c3000822aa06f81de88306f453'],
		tokenIDs: ['1237']
	}
}

const ok = await indexer.addWebhookListener({
	url: req.url,
    filters: req.filters
})
	
console.log('ok', ok)
```
:::

### Custom Return Data Types Glossary

##### TransferEvent (object)
| Field    | Type 	 | Description |
| -------- | ------- | ------- 	   |
|  operator 	| string    | the address of the operator |
|  from 		| string    | the address of who the transaction came from |
|  to 			| string    | the address of who the transaction is for |
|  tokenIDs 	| []i32    	| an array of the token IDs transferred |
|  amounts 		| []i32    	| an array of the amounts of tokens transferred |

##### OrderbookRequestCreated (object)
| Field    | Type 	 | Description |
| -------- | ------- | ------- 	   |
|  requestId 		| i32    | the request id as an incremented value of the order|
|  creator 			| string    | the user address who created the order |
|  tokenContract 	| string    | the token contract of that the order is for |
|  tokenId 			| i32    | the token identifier |
|  isListing 		| boolean    | whether the order is to list (true) or offer orders (false) |
|  quantity 		| i32    | the number of tokens the order is for | 
|  currency 		| string    | the currency address of the order |
|  pricePerToken 	| i32    | the price per token for the order |
|  expiry 			| i32    | the expiry of when the order is no longer valid |
|  raw 				| [Log](/api/indexer/examples/webhook-listener#log-object)    | the raw log |

##### OrderbookRequestAccepted (object)
| Field    | Type 	 | Description |
| -------- | ------- | ------- 	   |
|  requestId 		| i32    | the request id as an incremented value of the order|
|  buyer 			| string    | the user address for who purchased the order |
|  tokenContract 	| string    | the token contract of that the order is for |
|  receiver 		| string    | the user address for who who recieves the token |
|  quantity 		| i32    | the number of tokens |
|  quantityRemaining| i32    | the remaining number of tokens left in the order |
|  raw 				| [Log](/api/indexer/examples/webhook-listener#log-object)| the raw log |

##### OrderbookRequestCancelled (object)
| Field    | Type | Description |
| -------- | ------- | ------- |
|  requestId 		| i32    | the request id as an incremented value of the order|
|  tokenContract 	| string    | the token contract of that the order is for | 
|  raw 				| [Log](/api/indexer/examples/webhook-listener#log-object)| the raw log |  

##### Log (object)
| Field    | Type | Description |
| -------- | ------- | ------- |
|  address 		| string    | the address from which the event came from |
|  topics 		| []string    | the topic event hashes emitted in the logs |
|  data 		| []string    | data |
|  blockNumber 	| i64    | the hex of the block number |
|  txHash 		| string    | the transaction hash from the blockchain |
|  txIndex 		| i32    | the index of the transaction in the blockchain block in hex |
|  blockHash 	| string    | the hash of the block for the transaction |
|  index 		| i32    | the log index in the transaction |
|  removed 		| boolean    | if the log of the event has been removed based on reorganizations |

# Wallet transaction history

## Fetch the transaction history for any wallet address

Fetches the transaction / token history for any wallet address of any ERC20, ERC721 and ERC1155 token.
The response includes decoded transaction details for easy consumption / rendering.

*Sequence Indexer `GetTransactionHistory` Method:*

* Request: POST /rpc/Indexer/GetTransactionHistory
* Content-Type: application/json
* Body (in JSON):
	* `filter` (object)
		* `accountAddress` (string) -- the wallet account address
		* `contractAddress` (string) -- optionally specify a contract address to filter
		* `accountAddresses` (string array) -- optionally specify a list of wallet account addresses
		* `contractAddresses` (string array) -- optionally specify a list of contract address
		* `transactionHashes` (string array) -- optionally specify a list of transaction hashes
		* `metaTransactionIDs` (string array) -- optionally specify a list of meta transaction IDs
	* `includeMetadata` (boolean - optional - default: false) -- toggle token metadata to be included in the response
	* `metadataOptions` (object - optional) -- additional options for metadata
		- `verifiedOnly` (boolean - optional) -- return only contracts which are 'verified' to help reduce spam
		- `includeContracts` ([]string - optional) -- list of specific contract addresses to always be included, even if verifiedOnly is enabled.


<br />

**Example: `GetTransactionHistory` of a wallet account address on Astar zKyoto using an `API_ACCESS_KEY`**


:::code-group

```bash [cURL]
curl -X POST -H "Content-Type: application/json" -H "X-Access-Key: AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY" https://astar-zkyoto-indexer.sequence.app/rpc/Indexer/GetTransactionHistory -d '{ "filter": { "accountAddress": "<ACCOUNT_ADDRESS>" }, "includeMetadata": true }'
```

```ts [Typescript]
// Works in both a Webapp (browser) or Node.js:
import { SequenceIndexer } from '@0xsequence/indexer'

const indexer = new SequenceIndexer('https://astar-zkyoto-indexer.sequence.app', 'AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY')

// try any account address you'd like :)
const filter = {
	accountAddress: "0xabc..."
}

// query Sequence Indexer for all token transaction history on Astar zKyoto
const transactionHistory = await indexer.getTransactionHistory({
	filter: filter,
	includeMetadata: true
})
	
console.log('transaction history in account:', transactionHistory)
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
	seqIndexer := indexer.NewIndexer("https://astar-zkyoto-indexer.sequence.app", "AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY")

	filter := &indexer.TransactionHistoryFilter{
		AccountAddress: &accountAddress,
	}

	metadataOptions := indexer.MetadataOptions{
		VerifiedOnly:     true, // Set to true if you want to fetch only verified contracts
		UnverifiedOnly:   false,
		IncludeContracts: nil, // Provide a list of specific contracts to include, if any
	}

	_, history, err := seqIndexer.GetTransactionHistory(context.Background(), filter, nil, nil, &metadataOptions)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println("transaction history:", history)
}
```

:::

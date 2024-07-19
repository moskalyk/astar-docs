# Contract token history

### Fetch / listen to the transaction history for any ERC20, ERC721, ERC1155 contract.

This query is helpful to track transaction history of a particular token contract.
In this example, we use a token contract address 0x21a0055a7bc2c6c3000822aa06f81de88306f453
on the Astar zKyoto. You may query any contract address on either `astar-zkyoto` or `astar-zkevm`.

_Sequence Indexer `GetTransactionHistory` Method:_

- Request: POST /rpc/Indexer/GetTransactionHistory
- Content-Type: application/json
- Body (in JSON):
  - `filter` (object)
    - `contractAddress` (string) -- a ERC20 / ERC721 / ERC1155 contract address

<br />

**Example: `GetTransactionHistory` of a contract on Astar zKyoto using an `API_ACCESS_KEY`**

:::code-group

```bash [cURL]
curl -X POST -H "Content-Type: application/json" -H "X-Access-Key: AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY" https://astar-zkyoto-indexer.sequence.app/rpc/Indexer/GetTransactionHistory -d '{ "filter": { "accountAddress": "0x21a0055a7bc2c6c3000822aa06f81de88306f453" }, "includeMetadata": true }'
```

```typescript [Typescript]
// Works in both a Webapp (browser) or Node.js:
import { SequenceIndexer } from "@0xsequence/indexer";

const indexer = new SequenceIndexer('https://astar-zkyoto-indexer.sequence.app', 'AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY')

// here we query a contract address, but you can use any
const contractAddress = "0x21a0055a7bc2c6c3000822aa06f81de88306f453";

// query Sequence Indexer for all token details / supplies
// try any contract address you'd like :)
const filter = {
  contractAddress: contractAddress,
};

// query Sequence Indexer for all token transaction history on Astar zKyoto
const transactionHistory = await indexer.getTransactionHistory({
  filter: filter,
});

console.log("transaction history of contract:", transactionHistory);
```

```go [Go]
import (
	"context"
	"fmt"
	"log"
	"net/http"

	"github.com/0xsequence/go-sequence/indexer"
)

func GetTransactionHistory(contractAddress string) {
	seqIndexer := indexer.NewIndexer("https://astar-zkyoto-indexer.sequence.app", "AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY")

	filter := &indexer.TransactionHistoryFilter{
		ContractAddress: &contractAddress,
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

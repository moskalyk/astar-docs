# Tokens in a contract

### Fetch all unique tokens in a particular ERC20/721/1155 contract, including total supplies

**Fetches token supplies and metadata for any ERC20, ERC721, ERC1155 contract.**

This query is helpful to render all tokens in a token contract, or to query the total token supplies.
In this example, we use a token contract address 0x21a0055a7bc2c6c3000822aa06f81de88306f453
on the Astar zKyoto network. You may query any contract address on any of the supported networks (but make
sure to query the indexer of the corresponding network).


*Sequence Indexer `GetTokenSupplies` Method:*

* Request: POST /rpc/Indexer/GetTokenSupplies
* Content-Type: application/json
* Body (in JSON):
	* `contractAddress` (string) -- a ERC20 / ERC721 / ERC1155 contract address
	* `includeMetadata` (boolean - optional - default: false) -- toggle token metadata to be included in the response
	* `metadataOptions` (object - optional) -- additional options for metadata
		- `verifiedOnly` (boolean - optional) -- return only contracts which are 'verified' to help reduce spam
		- `includeContracts` ([]string - optional) -- list of specific contract addresses to always be included, even if verifiedOnly is enabled.


<br />

**Example: `GetTokenSupplies` of a contract on Astar zKyoto using an `AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY`**

:::code-group

```bash [cURL]
curl -X POST -H "Content-Type: application/json" -H "X-Access-Key: AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY" https://astar-zkyoto-indexer.sequence.app/rpc/Indexer/GetTokenSupplies -d '{ "contractAddress": "0x21a0055a7bc2c6c3000822aa06f81de88306f453", "includeMetadata": true }'
```

```ts [Typescript]
// Works in both a Webapp (browser) or Node.js:
import { SequenceIndexer } from '@0xsequence/indexer'

const indexer = new SequenceIndexer('https://astar-zkyoto-indexer.sequence.app', 'AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY')

// here we query a contract address, but you can use any
const contractAddress = '0x21a0055a7bc2c6c3000822aa06f81de88306f453'

// query Sequence Indexer for all token details / supplies
const tokenDetails = await indexer.getTokenSupplies({
	contractAddress: contractAddress,
	includeMetadata: true
})
console.log('token details of contract:', tokenDetails)
```

```go [Go]
go
import (
	"context"
	"fmt"
	"log"
	"net/http"

	"github.com/0xsequence/go-sequence/indexer"
)

func GetTokenSupplies(contractAddress string) {
	seqIndexer := indexer.NewIndexer("https://astar-zkyoto-indexer.sequence.app", "AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY")

	metadataOptions := indexer.MetadataOptions{
		VerifiedOnly:     true, // Set to true if you want to fetch only verified contracts
		UnverifiedOnly:   false,
		IncludeContracts: nil, // Provide a list of specific contracts to include, if any
	}

	_, _, tokenDetails, err := seqIndexer.GetTokenSupplies(context.Background(), contractAddress, nil, &metadataOptions, nil)
	
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println("token details:", tokenDetails)
}
```

:::

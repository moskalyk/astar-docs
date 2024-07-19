# Native network balances (ie. ETH, MATIC, etc.)

### Fetch native network balance

*Sequence Indexer `GetEtherBalance` Method:*

* Request: POST /rpc/Indexer/GetEtherBalance
* Content-Type: application/json
* Body (in JSON):
  * `accountAddress` (string) -- the wallet account address

<br />

**Example: `GetEtherBalance` ASTR balance of a wallet account address on Astar zkEVM using an `API_Access_Key`**

:::code-group

```bash [cURL]
curl -X POST -H "Content-Type: application/json" -H "X-Access-Key: AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY" https://astar-zkevem-indexer.sequence.app/rpc/Indexer/GetEtherBalance -d '{ "accountAddress": "0x57886924721C33F798E2b6F898CA91e8584AE79f" }'
```


```ts [Typescript]
// Works in both a Webapp (browser) or Node.js:
import { SequenceIndexer } from '@0xsequence/indexer'

const indexer = new SequenceIndexer('https://astar-zkevm-indexer.sequence.app', 'AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY')

// try any account address you'd like :)
const accountAddress = '0xabc...'

// query Sequence Indexer for the ASTR balance on Astar zkevm
const balance = await indexer.getEtherBalance({
	accountAddress: accountAddress,
})
	
console.log('tokens in your account:', tokenBalances)
```


```go [Go]
import (
	"context"
	"fmt"
	"log"
	"net/http"

	"github.com/0xsequence/go-sequence/indexer"
)

func GetEtherBalance(accountAddress string) {
	seqIndexer := indexer.NewIndexer("https://astar-zkyoto-indexer.sequence.app", "AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY")

	nativeBalance, err := seqIndexer.GetEtherBalance(context.Background(), &accountAddress)
	
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println("nativeBalance:", nativeBalance)
}
```

:::

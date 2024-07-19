# Subscriptions

## Subscribe to Blockchain Events

You can subscribe to different blockchain events in real time using
subscription endpoints. Use filters to listen for particular contract
addresses, account addresses, and/or token IDs.

### Subscribing to Events
*Sequence Indexer `SubscribeEvents` Method:*

* Request: `POST /rpc/Indexer/SubscribeEvents`
* Content-Type: `application/json`
* Body (in JSON):
  * `Filters` ([]object) -- an array of filters
    * `contractAddresses` ([]string) -- a ERC20 / ERC721 / ERC1155 contract address
    * `accounts` ([]string) -- wallet addresses
    * `tokenIDs` ([]int) *optional* -- an array of token ids
    * `events` ([]string) -- an array of event names
    * `topicHashes` ([]string) -- an array of topic hashes

<br />

One of `contractAddresses`, `accounts` must be provided in the filter.

### Subscribing to Balance Updates
*Sequence Indexer `SubscribeBalanceUpdates` Method:*

### Subscribing to Receipts
*Sequence Indexer `SubscribeBalanceUpdates` Method:*

Example `SubscribeEvents`

:::code-group

```bash [cURL]
curl -X POST \
  -H 'Content-type: application/json' \
  -H "X-Access-Key: AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY" \
  https://astar-zkyoto-indexer.sequence.app/rpc/Indexer/SubscribeBalanceUpdates \
  -d '{"contractAddress":"<CONTRACT_ADDRESS>"}'
```

```go [Go]
import (
  "context"
  "log"

  "github.com/0xsequence/go-sequence/indexer"
  "github.com/0xsequence/go-sequence/lib/prototyp"
)

func SubscribeEvents() {
  seqIndexer := indexer.NewIndexer("https://astar-zkyoto-indexer.sequence.app", "AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY")

  reader, err := seqIndexer.SubscribeEvents(
    context.Background(),
    &indexer.EventFilter{
      ContractAddresses: []prototyp.Hash{prototyp.HashFromString("<CONTRACT_ADDRESS>")},
    },
  )
  if err != nil {
    log.Fatalf("SubscribeEvents: %v", err)
  }

  for {
    event, err := reader.Read()
    if err != nil {
      log.Fatalf("Read: %v", err)
    }

    log.Println("Event", event)
  }
}
```

```typescript [TypeScript]
// Works in both a Webapp (browser) or Node.js:
import { SequenceIndexer, WebrpcError } from '@0xsequence/indexer'

const indexer = new SequenceIndexer('https://astar-zkyoto-indexer.sequence.app', 'AQAAAAAAAI6BLZy0K5QmWGnhrWb_qtDQaGY')

const req = {
    filter: {
      contractAddresses: ['<CONTRACT_ADDRESS>'],
    },
}

const options = {
  onMessage: (msg: any) => {
    console.log('msg', msg)
  },
  onError: (err: WebrpcError) => {
    console.error('err', err)
  }
}

await indexer.subscribeEvents(req, options)
```

:::

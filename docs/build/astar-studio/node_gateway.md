---
sidebar_position: 9
---

# Node Gateway

Astar Studio gateway infrastructure enables you to have fail-over resilient RPC endpoints that can scale with your application.

By using the infrastructure, you save money for not having to deploy your own stack, and benefits from the feature of aggregating multiple public RPC providers into a single endpoint for use.

## Give it a try
Install `ethers` with `pnpm install ethers@5.7.2` or `yarn add ethers@5.7.2`

Acquire a Astar Studio access key to authenticate your connection and append to the endpoint, where the chain handle is either `astar-zkevm` or `astar-zkyoto` for testnet.

:::info
You can acquire a project access key [here](../astar-studio/quickstart.md#5-claim-an-api-access-key)
:::


```typescript
// Import the ethers library
import { ethers } from "ethers";
 
// Function to create a provider and fetch the latest block
async function getLatestBlock() {
  // Replace the following URL with your actual RPC endpoint
  const rpcUrl =
    "https://nodes.sequence.app/<chain_handle>/<project_access_key>";
 
  // Create a provider using the RPC URL
  const provider = new ethers.providers.JsonRpcProvider(rpcUrl);
 
  // Fetch the latest block
  const latestBlock = await provider.getBlock("latest");
 
  console.log("Latest Block:", latestBlock);
}
 
// Call the function to get the latest block
getLatestBlock().catch(console.error);
```
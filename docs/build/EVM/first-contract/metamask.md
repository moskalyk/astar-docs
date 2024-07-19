---
sidebar_position: 3
---

import Figure from '/src/components/figure'

# Configure MetaMask

## Add Astar kEVM or zKyoto to Metamask

#### Metamask Network Configuration

While using Metamask, a user can connect their wallet to a node gateway offered from Astar Studio with either: `astar-zkevm` or the testnet `astar-zkyoto`

##### 1. Open Wallet

<Figure src={require('/docs/build/EVM/first-contract/img/configure_wallet/wallet_open_networks.png').default} width="50%" />

##### 2. Select Networks

<Figure src={require('/docs/build/EVM/first-contract/img/configure_wallet/add_network_manually.png').default} width="50%" />

##### 3. Select Add Network

<Figure src={require('/docs/build/EVM/first-contract/img/configure_wallet/add_network.png').default} width="50%" />

##### 4. Add Network Manually

<Figure src={require('/docs/build/EVM/first-contract/img/configure_wallet/add_network_manually.png').default} width="50%" />

##### 5. Input Chain Details

<Figure src={require('/docs/build/EVM/first-contract/img/configure_wallet/save_network.png').default} width="50%" />

###### Astar zKyoto Testnet

| Properties                    | Network Details                |
| ----------------------------- | ------------------------------ |
| Network Name                  | Astar zKyoto Testnet |
| New RPC URL                   | `https://nodes.sequence.app/astar-zkyoto/<insert_astar_studio_project_access_key>`          |
| Chain ID                      | 6038361                           |
| Currency Symbol               | ASTR                           |
| Block Explorer URL (Optional) | https://zkyoto.explorer.startale.com/                               |

###### Astar Zkevm Network

| Properties                    | Network Details                |
| ----------------------------- | ------------------------------ |
| Network Name                  | Astar zkEVM |
| New RPC URL                   | `https://nodes.sequence.app/astar-zkevm/<astar_studio_project_access_key>`          |
| Chain ID                      | 3776                           |
| Currency Symbol               | ASTR                           |
| Block Explorer URL (Optional) | https://astar.blockscout.com/                               |

:::info
You can acquire a project access key [here](../../astar-studio/quickstart.md#5-claim-an-api-access-key)
:::

## Add Local Network to MetaMask

 >**_NOTE:_** Before  following the instructions below ensure you run a local node on your machine. Follow the instructions [here](https://docs.astar.network/docs/build/environment/local-network/#run-the-local-network).

It's easy to configure MetaMask to interact with the Astar/Shiden network family. To do so, open MetaMask, click the Network tab, and click Custom RPC. In the screen shown, please enter the information shown below:

| Properties                    | Network Details                |
| ----------------------------- | ------------------------------ |
| Network Name                  | My Network (anything you want) |
| New RPC URL                   | http://127.0.0.1:9944          |
| Chain ID                      | 4369                           |
| Currency Symbol               | ASTL                           |
| Block Explorer URL (Optional) |                                |

## Transfer Native Tokens to MetaMask

Since Astar Network has built a smart contract hub that supports both EVM and Wasm virtual machines, we need to support two different account types, H160 and SS58 respectively.

In order to send an asset to an H160 account (address B) from a Substrate-native ss58 account (address A), we will need to convert the H160 account address to its mapped Substrate-native ss58 account address (address B), before we can send the asset directly from address A to address B using [Polkadot.js](https://polkadot.js.org/apps/).

You can convert the destination H160 address to its mapped Substrate-native ss58 address by using our [address converter](https://hoonsubin.github.io/evm-substrate-address-converter/).
    
![Untitled](img/10.png)

Now, you are ready to receive some native tokens within MetaMask! Visit the Account page on the explorer and click the send button beside Alice. In the screen shown, you can input your ss58 address in the `send to address` field, choose an amount to send, and then click the `Make Transfer` button.

![4](img/4.png)

Congratulations!  You should now see some native tokens within MetaMask, and are one step closer to being able to deploy your first smart contract on Shiden local network!

![5](img/5.png)

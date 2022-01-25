---
description: API and free RPC WebSocket endpoints for the ICE community
---

# Get Started with ICE

## Network Details

The documentation corresponding contains details for the RPC - HTTP, WSS endpoints.&#x20;

{% tabs %}
{% tab title="Frost Network" %}
|                  |                                                                    |
| ---------------- | ------------------------------------------------------------------ |
| **Network name** | Frost Network                                                      |
| **Parent chain** | None (standalone network)                                          |
| **Parachain ID** | N/A                                                                |
| **Endpoints**    | <p>https://frost.icenetwork.io</p><p>wss://frost.icenetwork.io</p> |
| **Chain ID**     | 553                                                                |
| **Symbol**       | ICZ                                                                |
| **EVM RPC**      | https://frost.icenetwork.io:5545                                   |


{% endtab %}

{% tab title="Arctic Network" %}
|                  |                                                                       |
| ---------------- | --------------------------------------------------------------------- |
| **Network name** | Arctic Network                                                        |
| **Parent chain** | Rococo                                                                |
| **Parachain ID** | TBA                                                                   |
| **Endpoints**    | <p>https://arctic.icenetwork.io</p><p>wss://arctic.icenetwork.io </p> |
| **Chain ID**     | 552                                                                   |
| **Symbol**       | ICZ                                                                   |
| **EVM RPC**      | https://arctic.icenetwork.io:5545                                     |
{% endtab %}

{% tab title="Snow Netwrok" %}
|                  |                                                                  |
| ---------------- | ---------------------------------------------------------------- |
| **Network name** | Snow Network                                                     |
| **Parent chain** | Kusama                                                           |
| **Parachain ID** | TBA                                                              |
| **Endpoints**    | <p>https://snow.icenetwork.io</p><p>wss://snow.icenetwork.io</p> |
| **Chain ID**     | 551                                                              |
| **Symbol**       | ICZ                                                              |
| **EVM RPC**      | https://snow.icenetwork.io:5545                                  |
{% endtab %}

{% tab title="Ice Network" %}
|                  |                                                                |
| ---------------- | -------------------------------------------------------------- |
| **Network name** | Ice Network                                                    |
| **Parent chain** | Polkadot                                                       |
| **Parachain ID** | TBA                                                            |
| **Endpoints**    | <p>https://ice.icenetwork.io</p><p>wss://ice.icenetwork.io</p> |
| **Chain ID**     | 550                                                            |
| **Symbol**       | ICY                                                            |
| **EVM RPC**      | https://ice.icenetwork.io:5545                                 |
{% endtab %}
{% endtabs %}

## QuickStart

For the web3.js library, you can create a local Web3 instance and set the provider to connect to ICE (both HTTP and WS are supported):

```
const Web3 = require('web3'); // Load Web3 library
// Create local Web3 instance - set ICE as provider
const web3 = new Web3("https://ice.icenetwork.io")
```

For the ethers.js library, define the provider by using `ethers.providers.StaticJsonRpcProvider(providerURL, {object})` and setting the provider URL to ICE:

```
const ethers = require('ethers');

const providerURL = "https://ice.icenetwork.io";
// Define Provider
const provider = new ethers.providers.StaticJsonRpcProvider(providerURL, {
    chainId: 550,
    name: 'ice'
});
```

Any Ethereum wallet should be able to generate a valid address for ICE Networks (for example, [MetaMask](https://metamask.io)).

## Connect to Metamask

If you already have MetaMask installed, you can easily connect MetaMask to ICE:

{% hint style="info" %}
**Note:** MetaMask will popup asking for permission to add ICE as a custom network. Once you approve permissions, MetaMask will switch your current network to ICE.
{% endhint %}

If you want to connect MetaMask by providing the network information, you can use the following data:

* Network Name: `Ice`
* RPC URL: `https://ice.icenetwork.io`
* ChainID: `550` (hex: `0x226`)
* Symbol (Optional):`ICY`

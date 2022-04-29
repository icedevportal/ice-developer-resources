---
description: API and free RPC WebSocket endpoints for the ICE community
---

# Network Endpoints

## Network Details

The documentation corresponding contains details for the RPC - HTTP, WSS endpoints.&#x20;

{% tabs %}
{% tab title="Frost Network" %}
|                  |                                                                                      |
| ---------------- | ------------------------------------------------------------------------------------ |
| **Network name** | Frost Network                                                                        |
| **Parent chain** | None (standalone network)                                                            |
| **Parachain ID** | N/A                                                                                  |
| **Endpoints**    | <p>https://frost-rpc.icenetwork.io:9933</p><p>wss://frost-rpc.icenetwork.io:9944</p> |
| **Chain ID**     | 553                                                                                  |
| **Symbol**       | ICZ                                                                                  |
| **EVM RPC**      | https://frost-rpc.icenetwork.io:9933                                                 |
{% endtab %}

{% tab title="Arctic Network" %}
|                  |                                                                               |
| ---------------- | ----------------------------------------------------------------------------- |
| **Network name** | Arctic Network                                                                |
| **Parent chain** | Rococo                                                                        |
| **Parachain ID** | TBA                                                                           |
| **Endpoints**    | <p>https://arctic-rpc.icenetwork.io</p><p>wss://arctic-rpc.icenetwork.io </p> |
| **Chain ID**     | 552                                                                           |
| **Symbol**       | ICZ                                                                           |
| **EVM RPC**      | https://arctic-rpc.icenetwork.io                                              |
{% endtab %}

{% tab title="SNOW Network" %}
|                  |                                                                          |
| ---------------- | ------------------------------------------------------------------------ |
| **Network name** | Snow Network                                                             |
| **Parent chain** | Kusama                                                                   |
| **Parachain ID** | TBA                                                                      |
| **Endpoints**    | <p>https://snow-rpc.icenetwork.io</p><p>wss://snow-rpc.icenetwork.io</p> |
| **Chain ID**     | 551                                                                      |
| **Symbol**       | ICZ                                                                      |
| **EVM RPC**      | https://snow-rpc.icenetwork.io                                           |
{% endtab %}

{% tab title="ICE Network" %}
|                  |                                                                        |
| ---------------- | ---------------------------------------------------------------------- |
| **Network name** | Ice Network                                                            |
| **Parent chain** | Polkadot                                                               |
| **Parachain ID** | TBA                                                                    |
| **Endpoints**    | <p>https://ice-rpc.icenetwork.io</p><p>wss://ice-rpc.icenetwork.io</p> |
| **Chain ID**     | 550                                                                    |
| **Symbol**       | ICY                                                                    |
| **EVM RPC**      | https://ice-rpc.icenetwork.io                                          |
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Only Frost Testnet and Arctic Testnet are currently live, the Snow Testnet is WIP.
{% endhint %}

## QuickStart

For the web3.js library, you can create a local Web3 instance and set the provider to connect to Frost (both HTTP and WS are supported):

```
const Web3 = require('web3'); // Load Web3 library
// Create local Web3 instance - set Frost as provider
const web3 = new Web3("https://frost-rpc.icenetwork.io")
```

For the ethers.js library, define the provider by using `ethers.providers.StaticJsonRpcProvider(providerURL, {object})` and setting the provider URL to Frost:

```
const ethers = require('ethers');

const providerURL = "https://frost-rpc.icenetwork.io";
// Define Provider
const provider = new ethers.providers.StaticJsonRpcProvider(providerURL, {
    chainId: 553,
    name: 'frost'
});
```

Any Ethereum wallet should be able to generate a valid address for Frost Network (for example, [MetaMask](https://metamask.io)).

---
description: API and free RPC WebSocket endpoints for the ICE community
---

# Network Endpoints

## Network Details

The documentation corresponding contains details for the RPC - HTTP, WSS endpoints.&#x20;

{% tabs %}
{% tab title="Arctic Network" %}
|                  |                                                                                        |
| ---------------- | -------------------------------------------------------------------------------------- |
| **Network name** | Arctic Network                                                                         |
| **Parent chain** | Rococo                                                                                 |
| **Parachain ID** | 3025                                                                                   |
| **Endpoints**    | <p>https://arctic-rpc.icenetwork.io:9933</p><p>wss://arctic-rpc.icenetwork.io:9944</p> |
| **Chain ID**     | 552                                                                                    |
| **Symbol**       | ICZ                                                                                    |
| **EVM RPC**      | https://arctic-rpc.icenetwork.io:9933                                                  |
{% endtab %}

{% tab title="SNOW Network" %}
|                  |                                                                               |
| ---------------- | ----------------------------------------------------------------------------- |
| **Network name** | Snow Network                                                                  |
| **Parent chain** | Kusama                                                                        |
| **Parachain ID** | TBA                                                                           |
| **Endpoints**    | <p>https://snow-rpc.icenetwork.io:9933</p><p>wss://snow-rpc.icenetwork.io</p> |
| **Chain ID**     | 552                                                                           |
| **Symbol**       | ICZ                                                                           |
| **EVM RPC**      | https://snow-rpc.icenetwork.io:9933                                           |
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
**Arctic** Testnet is currently <mark style="color:green;">live.</mark>

**SNOW** mainnet is also <mark style="color:green;">live</mark>.
{% endhint %}

## QuickStart

For the web3.js library, you can create a local Web3 instance and set the provider to connect to Arctic (both HTTP and WS are supported):

```
const Web3 = require('web3'); // Load Web3 library
// Create local Web3 instance - set Arctic as provider
const web3 = new Web3("https://arctic-rpc.icenetwork.io:9933")
```

For the ethers.js library, define the provider by using `ethers.providers.StaticJsonRpcProvider(providerURL, {object})` and setting the provider URL to Arctic:

```
const ethers = require('ethers');

const providerURL = "https://arctic-rpc.icenetwork.io:9933";
// Define Provider
const provider = new ethers.providers.StaticJsonRpcProvider(providerURL, {
    chainId: 552,
    name: 'arctic'
});
```

Any Ethereum wallet should be able to generate a valid address for Arctic Network (for example, [MetaMask](https://metamask.io/)).

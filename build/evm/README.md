---
description: Ethereum Virtual Machine on ICE/SNOW Network
---

# EVM

Users and Developers can write and deploy smart contracts using Solidity, use Metamask as their personal wallet, thanks to the EVM Support provided by [Frontier](https://github.com/paritytech/frontier). Frontier, developed by [Parity Technologies](https://www.parity.io/), is an Ethereum compatible layer on Substrate, which enables the substrate-based chains like ICE/SNOW to run  Ethereum __ smart contracts out of the box.

## QuickStart

Using the [web3.js library](evm-and-solidity-smart-contracts/using-web3.js/), you can create a local Web3 instance and set the provider to connect to Arctic (both HTTP and WS are supported):

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
    chainId: 553,
    name: 'arctic'
});
```

Any Ethereum wallet should be able to generate a valid address for Arctic Network (for example, [MetaMask](configuring-metamask.md#steps)).

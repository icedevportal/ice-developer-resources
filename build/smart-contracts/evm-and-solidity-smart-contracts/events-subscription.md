---
description: Client side subscription to events emitted by the solidity smart contracts
---

# Events Subscription

[**Events**](https://docs.soliditylang.org/en/develop/contracts.html?highlight=events#events) in simple terms, are logging mechanisms to notify the world, outside of the smart contracts, that something has occurred on the blockchain. For example, a **Transfer** event is emitted when an ERC20 token transfer occurs.

Just like any other EVM compatible blockchains, we can use [web3.js](https://web3js.readthedocs.io/), [ethers.js](https://docs.ethers.io/) or any other library of our choice to subscribe to event logs.

Let ‘s assume that we have the following contract **EventsDemo** that emits an event **contractEvent**, whenever the contract variable **intVal** is changed.

```
//SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.4;
 
contract EventsDemo {
 
   int public intVal;
 
   event contractEvent(int, string);
 
   constructor() {
       intVal  = 100;
   }
 
   function setVal(int _val) public {
       intVal = _val;
       emit contractEvent(_val, "Value changed");
   }
}
```

Assuming this contract is deployed at address **0x00Fe7CBE594FF95CaA560336D6e1B7eAC2C59eCe** on the [**Arctic network**](../../../ice-testnet-details/network-endpoints/), we can subscribe to the **contractEvent** event using the following code.

```
const Web3 = require('web3');
const web3 = new Web3('wss://arctic-rpc.icenetwork.io:9944');
 
const typesArray = [
   { type: 'int256', name: 'intVal' },
   { type: 'string', name: 'str' },
];
 
web3.eth.subscribe('logs', {
   address: '0x00Fe7CBE594FF95CaA560336D6e1B7eAC2C59eCe',
   topics: [web3.utils.sha3('contractEvent(int256,string)')]   // only interested in the “contractEvent” event
}, (error) => {
   if (error)
       console.error(error);
})
.on("connected", function (subscriptionId) {
   console.log(subscriptionId);
})
.on("data", function (log) {
   // Decode the received data into JS object
   const decodedParams = web3.eth.abi.decodeParameters(typesArray, log.data);
   console.log(decodedParams);
});
```

{% hint style="info" %}
The demonstrated code was tested with _**web3.js v1.7.1** _ and ** **_**solc v0.8.12**._
{% endhint %}

First of all, our code creates a web3 instance connected to the [**Arctic network websocket endpoint**](../../../ice-testnet-details/network-endpoints/#network-details). Then we subscribe to event logs of the deployed instance of the **EventsDemo** contract at address __ 0x00Fe7CBE594FF95CaA560336D6e1B7eAC2C59eCe, and only listen for the specific **contractEvent** being emitted. Finally, when this event is emitted by the contract, our code decodes the hex data into JS object and outputs it to the console.

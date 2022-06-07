---
description: >-
  Let's communicate with our freshly deployed contract in the ice testnet using
  web3.js
cover: ../../../.gitbook/assets/1_W0eKVsybZ6TdxV8UYJX5Yg_midweb3js.jpg
coverY: 0
---

# Interact with contracts using web3.js

### Interact with contract

Create <mark style="color:blue;"></mark> <mark style="color:blue;"></mark>_<mark style="color:blue;">interact.js</mark>_

```
const Web3 = require('web3');
const { abi } = require('./compile');

const providerRPC = {
  development: 'https://arctic-rpc.icenetwork.io:9933'
};
const web3 = new Web3(providerRPC.development);


const account_from = {
  privateKey: 'Your private key',
};
const contractAddress = '0x270E2e4BDbDDa951504E90c11275f55b9eda112B' // deployed contract address

/*
   -- Send Function --
*/
// Create Contract Instance
const counter = new web3.eth.Contract(abi, contractAddress);

// Build Increment Tx
const incrementTx = counter.methods.incrementCounter();

const increment = async () => {
   
  console.log(
    `Calling the increment by 1 function in contract at address: ${contractAddress}`
  );

  try {
      //   Sign Tx with PK
  const createTransaction = await web3.eth.accounts.signTransaction(
    {
      to: contractAddress,
      data: incrementTx.encodeABI(),
      gas: await incrementTx.estimateGas(),
    },
    account_from.privateKey
  );


//   Send Tx and Wait for Receipt
  const createReceipt = await web3.eth.sendSignedTransaction(createTransaction.rawTransaction);
  console.log(`Tx successful with hash: ${createReceipt.transactionHash}`);


  // Read function
  const currentCount = await counter.methods.getCount().call();
  console.log(`Current Count: ${currentCount}`); // Should return 1
  } catch (error) {
      console.log(error)
  }
};

increment();
```

Next run

`node interact.js`

This first outputs the tx hash for calling incrementCount and then the value of current count that should be now 1 (after running first time). So here we invoked both read and write function

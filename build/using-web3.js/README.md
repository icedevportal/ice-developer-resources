---
description: >-
  This post will show you how to deploy and interact with a Solidity-based smart
  contract on ICE using the Solidity compiler and web3.js.The web3.js library
  may be used directly with an ICE node due to
cover: ../../.gitbook/assets/1_W0eKVsybZ6TdxV8UYJX5Yg_midweb3js.jpg
coverY: 0
---

# Using Web3.js

[Web3.js](https://web3js.readthedocs.io/en/v1.7.0/index.html) lets us to carry out the second obligation, which is to create clients that communicate with The Ethereum Blockchain. It is a set of libraries that enable you to accomplish tasks like as sending Ether from one account to another, reading and writing data from smart contracts, creating smart contracts, and much more.

Here we will write a smart contract which simply increases and decreases a count variable and the deploy the smart contract on ICE's network and interact with it using web3.js

### Create Project

Create a directory to store all required files

```
mkdir Counter && cd Counter/
```

### Initialize npm package

```
npm init -y
```

### Install dependencies

Install web3 and solc dependencies

```
npm install web3 solc
```

This example's setup will be straightforward, and it will include the files listed below:

&#x20;_**counter.sol**_: the file with our Solidity code&#x20;

_**compile.js**_: compiles the contract with the Solidity compile

_**deploy.js**_: it will handle the deployment to our ICE testnet node&#x20;

_**interact.js**:_ it will be used to interact with contracts

### Create contract

Create _<mark style="color:blue;">Counter.sol</mark>_ file in root

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

contract Counter {
    uint256 private count = 0;
    uint256 moneyStored = 0;

    function incrementCounter() public {
        count += 1;
    }
    function decrementCounter() public {
        count -= 1;
    }

    function addMoney() payable public {
        moneyStored += msg.value;
    }

    function getCount() public view returns (uint256) {
        return count;
    }

    function getMoneyStored() public view returns (uint256){
        return moneyStored;
    }
}
```

### Compile Contract

Create _<mark style="color:blue;">compile.js</mark>_ . The _<mark style="color:blue;">compile.js</mark>_ file's only function is to utilize the Solidity compiler to generate the contract's bytecode and interface (ABI).

```
const path = require("path");
const fs = require("fs");
const solc = require("solc");

// Compile contract
const contractPath = path.resolve(__dirname, "Counter.sol");
const source = fs.readFileSync(contractPath, "utf8");
const input = {
  language: "Solidity",
  sources: {
    "Counter.sol": {
      content: source,
    },
  },
  settings: {
    outputSelection: {
      "*": {
        "*": ["*"],
      },
    },
  },
};
const tempFile = JSON.parse(solc.compile(JSON.stringify(input)));
const contractFile = tempFile.contracts["Counter.sol"]["Counter"];
module.exports = contractFile;
```

### Deploy Contract

Create _ <mark style="color:blue;">deploy.js</mark>_

```
const Web3 = require("web3");
const contractFile = require("./compile");

const account_from = {
  privateKey: 'your private key',
  address: 'public address of your privateKey',
};

const rpcProvider = {
  development: 'http://frost-rpc.icenetwork.io:9933'
}

const bytecode = contractFile.evm.bytecode.object;
const abi = contractFile.abi;

const provider = new Web3(rpcProvider.development);

const web3 = new Web3(provider);

// Deploy contract

const deploy = async () => {
  console.log("Deploying contract....");
 
  // Create contract instance
  const result = await new web3.eth.Contract(abi);

  // Create constructor tx
  const resultTx = result.deploy({
    data: bytecode,
    arguments: [5]
  })
 
  // sign and send tx
  const createTx = await web3.eth.accounts.signTransaction(
    {
      data: resultTx.encodeABI(),
      gas: await resultTx.estimateGas(),
    },
    account_from.privateKey
  )

  // send tx and wait for receipt
  const createReceipt = await web3.eth.sendSignedTransaction(createTx.rawTransaction);
  console.log(`Contract deployed at address: ${createReceipt.contractAddress}`);

};

deploy();
```

Finally run following commands

```
node compile.js
node deploy.js
```

This should output the contract address.

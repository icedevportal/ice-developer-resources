---
cover: ../../../.gitbook/assets/ice_inkNew.png
coverY: 0
---

# Ink! Smart Contract Components

## **Contract Address**

An address is attached to a contract when it **** is uploaded and instantiated in the chain which we refer to as the contract address. Contract address maps to a specific runtime code that is executed when called by external clients. The underlying runtime code can be swapped for a contract address so that it calls a different set of runtime logic.

### **Contract Code Hash**

It's the unique hash value of the WASM code that is uploaded in the chain. We can use this hash value to delegate calls or even instantiate specific contracts and create its reference on another contract as well. The same contract code can be deployed as separate contracts with their own contract addresses and storage.&#x20;

### Contract ABI&#x20;

It's the interface exposed by a contract that provides its public function signatures and type information.

### Contract Storage&#x20;

Every contract is provided with persistent storage in the chain that the contract can access to store and retrieve values.&#x20;

###

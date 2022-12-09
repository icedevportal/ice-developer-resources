---
description: >-
  This article covers the procedures required to set up a development node for
  testing locally.
cover: ../.gitbook/assets/ICE-Cicles.gif
coverY: 0
---

# Local Standalone Blockchain

Developers looking to build smart contracts on ICE blockchain can run ICE blockchain locally, inspect the blockchain state, and test their code. Following are the steps to setup development node locally.

### Install Rust

_**If you are building the ICE/SNOW binary release manually**_, \
follow [**this article**](https://docs.substrate.io/install/) **** to install Rust and all the the packages essential for the build process.

{% hint style="info" %}
**Depending on the OS, Wasm toolchain might require manual installation.**

E.g. on macOS (Big Sur v11.6), Wasm is added using following command

`rustup target add wasm32-unknown-unknown --toolchain nightly-x86_64-apple-darwin`
{% endhint %}

### Prepare the ICE/SNOW Network binary

#### Option 1: Download the ICE/SNOW binary

Download the `ice-node` binary release from [here](https://github.com/web3labs/ice-substrate/releases).

#### Option 2: Build the binary release

The [ice-substrate ](https://github.com/web3labs/ice-substrate)repo's main branch contains the latest ICE code

```
git clone https://github.com/web3labs/ice-substrate.git
```

Build the code with the following command, which will generate the `ice-node` executable file inside `./target/release` folder

```
cargo build --release
```

### Run the local development node

```
./ice-node --dev
```

Once your node is running you should be able to see output similar to this on your terminal

![](<../.gitbook/assets/image (1) (1) (2) (1).png>)

### Connecting to Polkadot.js

Now you can use [polkadot explorer ](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/explorer)to communicate with the node. The websocket and RPC url for the locally running node are &#x20;

* **WS** - `ws://127.0.0.1:9944`
* **HTTP** - `http://127.0.0.1:9933`

{% hint style="info" %}
**NOTE: **_**** More about using polkadot explorer is_ [_here_](../explorer/ice-snow-explorer.md)__
{% endhint %}

### Configuring Metamask

Once the node is started and running , you can configure your metamask to the test node to start deploying smart contracts and building dapps on test node.

Configure network in your metamask according to following settings:

* Network Name: `ICE - local`
* RPC URL: `http://127.0.0.1:9933`
* ChainID: `42`
* Symbol:`ICZ`

{% hint style="info" %}
_Configuring metamask for SNOW/Arctic is_ [_here_](evm/configuring-metamask.md#steps)__
{% endhint %}

Now you will be able to make RPC calls to the local ICE node, [deploy Solidity smart contracts](evm/evm-and-solidity-smart-contracts/using-hardhat/), [interact with the smart contracts](evm/evm-and-solidity-smart-contracts/using-hardhat/interact-with-contracts-using-hardhat.md).

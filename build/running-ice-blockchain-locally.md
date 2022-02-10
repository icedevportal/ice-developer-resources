---
description: >-
  This article covers the procedures required to set up a development node for
  testing locally.
cover: ../.gitbook/assets/ICE-Cicles.gif
coverY: 0
---

# Running ICE blockchain locally

Developers looking to build smart contracts on ICE blockchain can run ICE blockchain locally, inspect the blockchain state, and test their code. Following are the steps to setup development node locally.

### Install Rust

If this is the first time you are installing Rust, run the following command.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

If you already have rust installed, please run the following command to update to the latest version

```
rustup update
```

### Configure your Rust environment

```
rustup update stable
rustup default stable
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

{% hint style="info" %}
**Depending on the OS, Wasm toolchain might require manual installation.**

E.g. on macOS (Big Sur v11.6), Wasm is added using following command

`rustup target add wasm32-unknown-unknown --toolchain nightly-x86_64-apple-darwin`
{% endhint %}

### Clone ICE node

The [ice-substrate ](https://github.com/web3labs/ice-substrate)repo's main branch contains the latest ICE code

```
git clone https://github.com/web3labs/ice-substrate.git
```

### Build the development node

```
cargo build --release
```

### Run the local development node

```
./target/release/ice-node --dev
```

Once your node is running you should be able to see output similar to this on your terminal

![](<../.gitbook/assets/image (1).png>)

### Connecting to Polkadot.js

Now you can use [polkadot explorer ](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/explorer)to communicate with the node. The websocket and RPC url for the locally running node are &#x20;

* **WS** - `ws://127.0.0.1:9944`
* **HTTP** - `http://127.0.0.1:9933`

{% hint style="info" %}
**NOTE: **_**** More about using polkadot explorer is_ [_here_](../polkadot.js-app/substrate-explorer-viewing-blocks-and-events.md)__
{% endhint %}

### Configuring Metamask

Once the node is started and running , you can configure your metamask to the test node to start deploying smart contracts and building dapps on test node.

Configure network in your metamask according to following settings:

* Network Name: `Ice local node`
* RPC URL: `http://127.0.0.1:9933`
* ChainID: `553`
* Symbol (Optional):`ICZ`

{% hint style="info" %}
**NOTE:** _More about configuring metamask is_ [_here_](../ice-testnet-details/network-endpoints/interacting-with-frost-using-metamask.md)__
{% endhint %}

Now you will be able to make RPC calls to the local ICE node, [deploy Solidity smart contracts](using-hardhat/), [interact with the smart contracts](using-hardhat/interact-with-contracts-using-hardhat.md).

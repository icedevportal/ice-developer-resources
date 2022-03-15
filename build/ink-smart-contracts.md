---
description: >-
  This article will show you how to deploy ink! smart contracts to the Frost
  testnet.
cover: ../.gitbook/assets/ice_Ink.png
coverY: 0
---

# Ink! Smart Contracts

Besides Solidity, ICE also supports writing smart contracts in [Ink](https://paritytech.github.io/ink-docs/)! , an embedded domain specific language (eDSL) for writing smart contracts in Rust. These smart contracts are compiled into [WebAssembly (wasm)](https://webassembly.org)  code, which is executed by the [Contracts Pallet](https://docs.substrate.io/v3/runtime/smart-contracts/#contracts-pallet)  of the ICE blockchain.

## Getting Started

### **Installing Prerequisites**

* Ensure you have [installed Rust](running-ice-blockchain-locally.md#install-rust)  and [configured your Rust environment](running-ice-blockchain-locally.md#configure-your-rust-environment)
* Add additional Rust configuration for Ink! contracts

```
rustup component add rust-src --toolchain nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

* Install [cargo-contract](https://github.com/paritytech/cargo-contract),  a CLI tool for setting up and managing WebAssembly smart contracts written using ink!.

```
cargo install cargo-contract --vers ^0.17 --force --locked
```

* Install the [binaryen](https://github.com/WebAssembly/binaryen)  package, which is used to optimize the WebAssembly bytecode of the contract

```
# For Ubuntu or Debian users
sudo apt install binaryen
# For MacOS users
brew install binaryen
```

{% hint style="info" %}
**NOTE:** If you're unable to find a version of binaryen compatible with your OS, you can download the [binary directly](https://github.com/WebAssembly/binaryen/releases). You can also install the package globally [using NPM](https://www.npmjs.com/package/binaryen).
{% endhint %}

### **Creating Flipper Contract**

We shall create a simple “[Flipper](https://github.com/paritytech/ink/blob/v3.0.0-rc8/examples/flipper/lib.rs)” contract, which allows users to store, retrieve and toggle a boolean value.

In your working directory, run:

```
cargo contract new flipper
```

This command will create a new project folder named flipper with the following content:

_**flipper**_&#x20;

&#x20;      ****       └─ _lib.rs_                    <-- Contract Source Code&#x20;

&#x20;     └─ _Cargo.toml_         <-- Rust Dependencies and ink! Configuration&#x20;

&#x20;     └─ _.gitignore_

### **Building the contract**

* To Compile the contract, run:

```
cargo +nightly contract build
```

After executing the above command, you should see **three files inside “target/ink” folder**; a **Wasm binary**, a **metadata file** (which contains the contract's ABI) and a **.contract file** which bundles both. This **.contract** file can be used to deploy your contract to a chain.

> _**NOTE**_: If you get _`parity-scale-codec` is ambiguous_ error while compiling the contract then update the following dependencies in your `cargo.toml` file.
>
> ```
> scale-info = { version = "2", default-features = false, features = ["derive"], optional = true } 
> scale = { package = "parity-scale-codec", version = "3", default-features = false, features = ["derive", "full"]
> ```

* You can also run tests for the contract by executing the following command:

```
cargo +nightly test
```

### **Deploying the Contract**

{% hint style="info" %}
**Note:** _To deploy Ink! contracts on ICE network, you should have_ [_Polkadot.js wallet_](https://docs.icenetwork.io/polkadot.js-app/advanced#installing-polkadot-js-wallet-extension) _extension installed on your browser. Further, the wallet should have enough balance to pay for the fees required during the contract deployment process._
{% endhint %}

The Ink! smart contract deployment is a two step process:

1. Putting your code on the blockchain
2. Creating an instance of your contract

With this pattern, contract code like the ERC20 standard can be put on the blockchain a single time, but instantiated any number of times, thus saving storage space on the chain.

Creating an instance of Ink! contracts on Frost Network will create a new AccountId (a wallet/account) which will store any balance managed by the smart contract and allow users to interact with the contract. Therefore, the contract balance should be greater than the Existensial Deposit required by the Frost Network

Head over to the [PolkadotJs App](https://polkadot.js.org/apps/)  to deploy the compiled flipper contract.&#x20;

* On the top Navbar, select _**Developer-**_> _**Contracts**_.

![](<../.gitbook/assets/image (5).png>)

* Select “Upload & deploy code” button.
* On the popup, Select the wallet to deploy the contract from, choose the “flipper.contract” file that was created after compiling the flipper contract, and give a proper name to the contract for display purpose.

![](https://lh3.googleusercontent.com/M1vB8lLEuIto7\_8e2FNHpZ4vsI2gsQ4bZi8Fif66a35YB0lif74OIZXjEsToDyE\_Y\_\_7mD7R-m5VZlWHvGENevnnmZm9NXtZ9SJwAOY7X\_FjUN7LALEcEbjs5hiU6Yk3DCLOOsRl)

* Provide the parameters required by the contract’s constructor method. For the Flipper contract, you can provide the default boolean value of _**False**_. You can adjust the maximum amount of gas that you want the contract deployment process to consume.

![](https://lh3.googleusercontent.com/eWvgPnaER0ureil2uPQEAFyPzKzzylEcaNLWbdjaZAFYiKoo9cjOCOg1sueM4JIjCvV27oAwMS\_2md9AGtEPVOEWlcmsSUiHlCgCVBReoOPJP0OqVNla4KQ-Wz1uhdwwBBdqB8og)

* Click on Deploy. Sign and send the transaction with your Polkadot.js wallet. You should see the following screen

![](https://lh5.googleusercontent.com/kYo4yBT5vkO3l-Z6x5jMl182FLsXyWAS0AniY-Nu81YR3vQqKV2BtrIFw7kq8R2281G52oSPaeQlMJJlhhRfpG1J3yKrJ5UHgg2rnxpc8LHspjKlUQ7CXcdDZWjskucwXv9xPcED)

It has two sections:&#x20;

* The “contracts” section is the actual instance of your deployed contract. You can call its read-only method _get()_ and execute the state-changing _flip()_ method.

![](<../.gitbook/assets/image (4).png>)

![](https://lh3.googleusercontent.com/iwbHyRuqtOhWYbUSLPcQBxTItJNRhXi4BN2ura0s8nIrL3VBJrbeCb-g5K7KQl5-Cy43oUSQvaTw9QZMeGQ06UOoohqim6mWaoK6nnV-Pb6\_sOk0GXF4CDUHRnWjoGUkA6Ca6C0W)

* The “code hashes” section is the reusable contract code that reside on-chain. If you want to deploy another instance of this same contract, you can do that from here with ease. All you need is to remember the hash (_beginning with 0x…_).

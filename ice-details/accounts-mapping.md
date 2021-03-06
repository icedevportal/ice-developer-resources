---
description: Ethereum - Substrate account Mapping
---

# Accounts Mapping

EVM pallet enables the Ethereum EVM capabilities on a native Substrate chain. To make use of EVM similar to any EVM-based blockchain, one should understand how an Ethereum account is mapped relative to the Substrate chain.

### Account Mapping

Every Ethereum address(20-byte) on the EVM is mapped with a unique ss58 address(32-byte) on the Substrate chain, which acts as a proxy to maintain balance for the Ethereum address. The said Substrate address is generated deterministically from the Ethereum address on funding.

The deterministically generated ss58 address is generated by the following steps:

* Consider a 20-byte Ethereum address: `0x6be02d1d3665660d22ff9624b7be0551ee1ac91b`
* Add bytes of `evm:` as prefix and concat it with the 20-byte Ethereum address bytes.
* Perform blake2b Hash on the concatenated bytes
* convert the hashed Hex to ss58 base address to get the Mapping Substrate account

Alternatively, one can run the script([substrate-address.js](https://github.com/web3labs/ice-network/tree/main/utils)) provided available with this repo, to generate a Substrate address from the Ethereum address.

### Converting Ethereum Address to substrate address and vice-versa

Head over to this [link](http://ss58-h160-convert.s3-website.us-east-2.amazonaws.com/) to easily convert your Ethereum address to substrate and vice versa.

Just select the input address format from the dropdown and enter the selected input format address in the input field and click on go. For example:

* Select the input address format to H160(ethereum)
* Enter your Ethereum address and click on go
* You will get your equivalent SS58(substrate) address
* In my case H160 and SS58 address were:

> H160 address: 0x7c0f5F59A22B657C8D9E21b44D2Dc0118fD2BE7B
>
> SS58 address: 5DLri6vcHLAGAs3kQFoE8wP9cG4gHfcqmNrFVZJT2tNMQREX

### Balance Mapping

Whenever the base Substrate account is funded with some units. A new account is created automatically if it doesn't exist & funds will be transferred from the God account/Faucet account to the created account.

During any transaction on the EVM, the funds are used by default from the mapped-Substrate address, the EVM always translates the 20-byte Ethereum address to the deterministically generated SS58 address.



To fund the Ethreum/Substrate account with Faucet, Please refer[#funding-substrate-or-ethereum-account-with-icy-testnet](faucet.md#funding-substrate-or-ethereum-account-with-icy-testnet "mention")

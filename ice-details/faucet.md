# Faucet

### Funding Substrate account with ICZ Testnet

This guide explains how to fund your Substrate & Ethereum account with ICZ tokens to interact and transact with Testnet or the EVM

{% hint style="info" %}
The network token for ICE will be ICY, but the Testnet denotes it as ICZ and can change in the future
{% endhint %}

#### Pre-requisite

This requires one to hold the private key to the substrate account or the Ethereum account in request.

* To create a Substrate account, refer [here](../polkadot.js-app/using-polkadot.js-app.md) for more details on the explorer app & goto accounts tab -> Add Account, to create a new one.
* To create an Ethereum account, use any Ethereum compatible wallets ([Metamask wallet](https://metamask.io/))

#### Faucet

| Network        | Link                                                                                                          | Note                                                                                                                             |
| -------------- | ------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Arctic testnet | Join this [Discord](https://discord.com/channels/880651922682560582/970759671117922366) link to request funds | <p>In the <code>dev-ice-faucet</code> guild,<br>type in <code>!send &#x3C;substrate/Ethereum address></code> &#x26; hit send</p> |

* Requesting address will be provisioned with **1000 ICZ** on **Arctic** testnet and a successful response.
* Users will have to wait for 6 hours between each request.

### Usage/Examples

Following commands use a sample account number, replace it with your own account to which you hold the private key.

**Funding Substrate account with ICZ**

Example command for valid ss58 account address

```
!send 5HWKSRyhAVnwioKWFZS3mvLQtqRc8Z2PsHfQL69tg4tJgqyC
```

**Funding Ethereum account with ICZ**

Example command for valid Ethereum address

```
!send 0x6D5bA807f8D8c7A4738C102E414D8e55F784E813
```

* After a successful transaction, the amount should be reflected in the respective wallet.
* To add the custom Testnet RPC details, refer here [Network Details](../ice-testnet-details/network-endpoints/)

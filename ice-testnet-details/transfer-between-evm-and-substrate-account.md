---
description: >-
  This article guides you through the process of transferring ICZ tokens form an
  EVM (H160) account to a Substrate(SS58) account and vice-versa.
---

# Transfer between EVM and Substrate Account

For this example, we have created two different accounts from two different wallets.

* H160 (from Metamask) : `0x7c0f5F59A22B657C8D9E21b44D2Dc0118fD2BE7B`
* SS58 (form Polkadot.js):  `5Fmqx9v6SEcCjDCZvgepLTQEYtGvzBCP49EzFaJhDgmKpgWU`

## Transfer ICZ from H160 to SS58

H160 accounts can only transfer to H160 formatted accounts. So, when someone wants to transfer assets from H160 to SS58 account, as a work around we can transfer assets into the mapped H160 address of the destination SS58 address.

### Converting SS58 to H160

We have to first convert our SS58 address to H160 address using this [conversion tool](http://ss58-h160-convert.s3-website.us-east-2.amazonaws.com/).

* Head over to conversion tool link above.
* Select the **Input address format** as **SS58(Substrate)**
* Paste our SS58 address into **Address** field and click on **Go.**
* It will output the mapped H160 format address of the SS58 address.

In our case,

**SS58**: `5Fmqx9v6SEcCjDCZvgepLTQEYtGvzBCP49EzFaJhDgmKpgWU`

**Mapped H160**: `0xa41502bf45df85989e153cec92158e3f5b6a9978`

We can use this mapped H160 as destination address where we want to send funds.

### Transferring funds using Metamask

{% hint style="info" %}
_**Note:** Make sure that Metamask is configured with the_ [_arctic testnet_](network-endpoints/interacting-with-arctic-using-metamask.md)__
{% endhint %}

* Open Metamask and click on **Send** button.
* Enter destination address as mapped H160 address: `0xa41502bf45df85989e153cec92158e3f5b6a9978`
* Enter the **Amount** of ICZ you want to send.
* Click on **Next** and then **Confirm** the transaction.



<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Send ICZ from H160 to SS58</p></figcaption></figure>

we've transferred 100 ICZ tokens to the mapped H160 account. This token, however, will not be added to the Substrate balance of account: `5Fmqx9v6SEcCjDCZvgepLTQEYtGvzBCP49EzFaJhDgmKpgWU` immediately.

This token is instead stored in the EVM deposit, which is effectively the balance of the mapped H160 account within the EVM sandbox. The original SS58 account must invoke the _**evm.withdraw**_ method to withdraw the tokens in the EVM deposit. It takes two parameters:

* **mapped H160 address** of the destination SS58&#x20;
* **amount** that was transferred (Currently 10^18 denomination).

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

## Transfer ICZ from SS58 to H160

Just like H160 address can only transfer to H160 address, a SS58 address can only transfer to a SS58 address.. So, as a work around we can transfer assets into the mapped SS58 address of the destination H160 address. We can again use the [conversion tool](http://ss58-h160-convert.s3-website.us-east-2.amazonaws.com/) to get SS58 address from H160.

### Converting H160 to SS58

Hence we have to first convert our SS58 address to H160 address using this [conversion tool](http://ss58-h160-convert.s3-website.us-east-2.amazonaws.com/).

* Head over to conversion tool link above.
* Select the **Input address format** as **H160(Ethereum)**
* Paste our H160 address into **Address** field and click on **Go.**
* It will output the mapped SS58 format address of the H160 address.

In our case,

**H160**: `0x7c0f5F59A22B657C8D9E21b44D2Dc0118fD2BE7B`

**Mapped SS58**: `5DLri6vcHLAGAs3kQFoE8wP9cG4gHfcqmNrFVZJT2tNMQREX`

We can use this mapped SS58 as destination address where we want to send funds.

### Transferring funds using Polkadot.js

Head over to [Polakdot.js](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Farctic-rpc.icenetwork.io%3A9944#/accounts).

* Click on **Account** dropdown and select **Transfer**
* Enter Source address in **Send from** input field (i.e. `5Fmqx9v6SEcCjDCZvgepLTQEYtGvzBCP49EzFaJhDgmKpgWU`)
* Enter mapped SS58 address in **Send to** field (i. e `5DLri6vcHLAGAs3kQFoE8wP9cG4gHfcqmNrFVZJT2tNMQREX )`
* Enter the **Amount** you want to send and click on **Make Transfer.**

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>Send ICZ from SS58 to H160</p></figcaption></figure>

Here we have transferred 100 ICZ to my H160 account, which can be directly seen in our Metamask wallet.

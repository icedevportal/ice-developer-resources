---
description: >-
  This article guides you through the process of transferring ICZ tokens form an
  EVM (H160) account to a Substrate(SS58) account and vice-versa.
---

# Transfer between EVM and Substrate Account

For this example, we have created two different accounts from two different wallets.

* H160 (from Metamask) : `0x7c0f5F59A22B657C8D9E21b44D2Dc0118fD2BE7B`
* SS58 (form Polkadot.js):  `5FpfUWrXt4goJZZhKdfLca1RvrJRgJ91WGQWpuR72ksTjtNH`

## Transfer ICZ from H160 to SS58

H160 accounts can only transfer to H160 formatted accounts. So, when someone wants to transfer assets from H160 to SS58 account, as a work around we can transfer assets into the mapped H160 address of the destination SS58 address.

### Converting SS58 to H160

We have to first convert our SS58 address to H160 address using this [conversion tool](http://ss58-h160-convert.s3-website.us-east-2.amazonaws.com/).

* Head over to conversion tool link above.
* Select the **Input address format** as **SS58(Substrate)**
* Paste our SS58 address into **Address** field and click on **Go.**
* It will output the mapped H160 format address of the SS58 address.

In our case,

**SS58**: `5FpfUWrXt4goJZZhKdfLca1RvrJRgJ91WGQWpuR72ksTjtNH`

**Mapped H160**: `0xa63b7ad340b0ce75a546c8d893ed7533c089d808`

We can use this mapped H160 as destination address where we want to send funds.

### Transferring funds using Metamask

{% hint style="info" %}
_**Note:** Make sure that Metamask is configured with the_ [_arctic testnet_](network-endpoints/interacting-with-arctic-using-metamask.md)__
{% endhint %}

* Open Metamask and click on **Send** button.
* Enter destination address as mapped H160 address: `0xa63b7ad340b0ce75a546c8d893ed7533c089d808`
* Enter the **Amount** of ICZ you want to send.
* Click on **Next** and then **Confirm** the transaction.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption><p>Send ICZ from H160 to SS58</p></figcaption></figure>

we have transferred 100 ICZ tokens to the mapped H160 account. We can confirm that this transaction happed by visiting [epirus explorer](https://arctic.epirus.io/transactions/0x06ab609cd6e708c8b0316f500768337e2872af6a220462ba827f05b1223f24dc).

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

This token, however, will not be added to the Substrate balance of account: `5FpfUWrXt4goJZZhKdfLca1RvrJRgJ91WGQWpuR72ksTjtNH` immediately.

This token is instead stored in the EVM deposit, which is effectively the balance of the mapped H160 account within the EVM sandbox. The original SS58 account must invoke the _**evm.withdraw**_ method to withdraw the tokens in the EVM deposit. It takes two parameters:

* **Mapped H160 (EVM) address** you want to withdraw the fund from
* **Amount** that you want to withdraw (Currently **10^18 denomination**).

So you need to go into your [polkadot.js apps](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Farctic-rpc.icenetwork.io%3A9944#/explorer). Then navigate to **Developer** > **Extrinsics.**  Then, select the **SNOW account** where you have transferred the tokens.

Finally select **evm** > **withdraw(address,value),** and the enter parameters given above, and sub

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

We can verify the above transaction happened by visiting[ subscan explorer](https://arctic.subscan.io/extrinsic/0xc5bbe7ba1bb48d5858eca6a29eb38dbc96eaf1f0165784c359371c4e4a358e56).

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**NOTE:** _You can check increment of you balance buy visiting_ [_account page_](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Farctic-rpc.icenetwork.io%3A9944#/accounts) _in polkadot.js App_
{% endhint %}

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
* Enter Source address in **Send from** input field (i.e. `5FpfUWrXt4goJZZhKdfLca1RvrJRgJ91WGQWpuR72ksTjtNH`)
* Enter mapped SS58 address in **Send to** field (i. e `5DLri6vcHLAGAs3kQFoE8wP9cG4gHfcqmNrFVZJT2tNMQREX )`
* Enter the **Amount** you want to send and click on **Make Transfer.**

<figure><img src="../.gitbook/assets/image (3) (2).png" alt=""><figcaption></figcaption></figure>

Here we have transferred 50 ICZ to our H160 account, which can be directly seen in our Metamask wallet.

This transaction can also be seen in [subscan explorer](https://arctic.subscan.io/extrinsic/0x15e6cd2b85aa302034be3f9820a30cde75b4e3f7e1ba3325cb24cdf9c95937fd)

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

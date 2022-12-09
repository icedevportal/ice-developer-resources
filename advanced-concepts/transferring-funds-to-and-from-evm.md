# Transferring Funds to and from EVM

You can use [**Hana Wallet**](https://chrome.google.com/webstore/detail/hana-wallet/jfdlamikmbghhapbgfoogdffldioobgl) to easily transfer funds between Substrate and EVM out of the box. [**Follow this article** ](https://medium.com/@hanawallet/moving-icz-between-snow-snow-evm-aa3b1e50c369)for step by step guide on making the transfer.

## Transfer ICZ from SNOW to Ethereum (H160) Address

1. Get your Sender SNOW account ready and head over to [**SNOW Address Converter**](https://snow-address-converter.netlify.app/)**.**
2. Select **H160 (Ethereum)** option on the **Input address format** field.
3.  Enter the **receiving** **Ethereum (H160) account address** and click on **Go!**.

    <figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption><p>Converting H160 address to SNOW Address format</p></figcaption></figure>


4. Copy the **mapped SNOW address** and send the desired amount of ICZ to this address.
5. The received ICZ will be shown on the **receiver** **H160 account**.

## Transfer ICZ from EVM to Substrate

1. Get your **Sender Ethereum (H160) account** ready and head over to [**SNOW Address Converter**](https://snow-address-converter.netlify.app/)**.**
2. Select **SNOW (mainnet/testnet)** option on the **Input address format** field.
3.  Enter the **receiving** **SNOW account address** and click on **Go!**.

    <figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>Converting SNOW Address to H160 address format</p></figcaption></figure>
4. Copy the **mapped H160 address** and send the desired amount of ICZ to this address.
5. The **receiver wallet** should now call the **EVM pallet's  `withdraw`** extrinsic with the following parameter:

```
withdraw(
    mapped H160 address of the destination SNOW address, 
    amount that was transferred (ICZ value multiplied by 10^18)
)
```

This can be achieved via **Polkadot.js app** (_Developer -> Extrinsic -> EVM -> withdraw_)&#x20;

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>Calling Withdraw from Polkadot.js app</p></figcaption></figure>

or from **within Hana wallet**.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

6\. The received ICZ will be shown on the **receiver** **Ethereum (H160) account**.\

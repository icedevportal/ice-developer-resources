---
description: Verify EVM Contract to interact with its read-write methods
---

# Verifying Solidity Contracts

Verifying EVM contracts allows you to interact with their read-write methods directly from the Epirus  Explorer.

*   Head over to [Arctic Epirus EVM Explorer](https://arctic.epirus.io/) and select **contracts** on the left pane.

    <figure><img src="../../.gitbook/assets/Screenshot from 2022-12-12 15-36-54.png" alt=""><figcaption></figcaption></figure>
*   Select the contract address that you want to verify.

    <figure><img src="../../.gitbook/assets/Screenshot from 2022-12-12 15-37-38.png" alt=""><figcaption></figcaption></figure>


*   Click on the **Sources** tab option.

    <figure><img src="../../.gitbook/assets/Screenshot from 2022-12-12 15-37-54.png" alt=""><figcaption></figcaption></figure>


* Drag and Drop your **contract metadata** file (.json) and the **Solidity contract** file (.sol). Then click on **Verify Contract Sources**.

<figure><img src="../../.gitbook/assets/Screenshot from 2022-12-12 16-33-55.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Hardhat compiled _****_ Contract metadata can be found inside _**artifacts/build-info**_ in the working folder.\
Using inappropriate metadata json files will not allow you to make the verification.
{% endhint %}

* You will be presented with a screen saying **Contract Source Code Verified** and can interact with Read/Write methods of the contract.

<figure><img src="../../.gitbook/assets/Screenshot from 2022-12-12 16-34-18.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot from 2022-12-12 17-18-29.png" alt=""><figcaption></figcaption></figure>

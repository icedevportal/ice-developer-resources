---
cover: ../../.gitbook/assets/1_W0eKVsybZ6TdxV8UYJX5Yg_midpolkadotjs.jpg
coverY: 0
---

# Making EVM RPC calls

RPC (Remote Procedure Call) is a collection of protocols and interfaces through which the client communicates with the blockchain system. The user can utilize the RPC interface to retrieve blockchain-related information (such as block number, blocks, node connectivity, and so on) and make transaction requests.

### Making RPC calls in polkadot.js app

* Select RPC calls from the Developer option on the navigation bar.

![](<../../.gitbook/assets/image (4) (1) (1) (1).png>)

* To get details about EVM transactions like contract deployment, state changing calls, etc, select **eth -> getTransactionReceipt(hash**). Enter the **EVM transaction hash** that you want to inspect, and click on **Submit RPC call**.

![](<../../.gitbook/assets/image (3) (1) (1) (1).png>)

* Other RPC endpoints that might be useful for Ethereum developers are as follows:
  * **getBlockByHash(hash, full) :** Get EVM block details by its hash

{% hint style="info" %}
Arguments:

**hash:** 32 Bytes - Hash of a block

**full:** if TRUE, returns the full transaction objects. If FALSE, returns only the hashes of the transactions.
{% endhint %}

* **getBalance(address, number):** Fetch balance of the provided H160 (Ethereum) Address

{% hint style="info" %}
Arguments:

**address:** Ethereum address to check for balance

**number**(optional): hex value of block number
{% endhint %}

* **getBlockByNumber(block, full):** Get EVM block details by its block number

{% hint style="info" %}
Arguments:

**block:** hex value of a block number

**full:** Boolean, if TRUE, returns full transaction objects. If FALSE, returns only hashes of transactions.
{% endhint %}




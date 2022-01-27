---
cover: ../.gitbook/assets/1_W0eKVsybZ6TdxV8UYJX5Yg_midpolkadotjs.jpg
coverY: 0
---

# Making EVM RPC calls

* Select RPC calls from the Developer option on the navigation bar.

![](<../.gitbook/assets/image (4).png>)

* To get details about EVM transactions like contract deployment, state changing calls, etc, select **eth -> getTransactionReceipt(hash**). Enter the **EVM transaction hash** that you want to inspect, and click on **Submit RPC call**.

![](<../.gitbook/assets/image (3).png>)

* Other RPC endpoints that might be useful for Ethereum developers are as follows:
  * **getBlockByHash(hash, full) :** Get EVM block details by its hash
  * **getBalance(address, number):** Fetch balance of the provided H160 (Ethereum) Address
  * **getBlockByNumber(block, full):** Get EVM block details by its block number




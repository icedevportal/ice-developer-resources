---
description: >-
  Polkadot.js app is the portal into the ICE test network. It allows users to
  view transactions, blocks, events, transfer balance, query blockchains and
  create transactions.
cover: ../.gitbook/assets/1_W0eKVsybZ6TdxV8UYJX5Yg_midpolkadotjs.jpg
coverY: 0
---

# Using Polkadot.js App

To use polkadot.js app as an explorer, please follow the steps below:

* Go to the [polkadot.js](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Ffrost-rpc.icenetwork.io%3A9944#/explorer) explorer page for Frost
* In a separate tab, open [https://frost-rpc.icenetwork.io:9944](https://frost-rpc.icenetwork.io:9944). This is for your browser to download the ssl certificate for frost-rpc.icenetwork.io, that is used by polkadot.js to make a web socket connection to the Frost node.

You might see one of the following warnings in your browser:

* **Chrome:** You might see the following warning `Your connection is not private`. Please click on **Advanced** > **Proceed to frost-rpc.icenetwork.io (unsafe)**

![](<../.gitbook/assets/image (4) (1).png>)

* **Brave:** You might see the following warning `Your connection is not private`. Please click on **Advanced** > **Proceed to frost-rpc.icenetwork.io (unsafe).**                                                   If you are unable to get **Advanced** button then click on browser body and type `thisisunsafe.`

![](../.gitbook/assets/273455507\_352716266490671\_7958131310511955853\_n.png)

* **Firefox:** You might see the following warning `Warning: Potential Security Risk Ahead`. Please click on **Advanced** > **Accept the risk and continue.**

![](<../.gitbook/assets/Screenshot 2022-02-10 113220.png>)

* You will see the following message in your browser : _WebSocket Protocol Error: Unable to parse WebSocket key._ This is expected.

![](<../.gitbook/assets/image (7).png>)

* Go back to the [polkadot.js](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Ffrost-rpc.icenetwork.io%3A9944#/explorer) explorer page for Frost and it will start working now.

Now you are ready to query and interact with the **Frost Network** on ICE blockchain



{% content-ref url="explorer/" %}
[explorer](explorer/)
{% endcontent-ref %}

{% content-ref url="making-evm-rpc-calls.md" %}
[making-evm-rpc-calls.md](making-evm-rpc-calls.md)
{% endcontent-ref %}

{% content-ref url="advanced.md" %}
[advanced.md](advanced.md)
{% endcontent-ref %}

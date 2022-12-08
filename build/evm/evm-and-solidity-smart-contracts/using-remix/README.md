---
cover: ../../../../.gitbook/assets/ice+remix.png
coverY: 0
---

# Using Remix

Remix is one of the most popular Ethereum programming environments for smart contracts. And due to ICE's Ethereum compatibility, Remix can be directly used to deploy smart contracts on ICE testnet or ICE development node

This post guides you through the process of creating and deploying smart contracts in ICE node using [Remix IDE](https://remix.ethereum.org/).&#x20;

For this process, make sure you meet the following prerequisite requirements:

* Metamask wallet extension in you browser, [connected to SNOW/Arctic](../../configuring-metamask.md#steps)
* Account with funds

{% hint style="info" %}
Head over to [Network](../../../network-endpoints.md) page to configure your account and to [Facuet](../../../faucet/) regarding funding information
{% endhint %}

### Getting started with Remix

* Head over to [Remix IDE](https://remix.ethereum.org/) official site to launch it.
* Create a workspace and a file in it named _`MyToken.Sol`_ in root directory.

![](https://lh6.googleusercontent.com/BPf2-QuVakIQXQo7AQeJHyLCNRS0hTRO7IxGnmP\_WI5l94L3iDfLSy1hY-ONm8l8PR5A0mjWHdhBPp\_CrhUsuOAFwA7C27lsX9357iY66zZEtZKtUyYLkomt-aDUvjPpw5HODPul)

* Paste following code in _`MyToken.sol`_

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract MyToken is ERC20, Ownable {
    constructor() ERC20("MyToken", "MTK") {
        _mint(msg.sender, 1000 * 10 ** decimals());
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }
}
```

{% hint style="info" %}
**NOTE:** This is a mintable ERC20 contract based on openzeppelin. It creates MyToken with symbol ‘MTK’ and initially mints 1000 MTK to the owner of the contract. You can generate this code from [OpenZeppelin](https://wizard.openzeppelin.com/) contract wizard
{% endhint %}

* Navigate to the solidity compiler  from the left side navigation and then click on Compile _`MyToken.sol`_

![](https://lh4.googleusercontent.com/Sz2l9fPDOCblfzz\_GF\_0rCLxAn\_YSjHM6\_-rb8yjUOhQDebmBvhgB0H6DGI7BHvwmR79Gm6cgrr8A3SVX8Xs1SzuJ2CqrBPBMmxycpNdT1FoTisWui2idKIi1XrIMURFmfYkVpNP)

Remix will download all the openzeppelin dependencies and compiles the contract

* Deploy the contract
  1. Navigate to the deploy and run transaction tab from left side navigation
  2. Change the environment to injected web3 from **Environment** dropdown. This will invoke the metamask extension in your browser. Make sure your metamask is configured to ICE testnet (Arctic) ([configure metamask](../../configuring-metamask.md#steps)).
  3. Select the account from metamask and confirm the connection
  4. From contracts dropdown select MyToken.sol and click on **Deploy** button

![](https://lh4.googleusercontent.com/Tj6hSn5tGnzUQWDotDUoG7byJViYmDQ31gipuF3nBGCHvdl3NxHvi9akipIJ6Mh8\_UgR3suFFJ5L2TsS7WjqHcDcfVNtKIesE\_INR59AJKeGh-SkG8MldbrbRr-PUu--dIIqnXTU)

* You will be asked to confirm the transaction through metamak popup , **confirm** it and wait till it is deployed.
* The contract details will appear under **deployed contracts** in remix

![](https://lh3.googleusercontent.com/cdIEPB9ZBpWJBU1S8JQGVOK2Bn4nmnt\_soAhc5vJOjoznBwk754hBjZpomusVGO5FJJcxdMlsFLJU4T4N2O2DkQ4aVenkI1YTnR6gMKDsqbGmnKCF-x8J4NrbXnn-oTB2Vz-zUC6)

Hence we deployed ERC20 token using Remix on ICE testnet node


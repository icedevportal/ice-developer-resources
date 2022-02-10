---
description: >-
  This article will show you how to interact with recently deployed smart
  contract on ice using hardhat
cover: ../../.gitbook/assets/1_W0eKVsybZ6TdxV8UYJX5Yg_midhardhat.jpg
coverY: 0
---

# Interact with contracts using Hardhat

### Launch hardhat console by running:

```
npx hardhat console --network testnet
```

Then, one by one, add the following lines of code. To begin, we construct a local instance of Token.sol contract

```
const MyToken = await ethers.getContractFactory('MyToken')
```

Next, connect this instance to an existing one by passing in the address we obtained when deploying the contract

```
const myToken = MyToken.attach('0xfCf562c65247A9fE4eaa3eb360d4223440410078')
```

Let’s call the methods of the contract now First transfer some tokens to a address by calling transfer() from contract

```
await myToken.transfer('0x758e3ACDBFb3818d49587418241E29E257Bd9308', 100)
```

You will get output similar to this:

![](<../../.gitbook/assets/image (2) (1).png>)

{% hint style="info" %}
NOTE: We initially pre-minted 1000 tokens so we can transfer upto 1000 token without minting another token
{% endhint %}



Then check the balance of available tokens in the address where we just transferred token by calling balanceOf() method

```
await myToken.balanceOf('0x758e3ACDBFb3818d49587418241E29E257Bd9308')
```

This should output 100 in the console.


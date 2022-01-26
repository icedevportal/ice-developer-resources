---
description: >-
  This article will show you how to interact with recently deployed smart
  contract on ice using truffle
cover: ../../.gitbook/assets/1_W0eKVsybZ6TdxV8UYJX5Yg_truffle (1).png
coverY: 0
---

# Interact with contracts using truffle

We can look at the javascript object MetaCoin supplied by truffle in the truffle console.

* Open truffle console

```
truffle console --network testnet
```

* Create instance for contract MetaCoin

```
truffle(testnet)> let instance = await MetaCoin.deployed()
```

* Making a transaction by calling sendCoin method from contract

```
truffle(testnet)> let accounts = await web3.eth.getAccounts()
truffle(testnet)> instance.sendCoin(accounts[1], 10, {from: accounts[0]})
```

{% hint style="info" %}
**NOTE**: if there is only one address in accounts then try replacing accounts\[1] by any other metamask account address
{% endhint %}

Next you should be able to see similar output

![ ](https://lh6.googleusercontent.com/B8nfTYuV9uBO-XBctrOm8uLsT-Sp9TTABZ2za5zPJvdHtEvgyGbWvc1iu6xWUvdzKvIlduZZ6OhstAXnIFo4Hpwt08BHmfYMmaQOTzMQXVpRS1kWwFLzc0CA9wtZstvArVBexSkS)

* Check balance of address by calling getBalance method of contract

```
truffle(testnet)> let balance = await instance.getBalance(accounts[1])
truffle(testnet)> balance.toNumber() // returns 10
//accounts[1] is the address we send coins to
```

